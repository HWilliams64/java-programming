# Transcript: Stream Lifecycle and Result Lists

This CSC-239 demonstration uses Java 21 in the Workspace. A source list supplies items for a report. The program collects that report and makes a separate list for edits. The recording shows the complete Main.java program and its actual output.

Gray labels beside some method arguments show parameter names. They are editor hints, not extra source. The editor may draw the two characters in an arrow operator as one joined shape. The source below preserves the exact Java characters.

## 0:00–0:15 — Goal

**On screen:** The title reads “Stream Lifecycle and Result Lists.” The empty Main.java editor appears while the goal is introduced. No output has been shown.

A report pipeline describes work, while its result stores values. We will build a pending stream, collect its report, and make an editable copy.

## 0:15–0:57 — Describe work before collecting

**On screen:** The complete 19-line program is entered and displayed. A selection draws attention to source, pending, the kit addition, and the toList call. Captions stay below the source.

The complete source is:

```java
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Stream;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> source = new ArrayList<String>();
        source.add("map");
        Stream<String> pending = source.stream().map(item -> "Item: " + item);
        source.add("kit");
        List<String> report = pending.toList();
        System.out.println("Reported: " + report.size());
        ArrayList<String> editable = new ArrayList<String>(report);
        editable.add("Item: pen");
        System.out.println("Original result: " + report.size());
        System.out.println("Editable copy: " + editable.size());
        System.out.println("Fresh count: " + source.stream().count());
    }
}
```

Lazy evaluation means processing waits for a terminal operation. Pending describes how to add a label to each source item. Creating it does not collect the report. This ArrayList source is late bound: its contents are observed when terminal processing begins. Notice that kit is added before toList, not while the stream is processing.

## 0:58–1:24 — Copy the result and create a fresh stream

**On screen:** The complete program remains visible. The selection moves to report, the editable copy, and the fresh stream count. Captions remain below the source.

The report is an unmodifiable result list. Its entries cannot be added, removed, or replaced. The ArrayList constructor makes a collection copy with a separate list structure. This is a shallow copy: both lists initially hold the same String references. Strings cannot be changed in place. A stream is single use, so the final count uses a fresh stream from source. Count returns long, Java's wider whole-number type.

## 1:24–1:36 — Predict the result

**On screen:** The selection is cleared and all 19 lines remain visible. The terminal is closed, so no result has appeared. A three-second pause follows the prediction prompt.

Predict all four output lines. Track when kit enters source, when report is collected, and which list receives Item: pen. Pause here.

## 1:36–1:59 — Run and interpret the result

**On screen:** The terminal opens and displays the command and four output lines clearly. This closer view crops the first import and part of the second. Top captions briefly overlap parts of the class and main headers and the source list creation. The following additions, pending stream, collection, copy, and output statements remain readable; earlier views show the complete source. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Reported: 2
Original result: 2
Editable copy: 3
Fresh count: 2
```

The report contains two items because kit was added before collection. Adding Item: pen changes only the editable copy. The original result stays at two, the copy grows to three, and the fresh source count is two. You can read the stored report again, but pending has already been consumed by its terminal operation.

## 1:59–2:14 — Change when an item is added

**On screen:** The wide view restores all 19 source lines, with the source, pending stream, collection, and copy selected. The four original output lines remain visible. The learner is asked to move the kit addition; that edit is not performed in the recording.

Move the kit addition to just after the report is collected. Predict all four counts before running. Which counts should change, and what does that tell you about the report's relationship to its source?

