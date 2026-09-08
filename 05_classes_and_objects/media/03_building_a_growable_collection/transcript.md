# Transcript: Building a Growable Collection

This CSC-239 demonstration uses Java 21 in the Workspace. It separates logical size from array capacity and grows a signup collection by copying its existing names in order.

## 0:00–0:20 — Goal

**On screen:** The title reads Building a Growable Collection, with the subtitle Preserve names while storage grows. Main.java then opens in the Workspace before code is typed. The title and opening narration introduce the goal and vocabulary without revealing the fixture results.

A signup list must grow without losing its order. Its backing storage is an internal array. Logical size counts added names. Capacity counts array positions, including unused ones.

## 0:20–1:10 — Grow storage while preserving names

**On screen:** The Workspace shows Main.java being typed, beginning with the storage and size fields and the constructor. The completed view contains all 42 source lines. Lines 2 through 18 are selected while the narration explains allocation, copying used entries, replacing the storage reference, and adding the new name. The full growth condition and loop are readable. The bottom captions are below the source. Gray name: labels beside arguments are editor hints, not text to type. The editor joins the two equals signs in the equality test visually; the exact Java source below preserves ==. The visible status counters show zero errors and zero warnings.

```java
class GrowingNames {
    private String[] storage;
    private int size;
    public GrowingNames() {
        storage = new String[2];
        size = 0;
    }
    public void add(String name) {
        if (size == storage.length) {
            String[] larger = new String[storage.length * 2];
            for (int index = 0; index < size; index = index + 1) {
                larger[index] = storage[index];
            }
            storage = larger;
        }
        storage[size] = name;
        size = size + 1;
    }
    public String get(int index) {
        return storage[index];
    }
    public int size() {
        return size;
    }
    public int capacity() {
        return storage.length;
    }
}
public class Main {
    public static void main(String[] args) {
        GrowingNames names = new GrowingNames();
        System.out.println("Start: " + names.size() + "/" + names.capacity());
        names.add("Maya");
        names.add("Luis");
        System.out.println("Full: " + names.size() + "/" + names.capacity());
        names.add("Nora");
        System.out.println("Grown: " + names.size() + "/" + names.capacity());
        for (int index = 0; index < names.size(); index = index + 1) {
            System.out.println(names.get(index));
        }
    }
}
```

When storage is full, add allocates an array twice as long. It copies only the used names in order, then replaces the storage reference. Each array keeps its own fixed length. Finally, it stores the new name and increases size.

## 1:10–1:26 — Predict size, capacity, and order

**On screen:** Lines 31 through 39 are selected: construct the collection, print the Start report, add Maya and Luis, print Full, add Nora, print Grown, then traverse the logical elements. All 42 lines remain visible, including the earlier growth code and getters. Captions remain below the source. No terminal result appears before the prediction. The three-second pause keeps the same code visible and clears the caption.

Unused String positions start as null. The final loop reads only indexes below size, as get requires. Predict the three size and capacity reports and the order of names, then pause.

## 1:26–1:42 — Execute and compare

**On screen:** The terminal opens and the camera emphasizes it. All six output lines and the successful return to the prompt are clear. The upper editor shows the growth algorithm and getters; caller statements below line 31 are below the shortened editor pane. Top captions overlap parts of the constructor and add method heading, but leave the growth condition, copying loop, size update and terminal output unobscured. The entire source was unobscured during modeling and prediction. There are no visible error squiggles or reported compilation errors. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
Start: 0/2
Full: 2/2
Grown: 3/4
Maya
Luis
Nora
```

The empty collection reports zero out of two. Two additions fill it. The third doubles capacity to four while size becomes three. Copying preserves Maya, Luis, Nora. The unused position is never printed.

## 1:42–1:56 — Add one more name

**On screen:** The camera returns to the full Workspace view with the terminal still open. The complete growth condition and method body remain visible above the same six output lines. Caller statements below line 31 are below the shortened editor pane; they were shown in full during the prediction and are reproduced in this transcript. The bottom caption leaves the source and terminal output clear while the learner considers a fourth name. GrowingNames.class and Main.class now appear in the file explorer. The ending holds the same view after the caption clears. Visible status counters show zero errors and zero warnings.

Add a fourth name before the Grown report. Predict its size, capacity, and printed order. Would this addition copy the array again? Explain using the growth condition.

