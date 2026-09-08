# Transcript: Catching and Tracing Exceptions

This CSC-239 demonstration uses Java 21 in the Workspace. It handles an integer division failure inside a loop and traces which statements run next.

## 0:00–0:18 — Goal

**On screen:** The title reads Catching and Tracing Exceptions, with the subtitle Handle one failure and continue the loop. The demonstration then opens Main.java in the Workspace.

A packing calculator can keep working after one input fails. An exception object describes a failure. We will use one to choose a response and trace where execution continues.

## 0:18–0:57 — Handle a failure inside the loop

**On screen:** Main.java is typed in the editor. The completed 23-line source is visible. The selection highlights the loop and the blocks that choose a response to a failed calculation. Small gray labels such as total:, groups: and x: are names shown by the editor beside arguments; they are not part of the Java source. Captions sit below the code. The loop calls share directly. The quote method is present but is not called in this demonstration.

```java
class RatioTools {
    public static int share(int total, int groups) {
        return total / groups;
    }
    public static int quote() {
        return share(12, 0);
    }
}
public class Main {
    public static void main(String[] args) {
        int[] groupCounts = {3, 0, 4};
        for (int groups : groupCounts) {
            try {
                System.out.println("Share: " + RatioTools.share(12, groups));
                System.out.println("Calculated");
            } catch (ArithmeticException problem) {
                System.out.println("Cannot divide by zero.");
            }
            System.out.println("Next input");
        }
        System.out.println("Done");
    }
}
```

A try block groups operations whose failures may be handled. A catch block receives a matching exception object and runs a response. ArithmeticException is the type for arithmetic failures such as integer division by zero. This loop calls share directly.

## 0:57–1:14 — Predict the complete output

**On screen:** The selection includes the groupCounts array, loop, try and catch blocks, and the messages after them. All 23 source lines remain visible. The terminal has not opened, and no computed output appears. A three-second pause follows the request to predict every line and identify skipped messages.

The try and catch are inside the loop. There is also a message after them and another after the loop. Predict every output line for the three group counts, including which messages are skipped. Pause before running.

## 1:14–1:41 — Execute and compare

**On screen:** The terminal opens beneath the source, and the view enlarges the result. The command and all nine output lines are clear. The complete loop, catch block and messages after them remain visible. The enlarged view crops the top class and method declaration; a top caption overlaps part of the unused quote method. The division inside share stays visible. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
Share: 4
Calculated
Next input
Cannot divide by zero.
Next input
Share: 3
Calculated
Next input
Done
```

Valid counts produce shares of four and three. The division failure leaves share without a result. This is abrupt completion: the operation ends before its remaining work finishes. Java leaves unfinished method calls as it searches outward for a matching catch. This is stack unwinding. The Share print and Calculated are skipped for zero. After the catch block, Next input runs, then the loop continues.

## 1:41–1:51 — Change the first group count

**On screen:** The view returns to the full Workspace. All 23 source lines and the original nine output lines remain visible. A bottom caption asks for a new prediction after changing the first group count to zero. No code is changed and no answer to that prompt is shown. The final image holds for two seconds after the narration.

Change the first group count to zero. Predict the complete output. Explain why the final group is still processed.

