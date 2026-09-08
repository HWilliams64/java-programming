# Transcript: Cleanup and Resources

This CSC-239 demonstration uses Java 21 in the Workspace. It uses printed messages to trace when objects are initialized and closed.

## 0:00–0:21 — Goal

**On screen:** The title reads Cleanup and Resources, with the subtitle Trace when cleanup happens. The Workspace then shows an empty Main.java editor while the opening explanation and its captions introduce the model.

A resource is something a program gets, uses, and releases. Its lifetime is the time between getting it and releasing it. NamedResource models that lifetime with printed messages. These objects only print messages.

## 0:21–1:04 — Follow automatic cleanup

**On screen:** Main.java is entered visibly. Near 0:36–0:38, the editor cursor moves to the closing brace on line 17, selects five excess leading spaces, and deletes them to align the brace with try. The code below is the complete corrected source. All 20 lines are visible during the explanation; the selection emphasizes the resource class and try block. Small gray name: and x: labels are editor hints for parameter names. They are not text to enter.

```java
class NamedResource implements AutoCloseable {
    private String name;
    public NamedResource(String name) {
        this.name = name;
        System.out.println("Opened: " + name);
    }
    @Override
    public void close() {
        System.out.println("Closed: " + name);
    }
}
public class Main {
    public static void main(String[] args) {
        try (NamedResource first = new NamedResource("first");
             NamedResource second = new NamedResource("second")) {
            System.out.println("Work");
        }
        System.out.println("Done");
    }
}
```

AutoCloseable is an interface that requires a close method. Try-with-resources declares objects inside parentheses after try. Java calls close on the successfully initialized resources when control leaves the block, including when an exception leaves it. The last object initialized is the first closed. This is reverse resource closure. If the running Java program is forcibly stopped, cleanup may not run.

## 1:04–1:20 — Predict the complete output

**On screen:** The two resource declarations, the Work statement, the closing brace and the later Done statement are selected. All 20 source lines remain visible. Captions sit below the code, then disappear for the three-second prediction pause.

Predict the complete output, including the order of construction, work, closing, and the final statement. Use the order of declarations and the reverse closing rule. Pause before running.

## 1:20–1:39 — Execute and compare

**On screen:** The view moves closer to the terminal, where all six result lines are readable. The upper edge crops the resource class heading and part of its field declaration. The first result caption covers part of the earlier constructor print statement and close method heading. The close method body, both resource declarations, Work, Done and the full output remain visible. The full source is shown in the preceding explanation and prediction views. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
Opened: first
Opened: second
Work
Closed: second
Closed: first
Done
```

The constructors print first, then second. The body prints Work. Java then closes second before first. Done appears after both close calls finish. The try statement supplies those calls automatically. Our printed messages show exactly when each step occurs.

## 1:39–1:51 — Swap the resource declarations

**On screen:** The full Workspace view returns, showing all 20 source lines and the six output lines together. The final caption asks you to swap the declarations while keeping each name with its object. The view holds after the prompt so you can consider your prediction.

Swap the two resource declarations, keeping each name with its object. Predict the new output and explain which rule controls the closing order.

