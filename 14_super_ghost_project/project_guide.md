# Super Ghost: Integrate the Graphical Interface, Protocol, and Player

In this module, you will learn to connect a graphical user interface, shared game data, and background work in Java, then test and package the resulting application.

CSC-239 · Module 14

Your team is building a **player**, the Java application that helps choose and submit your team's moves. A separate supplied program, the **arbiter**, announces whose turn it is, checks moves, and ends the game. The **word fragment** is the ordered text built from the letters already played. Your next move adds one letter at the front or back of that text.

The player needs two kinds of information. A **dictionary** supplies the words used to judge possible fragments. A **shared binary file** carries game records that the player and arbiter exchange using the supplied Java classes. The arbiter owns the current turn and game-over state. Your player reads that state and submits its own action when allowed; it does not assign itself a turn.

Success means a runnable player that shows the current fragment, accepts a letter and placement choice, follows the agreed game messages, and stays responsive while selection work runs. You will test the packaged application with the supplied arbiter, then submit the required runtime files through the instructor's Canvas project assignment.

Before connecting components, obtain the current project skeleton, SGhostApp.jar, and the required dictionary and runtime files from the instructor. Keep their actual paths and filenames in your project notes. Use the Java editor, terminal, and Desktop in your existing Grader Than Workspace. The [Module 14 glossary](terms.md) explains the project terms used here.

Keep a project record of the questions, planned checks, actual results, and corrections in this guide. The labeled response prompts identify what to write in your own editable project notes. This record supports your work; it does not add a new submission requirement.

