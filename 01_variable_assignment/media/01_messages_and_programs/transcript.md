# Transcript: Messages and Java Programs

Voice: Sky (Kokoro). The visual descriptions include the actions following each spoken passage.

## 00:00.650–00:12.742

**Visual description:** After a brief silent opening, a Java learning board introduces console output as displayed text, statements as individual instructions, and string literals as text in double quotation marks. These terms form a vertical board beside the learning goal; no source code or Workspace appears.

Welcome to your first Java lesson, where you'll produce console output, the text a program displays, using statements, or instructions, and string literals, or text in quotation marks.

## 00:13.394–00:26.770

**Visual description:** Console output connects to three software-use panels: displaying results, debugging by finding and fixing problems, and text interfaces. The horizontal panels develop a different arrangement from the first scene.

Console output lets applications display results, helps you find and fix problems by showing what a program is doing, and supports command-line interfaces, where people work with software through text.

## 00:27.624–00:36.150

**Visual description:** A campus help-desk scene places arriving students beside a single notice. Labels explain that we supply the wording and visitors read without typing.

We'll make a short notice for students arriving at a campus help desk. We'll supply the wording; visitors won't need to type anything.

## 00:36.895–00:43.046

**Visual description:** The retained A notice people can use layout reveals a greeting and a preparation reminder on one notice, alongside the goals Readable words and A clear next step. The exact target messages have not been shown as output.

The notice should greet each student and explain how to prepare, so they know what to do next.

## 00:43.091–00:47.043

**Visual description:** The Workspace appears after the four opening scenes. The Main.java view is opened by selecting its existing tab.

Now that we're in the Workspace, let's open Main.java.

## 00:50.760–01:06.561

**Visual description:** The starter structure is explained before its two opening lines are typed. Main names the class; main names the method where this program starts. The camera is directed toward the active code.

Main.java is open. This supplied frame is our program's starter structure. Main is the class that holds our code. Its main method is a named group of instructions where this program starts. We'll put our message statements inside it.

## 01:12.297–01:25.874

**Visual description:** The first worked statement is typed inside the supplied structure: System.out.println("Welcome.");. The statement is highlighted after typing for the following explanation.

Those opening lines give our statements a place to run. Let's add one instruction, called a statement, to display a short welcome. Java's print-line instruction sends our string to the console and ends the line.

## 01:29.500–01:44.302

**Visual description:** The first worked statement stays visible while its string literal and punctuation are explained. A second statement, System.out.println("Please take a number.");, is then typed on its own line.

Text written between quotation marks is a string literal. The marks show its boundaries; they aren't part of the message. Parentheses hold the text, and the semicolon ends the statement. Let's add a separate instruction for taking a number.

## 01:48.573–01:55.475

**Visual description:** Two closing braces finish the supplied structure around the two worked-example statements.

We have two message statements. Let's finish the supplied frame so the whole program is ready to run.

## 01:57.481–02:11.558

**Visual description:** The completed worked program is ready. The real inline Run control is activated, and the program displays its two lines in the terminal.

The completed frame contains both instructions. Let's click Run to compile and run the program. Compilation checks Java's rules; execution carries out our instructions. Watch how the source becomes a notice.

## 02:16.734–02:32.410

**Visual description:** The console displays Welcome. followed by Please take a number. on the next line. These different messages establish the pattern before the target prediction.

The console shows Welcome, then Please take a number, on separate lines. Execution followed the statement order. It printed the strings' text, without quotation marks or Java instructions. That gives us a pattern for the help desk notice.

## 02:32.758–02:43.334

**Visual description:** Only the two worked-example statements are removed and replaced with the help-desk statements. The existing Main/main structure is retained while the camera follows the active typing.

Let's replace only the two practice statements with the help desk's supplied messages. We'll keep the working Main frame and use a separate statement for each message.

## 02:54.867–03:10.394

**Visual description:** Both target statements remain visible while the learner predicts the exact output. The authored eight-second pause follows; the target output is not revealed until the next run.

The source now contains the help desk messages. Before we run it, write the exact two output lines in order. Will the quotation marks or the Java instruction itself appear? Use what the practice run showed you. Pause here if you'd like more time.

## 03:18.429–03:21.655

**Visual description:** The actual inline Run control is activated a second time to test the prediction.

Let's click Run to check your prediction.

## 03:25.836–03:42.012

**Visual description:** The console displays Welcome to the help desk. and then Please have your student ID ready. on separate lines, each with a final period.

The console says Welcome to the help desk, then Please have your student ID ready. Both messages end with a period. They appear on separate lines, in statement order, with no source-code punctuation added. Compare that with the two lines you wrote.

## 03:42.080–04:00.656

**Visual description:** The view widens to the completed source and console output. The closing captions are assigned to blank space between them while the original notice goal and programming concepts are connected.

We've built the notice the help desk needed: a greeting followed by a preparation reminder. Strings preserved the wording, print-line statements separated the messages, and statement order made the notice easy to follow. Compiling and running let us check the actual result, not just the source.

## 04:01.322–04:14.773

**Visual description:** The completed program remains visible for the transfer question. A version with swapped statements is not executed; the learner explains the possible change.

Before returning to the notebook, imagine swapping the two message statements. What would change in the console, what would stay the same, and why? Explain it using the difference between source code and printed text.

## Worked program

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Welcome.");
        System.out.println("Please take a number.");
    }
}
```

Its console output:

```text
Welcome.
Please take a number.
```

## Completed help-desk program

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Welcome to the help desk.");
        System.out.println("Please have your student ID ready.");
    }
}
```

The demonstrated action is the Workspace’s inline **Run** control. Both recorded executions completed successfully. The launch is performed by that control; no shell command is inferred. Final console output:

```text
Welcome to the help desk.
Please have your student ID ready.
```

## Editor annotations

Gray `x:` labels, when visible, are editor parameter hints rather than characters in the Java source. Diagnostic messages can appear while a statement or its surrounding structure is incomplete. The complete worked and help-desk programs each run successfully.

## Icon credits

Java icon: [Material Icon Theme contributors](https://github.com/material-extensions/vscode-material-icon-theme/blob/db37396672f801195be1bf082cca76942deb8c24/icons/java.svg), [MIT license](https://github.com/material-extensions/vscode-material-icon-theme/blob/db37396672f801195be1bf082cca76942deb8c24/LICENSE). Generic icons: [Font Awesome Free 6.7.2](https://github.com/FortAwesome/Font-Awesome/tree/6.7.2/svgs/solid) by Fonticons, Inc., [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/), with the BHCC palette applied where appropriate. No endorsement is implied.
