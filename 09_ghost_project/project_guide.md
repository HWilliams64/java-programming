# Ghost Project: Build, Test, and Package Your Player

CSC-239 · Module 9

This project combines your Java methods, collections, classes, interfaces, exceptions, and text-file work. You and your partner will build a player that competes against another program. The supplied **arbiter** is the program that starts and ends the game, announces turns, and checks the rules. Your player communicates through the shared text file that the arbiter supplies.

This module uses a project guide and Canvas pages. Work in the Java editor and terminal in your Grader Than Workspace.

## Learning goals

By the end of your project work, you should be able to:

- Explain which program may write each message in a game.
- Combine the supplied components into one player that follows the game rules.
- Launch a packaged player with the shared-file path supplied at startup.
- Use controlled scenarios and the provided arbiter to find and correct failures.

The [Ghost project specification](https://docs.google.com/document/d/1bwWAA_75oN1qiB8wt9ufGmh41b-K37NeA0Ey8hLySQA/edit?usp=sharing) and the instructor-provided project files control the required interfaces and submission. Keep those files beside this guide while you work. Tutorial names below do not replace their required names or methods.

## 1. Trace the game before connecting the program

A **game protocol** is the agreed set of messages and turn rules that cooperating programs follow. The **word fragment** is the current sequence of chosen letters. Each fragment must remain the beginning of at least one dictionary word.

A **legal move** sends one permitted ASCII alphabetic letter in the required format, only when it is your team's turn. ASCII here means the ordinary English letters; digits, punctuation, and other letter systems are not valid choices for this project. A correctly formatted move can still lose the game if its letter completes a word or creates an impossible fragment.

The assignment uses these rules:

- Add one letter to the end of the fragment on each turn.
- The player who completes a dictionary word with more than four characters loses. That means five or more characters.
- The player who makes a fragment that cannot begin any dictionary word loses.
- A response later than 15 seconds or a response that violates the text format can lose the game.
- Write only on your team's turn, and stop responding after GAME_OVER.

Remove whitespace from the team name and use uppercase. For example, Team 1 becomes TEAM1. Use the supplied TurnParser to interpret and format messages; inspect its actual methods instead of guessing names.

| Message | Writer and meaning |
|---|---|
| GAME_START | The arbiter announces the start. |
| TEAM1:TURN | The arbiter gives TEAM1 a turn. |
| TEAM1:T | TEAM1 submits the letter T on that turn. |
| TEAM2:TURN | The arbiter gives TEAM2 a turn. |
| GAME_OVER | The arbiter announces the end. |

The colon separates the team name from TURN or the chosen letter. A player sends its letter; it does not send a replacement TURN announcement.

### Practice: identify the writer and the fragment

For this paper exercise only, use the tiny dictionary THERE, THEIR, and THEORY. It is not the arbiter's real dictionary. Read this controlled transcript from top to bottom. Record the writer, the resulting fragment after each letter, and the first losing move.

```text
GAME_START
TEAM1:TURN
TEAM1:T
TEAM2:TURN
TEAM2:H
TEAM1:TURN
TEAM1:E
TEAM2:TURN
TEAM2:R
TEAM1:TURN
TEAM1:E
GAME_OVER
```

Your trace and explanation:

<details>
<summary>Show answer</summary>

The arbiter writes GAME_START, each TURN announcement, and GAME_OVER. Players write only their own letter messages. The fragments are T, TH, THE, THER, and THERE. The last TEAM1:E completes THERE, a five-character dictionary word, so TEAM1 loses. A TURN line does not add letters. Completing a word and merely matching a prefix are different checks; both matter to the decision.

</details>

## 2. Check the components you are connecting

Retrieve your Module 8 work and inspect the exact project starter files. The course plan names FileTextReader, FileTextWriter, AbstractFileMonitor, and AbstractDictionary for the earlier assignment, along with your FileManager and Dictionary implementations. The project also supplies TurnParser. Use the actual starter files to settle required method names, parameters, return types, and any naming differences in the older explanatory document.

Create a small responsibility table before writing the coordinating code:

| Responsibility | Evidence to record |
|---|---|
| Read the shared file | Required method, returned value, and missing-file behavior. |
| Notice a new game message | Required monitor operation and how it reports changes. |
| Interpret a turn | Actual TurnParser method and a known input/result pair. |
| Check words and prefixes | Known complete word, known prefix, and impossible fragment. |
| Format and write a response | Actual formatting method, writing method, and expected text. |
| Coordinate game state | How the current fragment, team, processed message, and end condition are retained. |

Explain each component in ordinary language to your partner. Then demonstrate a small passing check for it. A method mentioned in a document is not evidence that your implementation behaves correctly.

## 3. Connect one turn from input to response

Use this sequence to reason about one new message:

1. Read through the required file component and interpret the message through the supplied parser.
2. Update the state your player needs, including the fragment and whether the game has ended.
3. If this is a new turn for your team, choose a letter using dictionary evidence.
4. Format that team's letter response and write it through the required component.
5. Record enough processed-message context to avoid answering the same observed turn twice.

TEAM1:TURN appears more than once in a complete game. Distinguish a repeated observation of the same message from a later new turn; comparing only the recurring text is not a complete turn-identity rule. Use the supplied monitor/parser behavior and the message history they expose to make that distinction.

For each candidate letter, ask whether the new fragment can begin a dictionary word and whether it already completes a losing word. The specification requires a logical decision; selecting only a random letter does not meet that expectation. Count the letters still needed and alternate turns to predict who would complete a candidate word. A longer candidate may contain a shorter completed word that changes the result. A locally safe move is not proof of an optimal strategy.

### Practice: explain when a player should write

Your player is TEAM1. Describe its behavior in each case: a new TEAM2:TURN, a new TEAM1:TURN, an unchanged observation of the TEAM1 turn already answered, and GAME_OVER. Explain what evidence identifies the new turn.

<details>
<summary>Show answer</summary>

TEAM1 does not answer TEAM2's turn. It answers a new own-turn announcement once with one formatted letter. It does not answer an unchanged message again, and it stops sending moves after GAME_OVER. A later own turn may have the same text as an earlier one, so use the actual message/monitor contract and retained processed state to distinguish those events. Do not invent an unprovided parser method or assume that the shared file always contains only one line.

</details>

## 4. Make the shared-file path an explicit input

A **runtime argument** is a String supplied after the launch command and received in main's args array. The arbiter supplies one argument: the shared-file path. Your player uses args[0] for that path. When launching manually, check the argument count before reading that element so a missing argument gives a useful message.

A path containing spaces must still arrive as one argument. Quote the entire path in the terminal command. Resolve any other data your player needs, such as its dictionary, using a documented rule; do not depend on a path that exists only in your current editor session.

The following is a separate tutorial probe, not a Ghost implementation. It checks argument and file-reading mechanics:

```java
import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;

public class ArgumentProbe {
    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("Usage: java -jar argument-probe.jar <shared-file-path>");
            return;
        }
        Path shared = Path.of(args[0]);
        try {
            System.out.println("Arguments: " + args.length);
            System.out.println("File: " + shared.getFileName());
            System.out.print(Files.readString(shared, StandardCharsets.UTF_8));
        } catch (IOException problem) {
            System.out.println("Cannot read shared file.");
        }
    }
}
```

Save it as ArgumentProbe.java in a separate scratch directory. Create a subdirectory named game files and a UTF-8 file named shared state.txt inside it. Put these two lines in the file, ending each with a newline:

```text
GAME_START
TEAM1:TURN
```

## 5. Package a runnable JAR

A **runnable JAR** is a Java archive with an entry point that lets java -jar start the application. The archive must contain compiled classes. Its entry point names the class with the main method.

For the separate ArgumentProbe fixture, run these commands from its scratch directory:

```bash
javac -d classes ArgumentProbe.java
jar --create --file argument-probe.jar --main-class ArgumentProbe -C classes .
java -jar argument-probe.jar "game files/shared state.txt"
```

javac compiles the source into the classes directory. The jar command packages that directory and records ArgumentProbe as the starting class. The -C option changes the directory from which jar reads its input; the final dot includes the contents of that directory. The last command passes one quoted path to the program.

Expected probe output:

```text
Arguments: 1
File: shared state.txt
GAME_START
TEAM1:TURN
```

Use the same packaging idea with your player's actual main class and required compiled classes. Your editor may also offer packaging tools. Check that the resulting JAR launches correctly outside the editor.

### Practice: verify the package, not just the editor

Predict and test the probe with no argument and with a nonexistent file. Then copy the JAR and its test data into another directory and launch it there with the correct path. Explain what each check tells you.

<details>
<summary>Show answer</summary>

With no argument, the probe prints its Usage message and returns before indexing args. With a nonexistent file, it prints the argument count and requested filename, then Cannot read shared file. Running the copied JAR with copied data from another directory checks that the archive contains the classes it needs and that the supplied path is used. These checks verify only the probe's mechanics. They do not establish that a Ghost player parses turns, chooses letters, or cooperates with the arbiter correctly.

</details>

## 6. Test cooperating components and complete games

An **integration test** checks that cooperating components work together under their real shared contract. Passing separate dictionary and file checks is useful, but it does not prove that your whole player responds to the arbiter correctly.

First use controlled shared-file scenarios to inspect one behavior at a time. Then run against the provided arbiter; the project specification requires at least this test. The arbiter's graphical window appears in Workspace Desktop. Use the supplied Java Workspace and its Desktop option. The player communicates through files even when the arbiter has a graphical window.

Use the actual provided arbiter and player filenames in the launch instructions. A typical two-player launch has this shape; replace every example path before running it:

```bash
java -jar "/path/to/GhostApp.jar" "/path/to/player-one.jar" "/path/to/player-two.jar"
```

The supplied Workspace already includes JavaFX. The older project document's separate JavaFX installation and module-flag examples do not apply to this environment. Use the assignment's greater-than-four completed-word rule when checking the arbiter configuration; example commands that discuss other lengths do not change that rule.

Record expected and actual behavior for each row. Use the provided interfaces and arbiter to construct the scenario instead of guessing the required methods.

| Scenario | Evidence to collect |
|---|---|
| GAME_START | Required state initializes without an early letter response. |
| New own turn | Exactly one correctly formatted response within the required time. |
| Opponent turn | No own-team response. |
| Repeated observation | No duplicate response to an already handled turn. |
| Valid prefix | The chosen extension remains supported by dictionary evidence. |
| Completed word of five or more characters | The losing completion is recognized in the controlled test. |
| Impossible fragment | The invalid-prefix result is detected. |
| Missing or malformed input | Observed failure is handled according to the supplied contract and remains diagnosable. |
| Turn timeout | The test records the arbiter's timeout result. |
| GAME_OVER | No further letter is written; the player ends cleanly. |
| Quoted path with spaces | The entire shared-file path arrives as one argument. |
| Clean-location package | The JAR launches with its required runtime data outside the build directory. |

Test two separately packaged players with the arbiter. If you test with a classmate, agree on which runtime files to exchange. Recheck affected scenarios after a program change and keep a short record of the fix and result.

## 7. Review and submit the required files

The supplied specification asks for one submission per team to the Moodle assignment page. Submit the runnable JAR, or a ZIP containing the JAR and any additional files needed at runtime. If you use the same dictionary as the arbiter, the specification says that dictionary need not be submitted again.

This project is not submitted through Grader Than. Do not submit source code. The instructor requests the runnable package and required runtime files. Use the instructor's posted due date and grading information.

Before submitting, have your partner launch the exact files you intend to submit from a clean location. Record the launch command, required data, and a passing arbiter test. Explain the strategy and its limits, plus one failure that your tests helped you fix.

## Reflection and next connection

Which problem was easiest to miss when testing one component alone? Explain the message, state change, and observed result that exposed it. In the Canvas discussion, share a design or testing lesson without posting your complete project solution.

Module 10 returns to language techniques: you will pass behavior through lambda expressions and process collections with stream pipelines. Those techniques build on your interface and collection work; they do not replace the Ghost protocol requirements.

## Supplemental Reading

- [Ghost project specification](https://docs.google.com/document/d/1bwWAA_75oN1qiB8wt9ufGmh41b-K37NeA0Ey8hLySQA/edit?usp=sharing) provides the authoritative game and submission requirements.
- [Java 21 java command](https://docs.oracle.com/en/java/javase/21/docs/specs/man/java.html) documents launching a main class or executable JAR and supplying arguments.
- [Java 21 javac command](https://docs.oracle.com/en/java/javase/21/docs/specs/man/javac.html) explains compiling classes and choosing their output directory.
- [Java 21 jar command](https://docs.oracle.com/en/java/javase/21/docs/specs/man/jar.html) documents archive creation, main-class metadata, and -C input-directory handling.
- [Java 21 Files API](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/nio/file/Files.html) documents the UTF-8 file-reading operation used by the separate probe.
