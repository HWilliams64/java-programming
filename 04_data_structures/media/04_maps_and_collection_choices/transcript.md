# Maps and Collection Choices

## Narration

Welcome to this Java tutorial, where you'll use a HashMap to associate keys with values, replace a stored value, and retrieve information by its key.

These associations let applications find quantities by product name or totals by category, giving later reports and business rules a consistent way to work with named data.

A campus supply desk is checking its stock. The names pen and tag identify kinds of supplies, and each stored whole number is the quantity of physical items available. A corrected count must replace the earlier quantity for that same kind.

We'll store two quantities, correct one of them, and print the current quantities plus the number of recorded kinds. Then you'll predict a second stock report using different supplies before we run it.

Now that we're in the Workspace, let's open Main.java.

We need the HashMap class for our stock record. We'll import it, then put the program's statements inside main, the starting method in the Main class.

The program structure is ready. Our stock record needs text keys for the supply names and whole-number values for the quantities. Let's create an empty map with those two roles.

String identifies the key type, and Integer identifies the value type. Integer is the object form used to store a whole number in this map; the generic value position cannot use primitive int. The new expression creates the empty map, and stock refers to it.

Now we can record four pens and two tags. Each put call associates its first argument, the key, with its second argument, the quantity. Java automatically boxes each primitive number into the Integer form this map stores.

Those statements establish two associations. The desk then counts five pens, so the earlier pen quantity is no longer current. We'll put the corrected value under the existing pen key.

That put replaces four with five; it does not add five to four or create another pen key. The tag association stays unchanged. To build the report, we'll use get to look up each quantity by name and print it beside a label.

Each lookup supplies the Integer value currently associated with its key. Joining that result to a text label displays the number, so readers see the quantity rather than needing to understand its stored type. Both keys were inserted earlier; a missing lookup would instead return null, which is not numeric zero.

The report also needs the number of supply kinds on record. Size counts the map's distinct keys, not the sum of its quantities. Let's add that final line and finish the program.

The complete program now corrects one quantity and asks two different questions: how many items of each kind are available, and how many kinds are recorded. Let's click Run and check those results.

Pens is five because the later put replaced the earlier four. Tags stays two. Types is two because pen and tag are the two distinct keys. The current quantities total seven items, while size counts two kinds. Our explicit print statements determine which report line appears first.

The map gives each name a current value. A replacement changes that association without changing the key count. We did not need list positions or a promised HashMap traversal order to find these named quantities.

Let's apply the same rules to the desk's map and kit supplies. We'll replace the worked program with a fresh stock record, enter its initial quantities, and correct the map quantity. Keep your prediction for the complete report until all its statements are visible.

The two starting associations and the correction are entered. Now we'll add the named lookups and the key-count report, using the same operations as the worked case.

Before running the completed program, predict all three labeled output lines. Track the current value for each key after every put, then decide what size counts. Pause here if you'd like more time.

Let's click Run to compare the program's report with your prediction.

Maps is three because the second put for map replaced its earlier quantity of two. Kits stays one. Types is two because the record still has the same two distinct keys. The quantities add to four, but that is a different total from the number of kinds.

The desk now has a report of its corrected stock. Keys identify the supplies, put maintains each current value, and get retrieves those values for output. Distinguishing quantities from the key count makes the report meaningful and prepares you to build the frequency tables in the notebook.

Suppose a recount changes a recorded supply quantity to zero. Would that put remove the key or change the number of recorded kinds? Explain how you would distinguish that recorded zero from a supply name that was never entered.

## Visual description

Four distinct opening scenes show a Name-to-Quantity association beside academic goals; application rows for product quantities and category totals; a campus staff member beside a stock-count sheet; and an annotated current-stock report. The opening introduces the expected behavior without revealing the later prediction's answer.

The real Workspace shows Main.java. Eight groups of source are typed while the camera follows the insertion point. The worked HashMap associates pen with4 and tag with2, then replaces the pen quantity with5. Named get calls print the current quantities, and size reports the number of distinct keys. The actual Run Code toolbar button is clicked for each of two complete programs.

### Worked pen and tag

```java
import java.util.HashMap;
public class Main {
    public static void main(String[] args) {
        HashMap<String, Integer> stock = new HashMap<String, Integer>();
        stock.put("pen", 4);
        stock.put("tag", 2);
        stock.put("pen", 5);
        System.out.println("Pens: " + stock.get("pen"));
        System.out.println("Tags: " + stock.get("tag"));
        System.out.println("Types: " + stock.size());
    }
}
```

Actual output:

```text
Pens: 5
Tags: 2
Types: 2
```

### Canonical stock prediction

```java
import java.util.HashMap;
public class Main {
    public static void main(String[] args) {
        HashMap<String, Integer> stock = new HashMap<String, Integer>();
        stock.put("map", 2);
        stock.put("kit", 1);
        stock.put("map", 3);
        System.out.println("Maps: " + stock.get("map"));
        System.out.println("Kits: " + stock.get("kit"));
        System.out.println("Types: " + stock.size());
    }
}
```

Actual output:

```text
Maps: 3
Kits: 1
Types: 2
```

The editor is cleared before a fresh map-and-kit stock program is entered. An eight-second prediction pause leaves its complete source visible before execution reveals the answer. The closing explains replacement, named lookup and the difference between quantities and the key count. It asks whether recording zero removes a key and how recorded zero differs from a missing association; that transfer answer is not revealed.

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Icons: Font Awesome Free6.7.2 by Fonticons, Inc. (CC BY4.0). Full licenses and provenance remain with the composition.
