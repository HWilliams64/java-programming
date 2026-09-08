# Switch and Branch Choices

## Narration

Welcome to this Java tutorial, where you'll use a switch statement to match fixed choices, control each case with break, and explain the default fallback and fall-through, when execution continues into a later case.

Organizing fixed choices and their exits helps applications handle menu commands consistently, provide useful responses to unknown input, and avoid performing an unintended second action.

A library kiosk needs to show a visitor one service instruction for a supplied text command. We'll first build a small information menu with hours and status commands. Then we'll apply the same matching rule to borrowing and renewing. These examples display instructions; they don't access a real library account.

A supported command should select its own instruction, while other text should receive a reminder of the available choices. We'll also print a readiness message after our first switch, so you can see where execution continues. Later, you'll predict the completed borrowing and renewing example before we run it.

Let's open Main.java in the Workspace and start the information menu.

Main is the class containing this program's code, and its main method is where the program starts. We'll put our statements inside that method. The command variable will store hours. A switch matches that one supplied value against fixed choices; for ranges or combinations of facts, the earlier if statement is a better fit.

Command is the selector, the value being matched. We need an entry point for the hours request. The case keyword introduces its fixed text label, and the colon marks where that choice's statements begin. We'll display the opening time, then use break to leave the switch.

That break prevents the hours request from continuing into another service instruction. We'll add a status choice for the service desk and a default fallback for unmatched text. Default has no value to match. It identifies the starting point to use when none of the named cases matches.

Our default group is last, so reaching its end reaches the switch's closing brace. The final readiness print is outside the switch but inside main. With hours, Java should enter the first case, display the opening time, and break to that readiness print. Let's run the complete program to check the path.

We see the opening-time instruction followed by Menu ready. Break ended the switch, not the program. The status and default instructions did not run. Notice the braces around the switch body: case labels mark entry points, but they don't create separate blocks or local scopes.

The supported path works. We also need evidence for input outside the list. We'll change only the command to events, leaving every case and exit unchanged.

Events matches neither hours nor status. Java should start at default, print the available choices, and then continue to Menu ready. Let's run this unmatched case.

The fallback reminder prints, followed by the readiness message. The fallback is selected because no named case matches. String matching uses text contents and respects letter case and spaces. A label is an exact choice, not a test for whether one word appears somewhere inside a longer command.

Matching the right entry point is only half the job. We'll restore hours, then deliberately remove its break. The program will still compile, but it will violate our rule of one service instruction per command. Let's make those two small edits so we can see why.

Execution will enter the hours case and print its instruction. Without that break, it keeps going into the statements under status, without testing the status label again. This is fall-through. The break after the status message will finally leave the switch. Let's run the faulty version and inspect every output line.

Two service instructions appear before Menu ready. The selector never changed to status; execution simply continued past its label. The program ran successfully, but the result is wrong for our requirement. Testing only status would have missed this earlier missing break, so test each supported entry point.

We'll repair the hours action by restoring its print statement together with the missing break. The statement after the switch will stay in place, so the corrected run can still show where control continues.

Hours now prints its instruction and exits before the status label. Let's rerun that same input to check that the extra service instruction is gone.

The repaired version prints only the hours instruction and Menu ready. We changed the exit, not the selected command or its message. That comparison identifies the cause of the extra line. Fall-through can be deliberate in other programs, but it doesn't suit this menu's one-instruction rule.

We'll now replace the information menu with the lesson's borrowing and renewing program. It uses the same structure and matching rule, with a different set of commands and messages. This final version has no separate readiness print. Read the choices as we build it, then predict which one runs.

The supplied command is renew. We'll add the two supported case labels and their exits, followed by the fallback. Each print belongs to the label immediately above it. Use the worked information menu to trace where execution begins and where it stops.

Before we run, write the exact output you expect and name the label where execution begins. Explain whether either of the other messages will print. Pause the video here if you need more time.

Let's click Run and compare the actual instruction with your prediction.

The program prints Open your loan list. Renew matches the second case, so the earlier borrow statements are skipped. After the selected print, break leaves the switch before default. There is no later print in main, so this run produces exactly one instruction.

We've built a fixed-command choice, checked an unmatched command, and repaired an unwanted second instruction. A switch chooses an entry point, case labels name the supported values, default handles an unmatched value, and break controls the exit. Together, those parts give this kiosk a predictable response.

Now use the notebook to build its related library selector. Test every supported command, an unknown command, and the stated change in letter case. Compare both the message and the number of lines. Explain why these fixed choices suit a switch, and why a range-based rule would call for an if condition instead.

## Visual description

[Four code-free BHCC opening scenes show three learning goals, the benefits of a fixed-choice menu, a library visitor choosing hours or status information, and an annotated two-part response. This information menu does not perform account transactions.]

[Main.java is opened and built in small groups while the camera follows the actual typing. The first String command is hours. Matching case labels select the first printed instruction; break leaves the switch, and the statement after the switch prints Menu ready. A visible mouse click on the editor toolbar Run Code action produces The library opens at nine. followed by Menu ready.]

[Only the command declaration changes to events. Another actual Run click shows the default instruction Choose hours or status. followed by Menu ready. The spoken explanation identifies exact String matching and explains that spelling, spaces, and capitalization matter.]

[The command returns to hours, and the first break is deliberately deleted. A third actual Run prints The library opens at nine., The service desk is open., then Menu ready. The trace explains fall-through into the next case body. The missing break is restored, and a fourth Run returns to the original two-line output. Case labels do not make separate local blocks; braces define the switch block.]

[The worked menu is replaced with the complete canonical borrowing and renewal program below. Its command is renew. Students predict the instruction before the fifth actual Run, which prints Open your loan list. The closing connects matching, break, default, and testing several command choices with the notebook practice.]


## Canonical program

```java
public class Main {
    public static void main(String[] args) {
        String command = "renew";
        switch (command) {
            case "borrow":
                System.out.println("Visit the checkout desk.");
                break;
            case "renew":
                System.out.println("Open your loan list.");
                break;
            default:
                System.out.println("Choose borrow or renew.");
        }
    }
}
```

## Exact canonical output

```text
Open your loan list.
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Concept icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Sources, licenses and hashes are retained in production evidence.
