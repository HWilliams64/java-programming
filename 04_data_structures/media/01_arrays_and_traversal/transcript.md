# Arrays and Traversal

## Narration

Welcome to this Java tutorial, where you'll use an array, a fixed sequence of values, select its elements by index, and traverse that sequence with a loop to produce a report.

Storing an ordered batch and applying one rule to its entries helps applications process measurements, report inventory, and handle repeated work without a separate statement for every value.

A campus tour coordinator needs a route report from a supplied list of stop names. We'll store those names in their visiting order, replace one stop when the route changes, and print each stop with its position. Replacement must keep the same number of stops.

A useful report should preserve the route's order, include the replacement, and show the entry count. We'll first work through a two-stop route, then use what we've learned to predict a different three-stop report before running it.

Let's open Main.java in the Workspace and build the first route.

Main is the class containing our code, and its main method is where this program starts. Inside that method, we'll keep library and studio together in a String array. Each stored value is an element. One array keeps the route's visiting order explicit instead of scattering its stops across unrelated variables.

The square brackets in the type tell Java that route refers to an array of Strings. The initializer, the values inside braces, creates two elements in that order. Their indices are zero and one: an index is a position number, and Java starts counting positions at zero. The array's length is two, because length counts entries.

The coordinator has changed the second stop to gallery. We need to replace the element at index one. Assigning to that position changes its stored value while keeping the first stop and the two-position array intact.

The second position now holds gallery. Writing separate print statements would work for this tiny route, but a longer route would require more repeated code. Traversal means visiting the elements in turn. We'll use the for-loop pattern you already know, starting at zero and continuing only while the index is less than the length.

Each accepted index selects one stop for the print statement. The update then advances to the next position. With two entries, zero and one are valid, but two is not. When the index reaches two, the strict comparison is false, so the loop stops before attempting an invalid access. We'll add the entry count after the loop to distinguish that count from the last index.

For this worked route, we expect index zero to report library and index one to report gallery, followed by an entry count of two. Let's run the program and compare that reasoning with its output.

The report shows library, then gallery, with Entries: two underneath. Replacement changed a value, not the length or order. The loop printed exactly two stop lines because its condition accepted only indices zero and one. Notice that the array length has no parentheses; it is a field holding the count, unlike the String length method you've used before.

Traversal can also combine values into a result. A stockroom worker has counted two units in one bin and four in another and needs the total number of units. We don't need position labels for this task, so we'll replace the route example with an integer array and an enhanced for loop, which supplies each element's value in turn.

Amounts stores units per bin, and total starts at zero because no bins have been processed. The enhanced loop will supply each amount to a local variable. Adding that value to the earlier total preserves the units already counted. This produces a running total: the accumulated result after the entries processed so far.

The first iteration adds two to zero. The second adds four to the retained two, making six units. We print once after the loop, so this is a final total rather than a line for each bin. Let's run the stock check.

Units: six is the combined quantity. It is not the array length: there are two entries, each representing a bin. The enhanced loop was convenient because we needed each value but not its index. The indexed loop served the route report because its position labels mattered. Both forms visit the elements in order.

Let's return to the tour coordinator with the lesson's three-stop route. We'll replace the stock example with desk, lab, and hall, change one stored stop, and use the indexed reporting pattern. This time, you'll trace the result before we run it.

The initializer supplies three names in visiting order. We'll assign studio to index one, then print each valid index with the element it selects. The final line reports the array length. Apply the distinction between a position and an entry count as you read the completed program.

Before we run, write every line you expect, including the position labels and final count. Identify which original stop is replaced and explain why the loop never reads index three. Pause the video here if you need more time.

Let's click Run and compare the actual route report with your prediction.

The report shows desk at zero, studio at one, and hall at two, followed by Entries: three. The assignment replaced lab at index one. The other entries stayed in place, and the length stayed three. After printing hall, the loop advanced to three, where the strict bound became false and stopped the traversal.

We've used an array to keep a fixed sequence, an index to replace and read one element, and traversal to report every valid position. We also used an enhanced loop and a running total to combine quantities. The route report meets the coordinator's requirements, while the stock example shows how the same ordered processing supports a different result.

In the notebook, practice choosing valid indices and explaining what each loop's result measures. Compare the array's length with its last valid index, and the number of entries with a sum of their values. Those distinctions will help you choose and test the collections used later in this course.

## Visual description

Four distinct BHCC opening scenes introduce array elements, indices, length and traversal; connect fixed sequences to software data processing; establish a campus tour coordinator and ordered stop names; and state the replacement/order/count requirements. In Main.java, the camera follows each typed code chunk. The worked route stores library and studio, replaces index1 with gallery, and uses an indexed loop plus a count. An actual mouse Run Code click reveals two ordered stop lines and Entries:2. A separate stockroom example accumulates two and four units using an enhanced for loop; another actual Run click displays Units:6. Finally, students predict a three-stop desk/lab/hall route after index1 is replaced with studio. The third actual Run displays desk, studio, hall at indices0,1,2 and Entries:3. The conclusion connects replacement, length and safe traversal back to the report requirements.

## Demonstrated programs and exact outputs

### Program 1

```java
public class Main {
    public static void main(String[] args) {
        String[] route = {"library", "studio"};
        route[1] = "gallery";
        for (int index = 0; index < route.length; index = index + 1) {
            System.out.println(index + ": " + route[index]);
        }
        System.out.println("Entries: " + route.length);
    }
}
```

```text
0: library
1: gallery
Entries: 2
```

### Program 2

```java
public class Main {
    public static void main(String[] args) {
        int[] amounts = {2, 4};
        int total = 0;
        for (int amount : amounts) {
            total = total + amount;
        }
        System.out.println("Units: " + total);
    }
}
```

```text
Units: 6
```

### Program 3

```java
public class Main {
    public static void main(String[] args) {
        String[] locations = {"desk", "lab", "hall"};
        locations[1] = "studio";
        for (int index = 0; index < locations.length; index = index + 1) {
            System.out.println(index + ": " + locations[index]);
        }
        System.out.println("Entries: " + locations.length);
    }
}
```

```text
0: desk
1: studio
2: hall
Entries: 3
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT). Concept icons: Font Awesome Free by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Exact source versions, licenses and hashes are retained in the opening asset evidence.
