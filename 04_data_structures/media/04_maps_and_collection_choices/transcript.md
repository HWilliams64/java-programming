# Transcript: Maps and Collection Choices

This CSC-239 demonstration uses Java 21 in the Workspace. It associates supply names with quantities, replaces a stored quantity, and reports the values and number of distinct keys.

## 0:00–0:14 — Goal

**On screen:** The title introduces associating supply names with quantities. Main.java is open in the Java editor. No output is revealed.

A supply desk needs quantities for named items. A map links each unique key, an item's name, to a value, its quantity.

## 0:15–0:41 — Choose key and value types

**On screen:** The following source is typed and saved. Construction and put calls receive emphasis. All 12 source lines remain visible during the explanation and prediction, with no editor errors. Gray key: and value: labels are editor hints that identify arguments; they are not source text to type.

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

String and Integer are the key and value types. Integer is the object form of int, required here as a type argument. Java converts each supplied number automatically; that conversion is called boxing.

## 0:41–0:54 — Predict replacement and key count

**On screen:** The put calls, retrieval statements and key count receive emphasis. Bottom captions leave the full source visible. No terminal output has appeared. A three-second pause follows the prediction.

Put stores a value, replacing any value already under that key. Get retrieves by key, and size counts keys. Predict the three printed lines, then pause.

## 0:54–1:08 — Execute and compare

**On screen:** The view focuses on the terminal. The import and part of the class declaration are above the visible area, and top captions overlap earlier construction and put lines. The retrieval and count statements remain visible, and the command and all three output lines are clearly readable. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
Maps: 3
Kits: 1
Types: 2
```

The later put replaces two with three for map. Kit still holds one. There are two keys, so size is two. These print statements choose the order; HashMap traversal does not promise it.

## 1:08–1:19 — Change a quantity

**On screen:** The full source and all three output lines remain visible during the final question. Bottom captions leave both clear. The proposed change replaces only the quantity in the last put call; its key stays map. A two-second hold follows the question.

Now change only the last put to store five under map. Which output line changes, and why does the number of keys stay the same?

