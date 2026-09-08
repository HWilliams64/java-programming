# ArrayList and Changing Size

## Narration

Welcome to this Java tutorial, where you'll use an ArrayList, an ordered collection whose entry count can change, to add, replace, remove, and report text entries, then filter values into a separate list.

Collections that can grow and shrink help applications maintain changing requests, preserve meaningful order, and prepare selected records for reports without rebuilding a fixed-size array by hand.

A volunteer coordinator maintains sign-up entries as names arrive. A repeated name remains a separate entry because these are submitted labels, not verified identities. We'll correct one label, remove a canceled entry, and report the remaining names with their current positions.

The report should reflect each change and show the current entry count. We'll first work through one sign-up list, then build a separate list of selected supply labels and check an empty case. Finally, you'll predict a different sign-up report using the same rules.

Let's open Main.java in the Workspace and build the first sign-up list.

Main is the class containing this program, and its main method is where execution starts. We'll import ArrayList from Java's standard library so we can use its short name, then create an empty list for the coordinator's text entries.

ArrayList is a generic class: it can work with different element types. String is the type argument between the angle brackets, selecting text elements for this list. We write it explicitly on both sides here. New creates the empty list, and entries refers to it. Its size is zero because no entries have arrived yet.

The coordinator has received Ella, Sam, and another Ella, in that order. Appending means adding at the end. Each add call appends one entry, so the list can grow while keeping earlier positions and retaining the repeated label.

The entries now occupy indices zero, one, and two. The size is three, which counts entries rather than naming the last position. Sam's label needs to become Noor. We'll use set with the existing index first and the replacement text second, then remove the first entry because it was canceled.

Set replaces Sam with Noor without growing the list. Remove receives the integer zero, so it removes the entry at that index. Noor shifts from one to zero, and the remaining Ella shifts from two to one. Indices describe current positions; they aren't permanent identifiers attached to an entry.

To report those current positions, we'll traverse the list with an indexed for loop. Size is a method call on the list, unlike the length field of an array. Keeping the index strictly below that count prevents an attempt to read one position past the end. Get reads the element at the accepted index without removing it.

For this worked list, index zero should report Noor, and index one should report Ella, followed by an entry count of two. Let's run it and check both the order and the size.

The output matches: Noor at zero, Ella at one, and two entries. The three appends increased the count, replacement kept it unchanged, and removal decreased it. The report reads the positions after those changes, which is why Noor now appears at zero.

Sometimes we need a selected result while keeping the original data. A supply organizer has the labels pen, hold, card, and pen. Hold marks a request that shouldn't be printed yet. We'll replace the sign-up program with that source array and a separate result list, keeping the usable labels in their original order.

Labels keeps the original four entries. Selected starts empty because we haven't accepted any yet. Filtering means keeping values that meet a condition. An enhanced for loop supplies each source value in turn; the condition accepts a label only when it does not equal hold. The append belongs inside that condition so rejected labels never enter the result.

The first pen is accepted, hold is rejected, and card and the second pen are accepted. The selected list therefore contains pen, card, and pen in that order. No statement assigns to a source position. The organizer also wants to substitute marker for the first printable label, but there might be no printable labels. Before using index zero, we must check that the result contains an entry.

This size check is a guard: it permits the indexed operation only when an entry exists. Here the size is three, so replacement changes the first pen to marker without changing the count. If the list were empty, the condition would be false and the set call would be skipped. We'll print the result values with an enhanced loop because this report doesn't need position labels.

We expect marker, card, and pen, followed by three selected labels and a source count of four. The selected count measures accepted entries, while the source count still includes the held request. Let's run this report.

The result has the requested substitution and three labels. The source still has four entries, and the code only modified the separate list. Filtering decided which values to append; the guard then controlled whether the first retained position could be replaced. Those are separate decisions.

A successful ordinary case doesn't tell us whether indexed access is safe when no data arrives. We'll replace this program with the same filtering, guard, and reporting logic, changing only the source initializer to an empty array. Its braces contain no values.

