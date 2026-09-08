# Transcript: Encapsulation and Shared References

This CSC-239 demonstration uses Java 21 in the Workspace. It protects each supply bin through public operations and compares instance stock with a shared class counter.

**Notebook use:** The video runs Main.java in a new Java process. In the notebook, restart the Java kernel before replaying a counted example or solution. Repeating an identical class definition can keep its static counter. Supplementary examples use distinct class names so a fresh Run All keeps their counters separate.

## 0:00–0:19 — Goal

**On screen:** The title introduces protecting stock through public operations. Main.java is open in the Java editor. No request result is revealed.

A supply bin must never issue more items than it holds. Encapsulation keeps its state behind operations that control changes. We start each bin with nonnegative stock.

## 0:19–1:00 — Guard changes to stock

**On screen:** The following source is typed and saved. The private fields, constructor and guarded take method receive emphasis. All 32 source lines are readable during explanation and prediction, with no editor errors. Gray stock: and amount: labels identify arguments as editor hints; they are not source text. The editor joins the characters in <= into a single-looking symbol; the source still uses the two characters shown below.

```java
class SupplyBin {
    private int stock;
    private static int binsCreated = 0;
    public SupplyBin(int stock) {
        this.stock = stock;
        binsCreated = binsCreated + 1;
    }
    public boolean take(int amount) {
        if (amount <= 0 || amount > stock) {
            return false;
        }
        stock = stock - amount;
        return true;
    }
    public int getStock() {
        return stock;
    }
    public static int getBinsCreated() {
        return binsCreated;
    }
}
public class Main {
    public static void main(String[] args) {
        SupplyBin pens = new SupplyBin(5);
        SupplyBin maps = new SupplyBin(2);
        System.out.println("Take 3: " + pens.take(3));
        System.out.println("Take 4: " + pens.take(4));
        System.out.println("Pens: " + pens.getStock());
        System.out.println("Maps: " + maps.getStock());
        System.out.println("Bins: " + SupplyBin.getBinsCreated());
    }
}
```

Private fields cannot be changed directly by this caller. Public methods provide access. The take method rejects a nonpositive or excessive request before changing stock. That protects the rule that stock stays nonnegative.

## 1:00–1:17 — Predict instance and class state

**On screen:** The two bin creations, requests and five report statements receive emphasis. The complete SupplyBin definition stays visible above them. Bottom captions leave all source readable. No terminal output has appeared. A three-second pause follows the prediction.

Each bin has its own stock. The static binsCreated field belongs to the class, and the constructor updates it for every new bin. Trace both take calls and predict all five lines, then pause.

## 1:17–1:30 — Execute and compare

**On screen:** The view focuses on the terminal. The top of the class definition is partly above the view, and the longer top captions overlap earlier constructor statements and part of the take method heading. The guard, update, getters and caller code remain visible. The final outer closing brace is below the editor edge. The command and all five output lines are clearly readable. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
Take 3: true
Take 4: false
Pens: 2
Maps: 2
Bins: 2
```

Taking three succeeds, leaving two pens. Taking four fails without changing that stock. The maps bin still has two. The shared count is two because two bins were constructed.

## 1:30–1:41 — Change a request

**On screen:** The fields, constructor, guard, getters, caller code and all five output lines remain visible during the final question. The last outer closing brace stays below the editor edge. Bottom captions leave the source and output clear. The proposed change updates the second take argument and its printed label to two. A two-second hold follows the question.

Change the second request and its printed label to take two. Predict the new results. Why do the maps stock and the class count stay the same?