Keep the [Super Ghost project specification](https://docs.google.com/document/d/1G8VicM-wPkyrYYa20R4_cWp3P90b_1tGd23cuooOywU/edit?usp=sharing) and supplied project files beside this guide. Their actual declarations control method names, parameters, return types, and required behavior. This guide helps you organize and test the work; it does not replace the skeleton with tutorial classes.

## Learning goals

- Explain how front and back moves change dictionary checks.
- Preserve the supplied shared classes and follow the arbiter’s binary protocol.
- Keep background selection separate from short GUI updates.
- Test and package a player with the required controls and runtime files.

## 1. Compare the two games

Retrieve the original Ghost project’s turn discipline, dictionary checks, packaging, and integration tests. Then mark the changes:

| Concern | Ghost | Super Ghost |
|---|---|---|
| Letter location | Append at the end. | Add at the front or back. |
| Dictionary relationship | Fragment must be a prefix. | Fragment may be a substring. |
| Completed-word rule in the overview | More than four characters. | At least six characters. |
| Turn limit in the specification | 15 seconds. | 60 seconds. |
| Shared representation | Text messages. | Supplied serialized game-data objects. |
| Player interaction | Console/file player. | Required GUI with fragment, letter, and location controls. |

**Substring viability** means that the fragment appears as one continuous sequence anywhere in a dictionary word. It cannot skip or reorder letters. A **move location** is the front-or-back choice sent with a letter. Both choices affect the resulting fragment.

The overview says that completing a dictionary word of at least six characters loses. The detailed paragraph about minWordLength is not fully consistent about the boundary. Read the actual arbiter setting and test completed words immediately below, at, and above that setting. Record a discrepancy for the instructor instead of silently choosing a different rule. Keep the configured value available to your decision logic.

### Practice: check both ends

For this paper exercise only, use the dictionary PLANET and PLANER and the fragment LAN. This is controlled practice data, not the arbiter’s dictionary.

1. Add P at the front. Write the resulting fragment and one supporting word.
2. Add E at the back of the original LAN. Write the result and one supporting word.
3. Would a prefix-only search accept the original fragment LAN?
4. Is NAL a substring of either word? Explain why the same letters are insufficient.
5. Does finding one viable move prove it is the best move against an opponent?

My fragments and supporting words:

My explanation of the search rule and its limits:

<details>
<summary>Show answer</summary>

<p>Adding P at the front gives PLAN. Adding E at the back gives LANE. Both appear within PLANET and PLANER. LAN is a substring of both words but is not their prefix, so the old prefix-only test rejects a viable Super Ghost fragment. NAL reverses the letter order and appears in neither word.</p>

<p>Viability answers whether some dictionary completion remains possible. It does not prove that the move avoids an earlier completed word, beats every opponent response, or is an optimal strategy. Completing a losing word must be checked separately under the actual arbiter rule.</p>

<p>A common error is checking whether a word contains each letter separately. The game requires the entire ordered fragment to remain together. Another error is treating odd/even word length as a complete strategy without considering earlier word completions and the opponent’s choices.</p>

</details>

### Follow one candidate from idea to result

Suppose the current fragment is LAN and the arbiter gives your team a turn. You consider adding P at the front. First form PLAN and look for that complete, continuous fragment in the dictionary. Then check whether the move would complete a losing word under the arbiter's actual length rule. These checks answer different questions: a possible continuation can still complete a losing word now.

If you choose that move, the interface gathers the one letter and the front placement. Its input handler validates the choice and uses the supplied submission operation. The arbiter then decides how the game state changes. The player displays the newly supplied fragment through the intended update path. It must not display a guessed accepted state simply because the user pressed a button.

The following sections connect these responsibilities to the names in the supplied project. The documentation describes those names; inspect the current skeleton to confirm their exact declarations before implementing them.

## 2. Inspect the supplied project before changing it

Read the actual skeleton and fill in this inventory. Inspect each declaration; do not guess an API from a class name.

| Part | What to identify |
|---|---|
| Skeleton initialization | Where File Manager, Dictionary, IO Manager, and Turn Parser are created. |
| IOManager | Exact read/write methods, parameters, results, and required exceptions. |
| SharedGameData | How the supplied code exposes game state and the action record. |
| GameAction and AddLocation | The supplied representation of a submitted action and its location. |
| GameState | How to read the current turn and game-over state. |
| GameManager | Exact constructor, onTurn, updateGUI, and submitTurn declarations. |
| TurnData | The supplied create operation for team, letter, and front/back choice. |

**Shared class identity** means that cooperating Java programs agree on the supplied serialized class names, packages, and compatible definitions. A class’s package is part of its full name. The project requires its serialized types in the package named sharedCode. Keep AddLocation.java, GameAction.java, GameState.java, and SharedGameData.java in the supplied package and preserve their definitions.

The source document uses both ShareGameData and SharedGameData in its prose. Use the actual supplied filename and declaration. Do not create a second class to match a spelling variation in the document.

Keep the serialized project files unchanged. A private replacement class that happens to have similar fields does not become the class the arbiter expects. Preserve the supplied serialization identifiers and project organization as well.

**Arbiter-owned state** is state your player reads while the arbiter controls its values. GameState belongs to the arbiter. Do not set the turn yourself, change game-over values, or rewrite that object to force a desired outcome. Submit a player action through the provided submission path.

### Practice: diagnose a mismatch

A player can write and read its own replacement game-data class. It then fails when reading the arbiter’s shared file. Its developer proposes changing the arbiter’s serialized classes to match the player.

What did the local round trip establish? What agreement did it fail to check? What should the developer inspect and restore?

**Project response:** Record the two programs being compared, what the local test established, and which supplied files or declarations need inspection.

<details>
<summary>Show answer</summary>

<p>The round trip established compatibility with the player’s own class in that test. It did not establish compatibility with the arbiter’s supplied classes. Inspect the full package names, actual class names, preserved class definitions, serialization identifiers, and the classes included in the player’s JAR. Restore the supplied sharedCode files and implement the required IOManager contract around them.</p>

<p>The wrong repair is to change the shared protocol to fit one player. Both packaged programs must use the supplied agreement. A successful read from a self-created fixture is useful component evidence, but an arbiter integration test is still required.</p>

</details>

## 3. Build and validate the required interface

The minimum GUI includes a text field showing the current fragment, a text field for the next letter, and controls that select front or back. Refresh the fragment at the start of each round. Clear wording should tell the user what can be done now.

Build a small interface first. Use the layout, labels, event handlers, validation, and visible feedback from Module 12. Then connect it to the supplied project methods.

- Associate visible labels with the intended text fields.
- Keep the current fragment display separate from the editable next-letter input.
- Accept exactly one letter from the permitted alphabet. Reject blank, multiple-character, digit, and punctuation input before submitting.
- Use clear labels such as Add to front and Add to back. The location must not depend on color alone.
- Enable submission only when the project permits this team to act. Prevent an accidental second submission for the same turn.
- Show useful feedback for invalid input or a failed operation. Do not leave an old success message pretending a new submission worked.
- Test pointer and keyboard use in the Workspace Desktop.

The supplied TurnData.create operation accepts the team name, one char, and a boolean. The boolean is true for front and false for back. Use the actual project declaration and pass its result to the existing submitTurn method as the skeleton directs. Keep submitTurn’s supplied implementation.

### Practice: separate candidate input from accepted state

Your form displays fragment LAN. The user enters two letters and presses Add to front. State which validation fails, whether a TurnData object should be submitted, which fragment should remain visible, and what useful message could appear.

Then describe the corresponding valid one-letter submission. Include the team name source, letter, and location value. Do not invent a team name when the constructor already supplies one.

**Project response:** Record the rejected input, unchanged displayed state, correction message, and the three values in the valid request.

<details>
<summary>Show answer</summary>

<p>The input fails the one-letter requirement. No turn should be submitted. The current fragment remains LAN until the supplied game flow provides a new state, and a message such as “Enter exactly one letter” tells the user how to correct the input.</p>

<p>For P at the front, the request uses the constructor-supplied team name, the character P, and true. The handler passes the supplied TurnData result through submitTurn. A request is not proof that the arbiter accepted the move or that the game state already changed. Refresh from the supplied game flow instead of inventing an accepted fragment locally.</p>

<p>A common error is changing the display or disabling all correction controls before validation succeeds. Another is reversing the boolean meaning: true is front, false is back.</p>

</details>

## 4. Respect the callback and thread contracts

A **callback contract** tells you when a supplied caller invokes your method, what data it supplies or expects back, and which thread performs the call.

| Supplied callback or method | Responsibility and thread rule |
|---|---|
| GameManager constructor | Use the supplied Stage, IOManager, team name, minimum length, and dictionary to initialize the player as the skeleton requires. Keep values needed by later methods in appropriate fields. |
| onTurn(fragment) | Perform selection work for the supplied fragment outside the GUI thread. Do not change live controls here. Follow the actual declaration for any return value. |
| updateGUI(fragment) | Apply short visible updates after onTurn completes successfully. This callback runs on the GUI thread. |
| submitTurn(turnData) | Use the provided implementation from a valid input handler as directed by the skeleton. |

Retrieve Module 13’s distinction between background work and application-thread UI updates. Searching a large dictionary or waiting for input/output inside updateGUI can freeze the interface. Changing a live TextField directly from onTurn breaks the UI-thread rule.

Preserve the skeleton’s coordination. Do not add a second competing watcher or a second submission loop without understanding how it interacts with the supplied one. Use its intended completion path to make selected data available to updateGUI. A method being called later in time does not by itself explain safe cross-thread visibility; inspect the supplied handoff.

If your design adds background work, define how it finishes, reports failure, and stops at game end. Keep controls usable while selection proceeds. Do not call Thread.join or a blocking result wait on the GUI thread.

### Practice: repair a frozen interface

A player’s updateGUI method performs a long dictionary search. Its buttons stop responding until the search returns. Identify the misplaced responsibility, the work that belongs in onTurn, and the small result that updateGUI should display. Explain how you will verify the repair with an actual Desktop interaction.

**Project response:** Name the background work, the short interface update, and the interaction you will try while selection is still unfinished.

<details>
<summary>Show answer</summary>

<p>The long search occupies the thread that handles the interface. Perform the selection work in the supplied background path, following the skeleton’s onTurn contract. Transfer the completed suggestion through its intended coordination mechanism. Let updateGUI display the current fragment, suggestion, and appropriate control state with short UI operations.</p>

<p>During a controlled long or waiting selection, try a harmless enabled control or keyboard action in the Desktop. It should respond before selection finishes. Then verify that the final suggestion and any failure message appear through the correct GUI callback. Merely observing that the final answer eventually appears does not establish responsiveness.</p>

<p>Do not “fix” the freeze by updating controls from the background thread. Keep the computation and the UI update on their respective paths.</p>

</details>

## 5. Test the whole player with the supplied arbiter

Use controlled data and keep a record of expected and actual behavior. Mark planned tests separately from completed ones.

| Check | Expected evidence |
|---|---|
| First window and new round | Required controls appear and the latest supplied fragment is displayed. |
| Front and back | The same letter produces the intended different request location. |
| Blank or invalid letter | Visible correction message; no turn submitted. |
| Opponent turn and repeated activation | No unauthorized or duplicate action. |
| Substring choice | The whole ordered fragment appears in at least one relevant dictionary word. |
| Completed-word boundary | Actual arbiter behavior checked below, at, and above the configured minimum. |
| Shared classes | Packaged player reads the arbiter’s actual compatible binary data. |
| Read/write failure | Failure is handled according to IOManager and the skeleton; old data is not presented as a successful new read. |
| Background selection | An enabled interface action still responds while selection is unfinished. |
| Selection failure | Useful feedback appears through the intended completion path. |
| Window close during pending work | The native window closes and any worker your design owns finishes or cooperatively stops; record actual termination separately from a visible status label. |
| Timeout | Under the documented 60-second limit, record the arbiter response to a deliberately late move in a controlled test; do not use sleeping as a synchronization strategy. |
| Missing or malformed shared data | The supplied error contract is followed, no bogus state is accepted, and no unhandled failure leaves the player appearing ready. |
| Game over | No new turn is submitted, and added background work stops as designed. |
| Clean packaged launch | JAR entry point, shared classes, and required data are available outside the development directory. |
| Head-to-head run | Two packaged players cooperate with the same arbiter protocol. |

The supplied SGhostApp.jar supports a test with one player and a competition with two players. Use the real filenames on your system. These are command templates; replace the quoted paths with your actual arbiter and packaged players.

```text
java -jar "/path/to/SGhostApp.jar" "/path/to/player.jar"
java -jar "/path/to/SGhostApp.jar" "/path/to/player_1.jar" "/path/to/player_2.jar"
java -jar "/path/to/SGhostApp.jar" -h
```

Open the Workspace Desktop to view the arbiter and player windows. The course Workspace includes the tested JavaFX runtime; do not copy obsolete module-path examples into these commands without an actual runtime requirement. These templates do not prove that your player or the instructor’s JAR has already been tested. Record the real command, game scenario, and observed result for your submission candidate.

## 6. Package and submit the runtime artifacts

Reuse Module 9’s runnable-JAR process with the actual project’s entry point and build layout. Inspect the JAR contents and confirm that the required sharedCode classes are included under the correct package path. A class that runs only from the IDE has not yet passed the packaged launch check.

Copy the JAR and required data to a clean location you control, then perform the arbiter tests from that location. Use paths that include spaces in at least one launch check. Fix any dependence on a development-only file or an unintended working directory.

Submit the runnable JAR, or a ZIP containing the JAR and additional required runtime files, through the Canvas project assignment. Do not submit source code as the deliverable or submit this project through Grader Than. The specification says that the same dictionary used by the arbiter does not need to be resubmitted. Follow the instructor’s posted competition schedule, deadline, and current grading requirements.

Before submitting, explain:

1. Which test gives the strongest evidence that your player follows the binary protocol?
2. Which real interaction demonstrates that its GUI remains responsive?
3. Which boundary test found a problem, and what changed after the repair?
4. What required data and classes are present in the actual package?

## Review your evidence

Your completed integration should connect each responsibility to an observed result: a dictionary-backed candidate, an allowed action, compatible shared data, a current fragment display, a responsive interface, and a package that launches with its required files.

In your project notes, identify one component test that passed but did not establish that the whole player worked. Explain which later integration check supplied the missing evidence. If that check is still planned, say so and name the next action.

## Supplemental Reading

- [Super Ghost project specification](https://docs.google.com/document/d/1G8VicM-wPkyrYYa20R4_cWp3P90b_1tGd23cuooOywU/edit?usp=sharing) defines the required project, callbacks, arbiter use, and submission.
- [Java 21 String API](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/String.html#contains(java.lang.CharSequence)) documents contiguous substring checks.
- [Java 21 serialization specification](https://docs.oracle.com/en/java/javase/21/docs/specs/serialization/index.html) explains Java object serialization and compatible class descriptions.
- [Java 21 JAR tool](https://docs.oracle.com/en/java/javase/21/docs/specs/man/jar.html) documents creating and inspecting Java archives.
- [JavaFX 21 Application threading](https://openjfx.io/javadoc/21/javafx.graphics/javafx/application/Application.html) explains the JavaFX Application Thread and application lifecycle.
- [JavaFX 21 Task API](https://openjfx.io/javadoc/21/javafx.graphics/javafx/concurrent/Task.html) explains background work and application-thread completion behavior used in Module 13.
