# Transcript: Objects and Constructors

This CSC-239 demonstration uses Java 21 in the Workspace. It defines one pass class, creates two separate objects, and reports their independent visit counts.

## 0:00–0:17 — Goal

**On screen:** The title introduces one design with independent visit counts. Main.java is open in the Java editor. No visit-count result is revealed.

Two visitors share one pass design, but each pass keeps its own visit count. DeskPass is the class: one definition of the state and behavior each object has.

## 0:17–0:48 — Define fields and initialization

**On screen:** The following source is typed and saved. The DeskPass fields, constructor and visit method receive emphasis. All 22 source lines are readable during explanation and prediction, with no editor errors. Gray owner: labels beside the constructor arguments are editor hints, not source text to type.

```java
class DeskPass {
    String owner;
    int visits;
    DeskPass(String owner) {
        this.owner = owner;
        this.visits = 0;
    }
    void visit() {
        this.visits = this.visits + 1;
    }
}
public class Main {
    public static void main(String[] args) {
        DeskPass first = new DeskPass("Maya");
        DeskPass second = new DeskPass("Luis");
        first.visit();
        first.visit();
        second.visit();
        System.out.println(first.owner + ": " + first.visits);
        System.out.println(second.owner + ": " + second.visits);
    }
}
```

Owner and visits are instance fields, stored separately in each object. The constructor has the class name and no return type. It initializes a new pass. This refers to the current object, separating its owner field from the matching parameter.

## 0:49–1:03 — Predict the independent visit counts

**On screen:** The two object creations, visit calls and print statements receive emphasis. The DeskPass definition stays visible above them. Bottom captions leave all source readable. No terminal output has appeared. A three-second pause follows the prediction.

Visit is an instance method: it updates the object used for the call. Each new creates a separate pass. Trace the calls below and predict both printed lines, then pause.

## 1:03–1:20 — Execute and compare

**On screen:** The view focuses on the terminal. The top of the DeskPass definition is partly above the visible area, and top captions overlap earlier constructor statements and part of the visit method heading. Its update statement, the object creations, visit calls and print statements remain visible. The command and both output lines are clearly readable. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
Maya: 2
Luis: 1
```

Maya's pass receives two visits; Luis's receives one. Updating the first pass leaves the second unchanged. One method definition applies the same rule to both objects, so we avoid copying its implementation.

## 1:20–1:30 — Add a visit to one pass

**On screen:** The full source and both output lines remain visible during the final question. Bottom captions leave both clear. The proposed change adds one call to second.visit() before printing. A two-second hold follows the question.

Add one more call to second's visit method before printing. Which line changes, and why does the other pass keep its count?

