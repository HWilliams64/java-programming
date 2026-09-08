# Transcript: Serializing and Restoring Objects

This CSC-239 demonstration uses Java 21 in the Workspace. A temporary file holds a saved ScoreCard. The program restores it, checks its type and compares saved fields with temporary state. The recording shows the complete Main.java program and its actual output.

Gray labels beside some method arguments show parameter names. They are editor hints, not extra source. The source below preserves the exact Java characters.

## 0:00–0:18 — Goal

**On screen:** A title card names Serializing and Restoring Objects, with the subtitle Save object state and check the restored type. The Workspace then shows an empty Main.java editor while the goal is introduced. The program is typed visibly afterward.

We will save a score card, restore it from our own temporary file, and compare its saved values with temporary state. Watch how the program checks the restored object before using its methods.

## 0:18–1:48 — Choose saved and temporary state

**On screen:** The program is typed, then all 43 lines of Main.java are visible together. Lines 6 through 18 are selected to connect the explanation with ScoreCard, serialVersionUID, owner, points, views, the constructor and the getter methods. Bottom captions sit below the source.

The complete source is:

```java
import java.io.ObjectInputStream;
import java.io.ObjectOutputStream;
import java.io.Serializable;
import java.nio.file.Files;
import java.nio.file.Path;
class ScoreCard implements Serializable {
    private static final long serialVersionUID = 1L;
    private String owner;
    private int points;
    private transient int views;
    public ScoreCard(String owner, int points) {
        this.owner = owner;
        this.points = points;
        this.views = 1;
    }
    public String getOwner() { return owner; }
    public int getPoints() { return points; }
    public int getViews() { return views; }
}
public class Main {
    public static void main(String[] args) throws Exception {
        Path file = Files.createTempFile("score-card-", ".bin");
        try {
            ScoreCard original = new ScoreCard("Maya", 7);
            try (ObjectOutputStream writer = new ObjectOutputStream(Files.newOutputStream(file))) {
                writer.writeObject(original);
            }
            try (ObjectInputStream reader = new ObjectInputStream(Files.newInputStream(file))) {
                Object value = reader.readObject();
                if (value instanceof ScoreCard) {
                    ScoreCard restored = (ScoreCard) value;
                    System.out.println(restored.getOwner() + ": " + restored.getPoints());
                    System.out.println("Original views: " + original.getViews());
                    System.out.println("Restored views: " + restored.getViews());
                } else {
                    System.out.println("Unexpected object type.");
                }
            }
        } finally {
            Files.deleteIfExists(file);
        }
    }
}
```

Object serialization writes an object state representation into a byte stream. Serializable is a marker interface: it marks this support without requiring methods. Objects held in saved reference fields must support it too. The serialization version identifier helps check whether saved data and the current class can work together. Its long type stores whole numbers, and the L marks the written number as long. Matching identifiers alone do not make every class change compatible. Static fields belong to the class and are not saved as instance state. A transient instance field is excluded from default serialization. Here, views marks temporary state.

## 1:48–2:20 — Restore and check the object

**On screen:** The complete source stays visible. Lines 22 through 40 are selected: the temporary file, original card, writeObject and readObject calls, the check of the restored value’s type, the line that gives its reference the ScoreCard type, printed values, other-type branch and finally cleanup. Bottom captions remain below the source.

Object deserialization reconstructs an object from a compatible saved representation. The output stream writes our card, and the input stream reads it back. The readObject method returns Object, the common reference type. The runtime type check, instanceof, tests whether the actual non-null value is a ScoreCard. The reference cast then gives that reference the more specific ScoreCard type so we can call its methods. Other types take the else branch. Try with resources closes both streams, and finally deletes the file.

## 2:20–2:35 — Predict the result

**On screen:** The selection clears so the entire program can be examined. The terminal is still closed and no result has been revealed. The video holds for three seconds after the prediction prompt.

Predict all three printed lines. Which fields are saved, and what do you expect for views on the restored card? Decide whether restoring should repeat the constructor. Pause here.

## 2:35–2:57 — Run and interpret the result

**On screen:** The terminal opens and the view enlarges the actual command and all three result lines. The first import and part of the second are cropped at the top; source after line 31 falls below the editor divider. Top captions briefly cover parts of the remaining imports, class declaration, version identifier and owner declaration. The transient views field, constructor, object stream operations, type check and cast remain readable. The full source, including print statements and cleanup, was shown in the teaching and prediction views. Near the end of the result explanation, the ScoreCard definition is selected again. The terminal output remains clear throughout these result views. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Maya: 7
Original views: 1
Restored views: 0
```

Maya and seven are restored. Original views is one, but restored views is zero. Default deserialization of this ordinary Serializable class does not replay its constructor or field initializers. The transient int keeps its default zero value. Our type check succeeds, so the cast and getter calls proceed.

## 2:58–3:11 — Change and compare temporary state

**On screen:** The view returns to the full Workspace width with the terminal open. Lines 6 through 18 remain selected, making the transient field and constructor value easy to locate beside the unchanged result. The source below line 31 is outside the editor view. Bottom captions sit below the terminal output. The requested changes are learner prompts; the recording keeps the original source and result, then holds for two seconds.

Set the constructor’s views value to five and predict both view lines. Then remove transient and predict again. Explain which state belongs in a saved score card.

