# Transcript: Passing Behavior with Lambdas

This CSC-239 demonstration uses Java 21 in the Workspace. A help desk passes different text rules to one rendering method. The recording shows the complete conventional Main.java program and its actual output.

Gray labels beside some method arguments show parameter names. They are editor hints, not extra source. The editor may also draw the two characters in the arrow as one joined shape. The source below preserves the exact Java characters.

## 0:00–0:14 — Goal

**On screen:** The title introduces passing behavior with lambdas. The Workspace shows an empty Main.java while the goal describes a help desk choosing text rules.

A help desk can use different rules to prepare labels. We will pass each rule to the same rendering method, then compare the results.

## 0:14–0:51 — Receive and run a rule

**On screen:** The complete program is typed and saved. All 16 source lines are visible. Lines 2–5 are selected to show the rendering method, its Function parameter, and its call to apply. Captions sit below the source.

The complete source is:

```java
import java.util.function.Function;
class LabelPrinter {
    static String render(String text, Function<String, String> rule) {
        return rule.apply(text);
    }
}
public class Main {
    public static void main(String[] args) {
        Function<String, String> clean = text -> text.trim();
        Function<String, String> tag = text -> "Guest: " + text;
        System.out.println(LabelPrinter.render("  Maya  ", clean));
        System.out.println(LabelPrinter.render("Luis", tag));
        Function<String, String> namedClean = String::trim;
        System.out.println(LabelPrinter.render("  Nora  ", namedClean));
    }
}
```

A functional interface has one abstract method describing an operation. Here, Function takes a String and returns a String. Its first type argument describes the input. The second describes the result. LabelPrinter receives the rule as an argument. Calling apply runs that supplied rule on the text.

## 0:52–1:17 — Supply compatible behavior

**On screen:** The full source remains visible. Lines 9–14 are selected to show the two short expressions that supply behavior, a reference to an existing method, and their use in calls to render. The bottom captions leave these lines clear.

A lambda expression supplies behavior using parameters and a body. Here, text is the parameter. The expression after the arrow is the body. Creating the lambda does not run that body. A method reference supplies compatible behavior from an existing method. String colon colon trim uses trim on the String supplied when apply runs. Trim removes spaces from the ends of these inputs.

## 1:17–1:27 — Predict the result

**On screen:** The selection clears and all 16 lines remain visible. The learner is asked to predict three output lines and explain when each rule runs. A three-second pause follows before the terminal opens. No output is shown during the prediction.

Predict the three output lines. Which rule does each call pass, and when does that rule run? Pause here before checking.

## 1:27–1:47 — Run and interpret the result

**On screen:** The view moves closer to the terminal, where the command and all three output lines are clear. This view crops the import and most of the LabelPrinter class heading at the top. The upper caption briefly overlaps the earlier Main heading area. The call to apply, the supplied rules, and the calls to render remain readable. The complete source was visible in the teaching and prediction views. Lines 9–14 become selected near the end of the explanation. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Maya
Guest: Luis
Nora
```

The first line is Maya, with the surrounding spaces removed. The tag rule adds Guest, a colon, and a space before Luis. The method reference removes the spaces around Nora. Each render call invokes apply, so the same rendering method can use different behavior.

## 1:47–2:01 — Try another label rule

**On screen:** The view widens again, restoring all 16 source lines. Lines 9–14 stay selected while the learner is asked to change only the tag lambda. All three original output lines remain visible, with captions below them. The proposed change is not performed in this recording. A closing pause holds the original source and output.

Change only the tag lambda so it puts square brackets around its input. Predict the second output line, then run again. Which other output lines should stay the same, and why?

