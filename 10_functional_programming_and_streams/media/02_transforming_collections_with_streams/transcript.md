# Transcript: Transforming Collections with Streams

This CSC-239 demonstration uses Java 21 in the Workspace. A registration list supplies text to clean and select by length. The recording shows the complete Main.java program and its actual output.

Gray labels beside some method arguments show parameter names. They are editor hints, not extra source. The editor may draw the two characters in an arrow or comparison operator as one joined shape. The source below preserves the exact Java characters.

## 0:00–0:17 — Goal

**On screen:** The title reads “Transforming Collections with Streams,” followed by an empty Main.java editor as the goal is introduced. The output has not been shown.

A registration list contains names with extra spaces, a short name, and empty text. We will clean the text before choosing names by length.

## 0:17–0:58 — Clean and select values

**On screen:** The complete 20-line program is entered and displayed. A selection draws attention to the source list and the map and filter calls. The caption sits below the source.

The complete source is:

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<String>();
        names.add("  Maya  ");
        names.add("Li");
        names.add(" Luis ");
        names.add("");
        List<String> selected = names.stream()
            .map(String::trim)
            .filter(name -> name.length() >= 4)
            .toList();
        for (String name : selected) {
            System.out.println(name);
        }
        System.out.println("Selected: " + selected.size());
    }
}
```

A stream pipeline describes a source and a sequence of operations on its elements. Our source is names. Map and filter are intermediate operations. Each produces another stream stage. Mapping applies a function to each processed element. Here, trim supplies cleaned text. Filter uses a lambda returning true or false to decide which cleaned values continue. These operations leave the source list unchanged.

## 0:59–1:25 — Produce an ordered result

**On screen:** The complete program remains visible. The selection moves to the toList call, the loop over selected, and the printed count. The caption remains below the source.

A terminal operation starts processing and produces the final result. Here, toList collects results into a List, the interface type of the returned collection. The result is unmodifiable, meaning its entries cannot be added, removed, or replaced. Encounter order is the order supplied by a source. This pipeline preserves our list's order. A HashSet source would not gain a promised order just by using a stream.

## 1:25–1:37 — Predict the result

**On screen:** The selection is cleared and all 20 lines are visible. The terminal is closed, so the answer has not appeared. A three-second pause follows the prediction prompt.

Predict every output line, including the count. Apply trimming before the length test, then trace the loop over selected. Pause here.

## 1:37–1:55 — Run and interpret the result

**On screen:** The terminal opens and shows the command and three output lines clearly. This closer view crops the import lines at the top. Top captions briefly overlap the main header, list creation, and first add call. The map, filter, and toList calls, the loop, and the printed output remain readable; earlier views show the complete source. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Maya
Luis
Selected: 2
```

Maya and Luis each have four characters after trimming, so they remain. Li has two and empty text has zero, so they are excluded. The loop prints Maya before Luis, followed by Selected: two. Filter keeps every matching entry, including repeats.

## 1:55–2:09 — Try a repeated input

**On screen:** The wide view restores all 20 source lines, with the source list and operation calls selected. The original output remains visible while the learner is asked to add a repeated name. That change is not performed in the recording.

Add another Maya with surrounding spaces at the end of the source list. Predict every output line and the new count, then run again. Where should the repeated name appear, and why?

