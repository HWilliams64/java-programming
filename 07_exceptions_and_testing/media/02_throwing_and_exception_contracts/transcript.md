# Transcript: Throwing and Exception Contracts

This CSC-239 demonstration uses Java 21 in the Workspace. It reports invalid quantities and preserves an earlier failure when one exists.

## 0:00–0:21 — Goal

**On screen:** The title reads Throwing and Exception Contracts, with the subtitle Explain a failure and preserve its cause. The demonstration opens Main.java in the Workspace.

A quantity form needs to explain different failures. A custom exception class names a failure for our application. InvalidQuantityException is checked: Java requires callers to catch it or declare that it may leave their method.

## 0:21–1:30 — Explain the parser and its exception

**On screen:** Main.java is typed into the editor. The complete 32-line source is then visible, with the exception class and quantity parser selected. Bottom captions leave all source lines clear. Gray words before some supplied values are editor hints and are not part of the saved Java source. The editor draws the two characters in != together as a not-equal symbol. The source below contains the exact characters to type.

```java
class InvalidQuantityException extends Exception {
    public InvalidQuantityException(String message, Throwable cause) {
        super(message, cause);
    }
}
class QuantityParser {
    public static int read(String text) throws InvalidQuantityException {
        int quantity;
        try {
            quantity = Integer.parseInt(text);
        } catch (NumberFormatException cause) {
            throw new InvalidQuantityException("Quantity must be a whole number.", cause);
        }
        if (quantity < 0) {
            throw new InvalidQuantityException("Quantity cannot be negative.", null);
        }
        return quantity;
    }
}
public class Main {
    public static void main(String[] args) {
        String[] inputs = {"3", "two", "-1"};
        for (String input : inputs) {
            try {
                System.out.println("Quantity: " + QuantityParser.read(input));
            } catch (InvalidQuantityException problem) {
                System.out.println("Problem: " + problem.getMessage());
                System.out.println("Has cause: " + (problem.getCause() != null));
            }
        }
    }
}
```

The throws declaration names a possible failure. A throw statement raises an exception object now. Integer dot parseInt converts decimal digits with an optional leading plus or minus. It rejects whitespace, invalid text, and values outside the int range with NumberFormatException. That type is unchecked, so callers need not catch or declare it. Our new exception keeps a message and an optional cause: an earlier failure that explains this one. Throwable is the parent type used here to receive that earlier exception object. Passing the cause to super preserves it for the caller.

## 1:31–1:48 — Predict the complete output

**On screen:** The input array and the caller inside the loop are selected. The complete source remains readable, and no terminal result has appeared. The prediction caption ends before a three-second pause with the source still on screen.

The caller catches our checked exception separately for each input. It prints either the quantity or the problem message and whether a cause exists. Trace the three inputs and predict every output line. Pause before running.

## 1:48–2:13 — Execute and compare

**On screen:** The terminal opens below the editor, and the view moves closer to the running example. All five output lines are readable. During this closer view, the exception class heading is above the frame and top captions partly cover the read method declaration. Its conversion and validation body, the caller, and the terminal output remain clear. The complete source was visible during modeling and prediction. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
Quantity: 3
Problem: Quantity must be a whole number.
Has cause: true
Problem: Quantity cannot be negative.
Has cause: false
```

Three becomes a valid quantity. The word two fails conversion, so the new exception retains the original NumberFormatException. Has cause is true. Negative one converts successfully, then fails our nonnegative rule. There is no earlier exception, so its cause is null and Has cause is false. The catch block reports each failure and the loop continues.

## 2:13–2:24 — Try zero as the final quantity

**On screen:** The view widens to show the exception class, parser, caller, and unchanged five-line result. Source lines 1 through 31 are visible; the final class closing brace is below the terminal divider. The bottom caption asks you to change the final input and predict what follows. No code is changed and no transfer answer is shown. A two-second hold follows the final prompt.

Change the final input from negative one to zero. Predict the complete output and explain how the final call differs from the original.

