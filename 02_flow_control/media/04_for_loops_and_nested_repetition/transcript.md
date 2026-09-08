# For Loops and Nested Repetition

## Narration

Welcome to this Java tutorial, where you'll trace a for loop's starting step, test, and update, use an accumulator to keep a running total, and combine nested loops, one inside another, to visit every required pair.

These skills help programs process a known number of items, check totals across repeated work, and cover combinations such as rows and columns in a table.

A workshop assistant needs numbered labels for supply kits assigned to groups. Each label must identify one group and one kit within that group. Group numbers and kit numbers start at one, and every required pair needs exactly one label.

Our report should list the kits for each group in order, then show the number of labels actually printed. We'll begin with a small practice batch, work through several groups, and then predict the report for two groups with two kits each.

Let's open Main.java in the Workspace and start with the practice batch.

Main is the class containing our program, and its main method is where this program begins. We'll place our label-printing statements inside that familiar starter structure.

Before printing any labels, we need a count of the work completed. We'll start labelsPrinted at zero. This variable will be our accumulator: it keeps a running result as the loop does more work.

The count is ready. Our practice batch needs kits one through three, so a for loop can collect the starting step, condition, and update in one header. We'll start kit at one, allow values through three, and increase kit by one after each completed body.

The header is in place, but its written order isn't the full execution order. Initialization happens once. Java tests the condition, runs the body only when that test is true, and then performs the update before testing again. We still need the body to print the current kit and record that completed print.

Each body execution prints one label before increasing the count. Kit tells us which label we're handling; labelsPrinted tells us how many prints have finished. We initialized the count before the loop so earlier progress survives. After the loop stops, we'll print that retained count once and close the program.

The summary sits after the loop's closing brace, so it won't repeat with every kit. Let's click Run to see the complete practice report.

The report lists kits one, two, and three, followed by a count of three. After printing kit three, the update makes kit four. Four fails the condition, so there is no fourth label and no further body execution. The count stays three, and the summary reads it after the loop ends.

We can now print one numbered batch reliably. The workshop also needs to distinguish groups, so we'll replace the practice statements with a report for three groups, each with two kits. A nested loop lets the outer loop choose a group while the inner loop visits that group's kits. We'll keep one count outside both loops.

The outer loop starts with group one, and the count starts with no completed labels. Each time this outer body runs, it must visit that group's kits from the beginning. We'll put a second for loop inside it, initializing kit to one and allowing kits through two.

The inner loop is now inside the group loop. For group one, it will visit kit one and then kit two before the group changes. To identify each pair, we'll build a label from the current group and kit, then increase the shared count after that label prints.

The print uses both current values, and the count records one completed pair. We'll close the inner body first and the outer body second, then put the summary after both loops. That position makes it a report total rather than a separate total for each group.

The nested report is complete. The kit name is available only within the inner for statement; code after that statement cannot use it. Each new outer iteration reaches the inner declaration again and starts kit at one. The same labelsPrinted variable remains available across both loops because we declared it before them. Let's click Run and examine the order.

Group one has two consecutive kit labels, then group two starts again at kit one, and group three does the same. The report contains six different pairs. The accumulator reaches six because it increases after every label, including labels from later groups; it never resets at a group boundary.

At the end of each group, kit advances to three and fails its test against two. The outer update then advances the group. After group three is complete, group becomes four and fails its own test. Only then does the summary print. Both stopping checks matter: the inner one finishes a group, and the outer one finishes the report.

We have a working report for several groups. The actual request has two groups with two kits each, so we'll change only the outer loop's upper limit. The inner rule, the label statement, and the accumulator will stay in their existing positions.

The new group limit is in place. Before running this version, write every output line in order, including the summary. Trace one complete inner loop before advancing the group, and remember when the count changes. Pause here if you'd like more time.

Let's click Run to compare your predicted pairs and total with the actual workshop report.

The first two lines belong to group one, and the next two belong to group two. Each group starts with kit one and ends with kit two. The summary reports four labels. Check both the pair order and the total against your prediction: the right total alone wouldn't prove that every required pair appeared exactly once.

We've built the assistant's complete label report. Each for loop provides a clear start, test, and update; nesting makes the inner kit sequence repeat for each group; and the accumulator counts the labels actually printed. Keeping that count outside both loops preserves the work from every group, while the final false tests stop the report at its intended limits.

For your next experiment, imagine the inner loop starts at kit two instead of kit one, with both upper limits unchanged. Which required labels would disappear, and how would the count respond? Explain the missing work before you run that change.

## Visual description

Four code-free opening scenes show three academic capability columns; a field of rows and columns beside a report; a workshop assistant and workbench with a generic label containing separate group and kit fields; and a single report sheet with group order, kit order, and completed-total requirements. No exact target pair list or total appears in the opening.

The real Workspace then opens Main.java. The class and main method provide the familiar program frame. The editor follows small groups of typed statements. The first program counts completed prints while a for loop visits kits one through three. The actual native Run control is clicked, and the terminal shows:

```text
Kit 1
Kit 2
Kit 3
Labels: 3
```

The practice statements are visibly replaced with an outer group loop containing an inner kit loop. The accumulator stays before both loops. This worked case uses three groups and two kits, producing:

```text
Group 1, kit 1
Group 1, kit 2
Group 2, kit 1
Group 2, kit 2
Group 3, kit 1
Group 3, kit 2
Labels: 6
```

The code then changes only the outer limit from three to two. A prediction pause occurs before the third actual Run click. The final report lists both kits for group one before moving to group two and prints the retained total after both loops. The closing connects initialization, test, update, nested order and persistent count to a complete report. It asks what required labels would disappear if the inner start changed to two, without displaying that transfer answer.

## Canonical program

```java
public class Main {
    public static void main(String[] args) {
        int labelsPrinted = 0;
        for (int group = 1; group <= 2; group = group + 1) {
            for (int kit = 1; kit <= 2; kit = kit + 1) {
                System.out.println("Group " + group + ", kit " + kit);
                labelsPrinted = labelsPrinted + 1;
            }
        }
        System.out.println("Labels: " + labelsPrinted);
    }
}
```

## Exact canonical output

```text
Group 1, kit 1
Group 1, kit 2
Group 2, kit 1
Group 2, kit 2
Labels: 4
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Concept icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Sources and full licenses are retained with the composition.
