# Transcript: Reduction and Parallel Streams

This CSC-239 demonstration uses Java 21 in the Workspace. A list supplies three item counts. Two fresh pipelines combine those counts into totals. The recording shows the complete Main.java program and its actual output.

Gray labels beside some method arguments show parameter names. They are editor hints, not extra source. The editor may draw the two characters in an arrow operator as one joined shape. The source below preserves the exact Java characters.

## 0:00–0:17 — Goal

**On screen:** A title card names Reduction and Parallel Streams. The Workspace then shows an empty Main.java editor while the goal is introduced. No output is shown.

We will total three item counts with two fresh stream pipelines. The goal is the same correct sum whether the work stays together or is split into parts.

## 0:17–0:57 — Choose an identity and combination

**On screen:** The complete 14-line program is typed and saved. Lines 5–9 select the source list and first reduce call. All source lines, including both complete reduce expressions, remain readable above the bottom captions.

The complete source is:

```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> counts = new ArrayList<Integer>();
        counts.add(2);
        counts.add(4);
        counts.add(1);
        int sequential = counts.stream().reduce(0, (left, right) -> left + right);
        int parallel = counts.parallelStream().reduce(0, (left, right) -> left + right);
        System.out.println("Sequential: " + sequential);
        System.out.println("Parallel: " + parallel);
    }
}
```

Reduction combines elements into one result. Reduce uses zero as its identity: a neutral starting value that leaves a sum unchanged. The lambda combines left and right. Its two Integer inputs and Integer result match BinaryOperator, the functional interface for this combination. Addition is associative: grouping two and four first, or four and one first, gives the same sum. Subtraction can change when regrouped.

## 0:58–1:32 — Keep parallel processing correct

**On screen:** Lines 9–12 select both reduce calls and their print statements. The full program remains visible as the narration explains how the two calls combine values and what makes parallel processing correct.

Sequential processing handles the pipeline without splitting it into parallel parts. Parallel stream processing can compute parts at the same time and combine their results. Our lambda is stateless: its result depends only on its inputs, not changing shared values. Noninterference means leaving the source unchanged while processing. These rules support a correct reduction without a shared total. Encounter order does not promise the order in which parallel work happens. Splitting and combining add work, so parallel execution is not automatically faster.

## 1:32–1:44 — Predict the result

**On screen:** The selection clears and the complete program remains visible. The terminal is closed and the result has not been shown. A three-second pause follows the prediction prompt.

Predict both printed lines. Start with the identity, combine all three counts, and decide whether splitting the work should change the total. Pause here.

## 1:44–2:02 — Run and interpret the result

**On screen:** The view moves closer to the terminal. Both output lines and the complete reduce expressions remain readable. The import is above the cropped view, and a top caption briefly covers parts of the main header, list creation and first two additions. Those lines were fully visible during the earlier explanation and prediction views. The original program is run once; no parallel work order is displayed. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Sequential: 7
Parallel: 7
```

Both totals are seven. Zero adds nothing, and addition gives the same sum under regrouping. The print statements display the sequential result first and the parallel result second. That display order does not show which parallel part ran first.

## 2:02–2:18 — Test and extend the reduction

**On screen:** The wider view returns, showing all 14 source lines and the original two output lines. Lines 5–10 are selected while the learner is asked to change the list and extend the pipelines. The video leaves these changes for the learner and ends with a short hold on the unchanged program.

Add another four, then predict both totals. Next, try an empty list. How could you place filter and map before reduce to total only doubled positive counts? Explain why zero and addition still fit.