The source loop has no elements to visit, so it appends nothing and selected stays empty. We'll retain the guard and reporting logic. The size check will skip replacement, and the enhanced reporting loop will also have no elements to visit.

This time there should be no individual label lines. Both count lines should report zero. Let's run and check that the empty case finishes normally.

Both counts are zero, and there are no label lines or indexed-access errors. The false guard prevented the invalid replacement. A nonempty source containing only hold labels would also produce an empty selected list, so the check must use the result's size rather than the source's length.

Let's return to the volunteer coordinator for your prediction. We'll replace the supply example with the lesson's sign-up program. It appends Maya, Luis, and Maya, then corrects one entry and removes another before reporting current positions. Use the worked sign-up rules to trace this new input.

The three add calls preserve the submitted order and repeated name. We'll complete the program with the correction, indexed removal, and reporting loop. Read each operation in order, updating the current positions whenever the list changes.

Before we run, write every line you expect, including the position labels and final count. Explain which operation changes a value without changing the size, and which operation changes later indices. Pause the video here if you need more time.

Let's click Run and compare the actual report with your prediction.

The report shows Nora at zero, Maya at one, and Names: two. Set replaced Luis at index one while keeping three entries. Remove then deleted the first Maya, shifting Nora and the remaining Maya to their current positions. The loop read only those two valid indices, and the size method returned the current entry count.

The coordinator's report now reflects the correction and cancellation while preserving the remaining order. You've used an ArrayList to manage a changing entry count, distinguished append, replacement, removal, and reading, and used traversal to report the result. The supply example also showed how filtering builds a separate list and how a size guard protects an indexed operation when the result is empty.

In the notebook, explain why replacing an element cannot create the first entry in an empty list. Then compare an empty source with a source whose entries are all rejected by a filter. What stays the same about the result, and which count could differ? Use those cases when checking your own collection code.

## Visual description

The opening uses four distinct arrangements: a changing ordered list with add, replace, and remove labels; rows connecting list management to application work; a coordinator reviewing submitted entries; and an annotated report with a separate selection result. The opening introduces the learning outcomes, broader relevance, and concrete task before the Workspace appears.

In the real Java Workspace, the instructor builds a complete Main class in small chunks. The first program adds Ella, Sam, and Ella to an ArrayList, replaces the entry at index one with Noor, and removes the entry at index zero. An indexed loop then displays Noor and Ella with their current positions, followed by an entry count of two. Each operation is explained through its effect on the current list.

The next complete program reads a source array containing pen, hold, card, and pen. An enhanced for loop appends every label except hold to a separate ArrayList. A size guard permits replacement of its first entry with marker only when an entry exists. The visible output contains marker, card, pen, Labels: 3, and Source count: 4. The original source array remains unchanged. The instructor then replaces the source array with an empty array and runs the same logic. Only Labels: 0 and Source count: 0 appear; the guard and loops skip their bodies safely.

For the final canonical program, names are added in the order Maya, Luis, Maya. The entry at index one becomes Nora, then index zero is removed. The instructor asks learners to predict the current names and count before clicking the actual Run control. The output shows 0: Nora, 1: Maya, and Names: 2. The closing connects these observations to ordered entries, changing size, safe indexed access, and filtering into a separate list.

The camera follows actual caret positions during typing and widens for each real mouse Run action and its console output. Captions accompany the complete narration. Code, output, and Run controls must remain visible in the final reviewed composition.


## Canonical program

```java
import java.util.ArrayList;
public class Main {
    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<String>();
        names.add("Maya");
        names.add("Luis");
        names.add("Maya");
        names.set(1, "Nora");
        names.remove(0);
        for (int index = 0; index < names.size(); index = index + 1) {
            System.out.println(index + ": " + names.get(index));
        }
        System.out.println("Names: " + names.size());
    }
}
```

## Exact canonical output

```text
0: Nora
1: Maya
Names: 2
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Concept icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Sources, licenses and hashes are retained in production evidence.
