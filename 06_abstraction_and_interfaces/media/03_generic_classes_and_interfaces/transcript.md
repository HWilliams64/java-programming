# Transcript: Generic Classes and Interfaces

This CSC-239 demonstration uses Java 21 in the Workspace. It implements a generic Sequence interface with a Shelf class, then uses separate shelves of names and numeric scores.

## 0:00–0:18 — Goal

**On screen:** The title reads Generic Classes and Interfaces, with the subtitle Reuse operations with checked value types. The demonstration then opens Main.java in the Workspace.

Names and scores need the same shelf operations, but they use different value types. Generics allow us to write those operations once while the compiler checks each chosen type.

## 0:18–1:10 — Use a type parameter consistently

**On screen:** Main.java is typed in the editor. The completed 38-line source is visible. The selection highlights Sequence and Shelf, including the type parameter, method declarations, private list, constructor and method bodies. Captions sit below the code. Gray value: and index: labels beside arguments are editor hints; they are not Java source text.

```java
import java.util.ArrayList;
interface Sequence<T> {
    void add(T value);
    T get(int index);
    int size();
}
class Shelf<T> implements Sequence<T> {
    private ArrayList<T> values;
    public Shelf() {
        values = new ArrayList<T>();
    }
    @Override
    public void add(T value) {
        values.add(value);
    }
    @Override
    public T get(int index) {
        return values.get(index);
    }
    @Override
    public int size() {
        return values.size();
    }
}
public class Main {
    public static void main(String[] args) {
        Sequence<String> names = new Shelf<String>();
        names.add("Maya");
        names.add("Luis");
        System.out.println("First: " + names.get(0));
        System.out.println("Names: " + names.size());
        Sequence<Integer> scores = new Shelf<Integer>();
        scores.add(4);
        scores.add(7);
        int total = scores.get(0) + scores.get(1);
        System.out.println("Total: " + total);
    }
}
```

T is a type parameter: a placeholder for a type, not a stored value. Sequence uses it for additions and retrievals. Shelf carries that same placeholder into its private ArrayList and implements each operation by calling the list.

## 1:10–1:28 — Predict the three output lines

**On screen:** The selection moves to both shelf declarations, additions, retrievals and print calls. All 38 source lines remain visible, including the String and Integer type arguments. The terminal has not opened, and no computed output appears. A three-second pause follows the prediction request with the complete caller still selected.

The names reference chooses String, while scores chooses Integer. Each shelf has its own list. The score retrievals provide Integer values, which Java unboxes for arithmetic. Predict the first name, name count, and total, then pause.

## 1:28–1:48 — Execute and compare

**On screen:** The terminal opens beneath the source, and the view enlarges the result. The command and all three output lines are clear. Top captions overlap parts of the earlier interface ending, Shelf declaration and private field. The constructor and method bodies remain visible. The score declarations and calculation are below the smaller editor pane; they were fully visible during prediction. The narration describes an incompatible addition as a hypothetical compiler rejection; no incorrect program is run. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
First: Maya
Names: 2
Total: 11
```

Index zero returns Maya, and the names shelf contains two entries. The score entries are four and seven, so their sum is eleven. The same methods work with either chosen type. The compiler would reject adding a number through names because that reference requires strings.

## 1:48–2:02 — Change a score

**On screen:** The view returns to the full Workspace with the original output still visible. The generic definitions and name operations remain on screen. The score operations are below the editor pane. A bottom caption asks the learner to predict the result of changing the second score to zero. No code is changed and no answer to that prompt is shown. The final image holds for two seconds after the narration.

Change the second score to zero. Predict all three output lines. Explain why the names output stays the same, and identify the type argument that controls the score values.

