# Stream Lifecycle and Result Lists — video transcript

## Narration

Welcome to this Java tutorial, where you'll distinguish a stream's pending computation from its completed result and create a separate editable collection copy. You'll trace when processing occurs, when a fresh stream is needed, and which list an edit changes.

Software often needs both a generated report and an editable working draft. Separating those objects lets one feature preserve its result while another makes changes. It also helps you request a new computation without trying to reuse a stream that has already finished.

A supply desk starts with a request for map, and a kit request arrives later. Each collected report entry adds Item, a colon, and a space before the item name. After collection, the desk adds a pen label only to an editable copy. Our measurements count entries, not characters.

We'll compare the report size, the edited copy's size, and a fresh count of the source. First we'll collect before kit arrives. Then you'll predict what changes when that same addition moves before collection. The report must preserve its completed entries while the working copy can change.

Now that we're in the Workspace, let's open Main.java and set up the types that give the source, pipeline, and report their different roles.

We'll import ArrayList for stored input and the editable copy, List for the collected report, and Stream for a pending computation. Main is the class containing this program, and its main method is where execution starts. Our statements belong inside that method.

The report needs an input and a labeling rule before it can run. Let's create the source with map, then store a mapping pipeline in pending. The mapping adds the Item label to each element when that element is processed.

Pending holds a description of the work; no report has been collected yet. This is lazy evaluation: intermediate operations describe processing before a terminal operation starts it. Creating the stream also does not freeze a copied list of source entries.

For this first worked case, let's collect now, then add kit afterward. Keeping those two statements separate makes the timing visible.

To list is the terminal operation that collects the report. This ArrayList stream observes its source when terminal processing begins, which is called late binding. Here only map is present then. The following addition changes the source after collection has completed; it does not insert another entry into that completed report.

Let's print the size of the collected report so the output records what this computation produced.

Reported measures the completed list. We also need a working draft that can accept pen while the report remains unchanged. The to list result is unmodifiable: it supports reads but rejects adding, removing, or replacing entries. We'll give the draft its own ArrayList structure.

The constructor copies the report's current entries into a new list, and the addition targets only that copy. This is a shallow copy: the lists initially hold references to the same String elements. The constructor does not create new String objects. Adding pen changes list membership, without changing any String in place.

Let's print the original report and copy sizes separately, then request a fresh stream to count the source. A stream is single use, so this new count must not reuse pending after its earlier terminal operation.

Count returns long, Java's whole-number type with a wider range than int. We can print that value directly. The report was collected before kit arrived; the working copy received pen; the source now contains both requests. Let's click Run to compare those measurements.

Reported and Original result are both one. The completed report still contains only the map label. The editable copy grows to two after pen is added. Fresh count is two because the new stream counts the source after kit has been added. Reading the report again did not rerun the consumed pipeline.

Now let's move the kit addition before the report is collected. We'll replace just these two lines in their opposite order. The source values, mapping, copy edit, and print statements stay the same.

Before running, predict all four lines. Which source entries exist when terminal processing starts now? Which list receives pen, and which entries does the fresh count measure? Use those three object roles to explain which numbers should change.

Let's click Run and compare your timing prediction with the actual output.

Reported and Original result are now two because map and kit are both present before collection begins. The copy starts with those two labels and grows to three when pen is added. Fresh count stays two: it measures the source, which never received the copy's pen entry.

You separated a pending computation, a completed report, and an editable working list. Late binding explained the input seen at collection; a fresh stream enabled another computation; and a shallow collection copy gave edits their own list structure. For a transfer task, describe a report whose input can change after generation. Explain when you would read the existing report, copy it for editing, or request a new computation.

## Visual description

[Four designed opening scenes distinguish a pending stream computation from a completed report and editable copy, explain why reports and working drafts need separate roles, introduce the map and kit supply requests and Item labeling rule, and present the measurements without revealing the later prediction.]

[The real Workspace opens Main.java. The camera follows typing of the ArrayList, List and Stream imports, Main and main, the source containing map, and the pending mapping pipeline. The first worked case collects the report before adding kit. Separate code builds an editable ArrayList copy, adds Item: pen only to that copy, and prints the report, copy and fresh source counts.]

[The pointer clicks the native Run Code button. The four output lines are Reported: 1, Original result: 1, Editable copy: 2 and Fresh count: 2. The completed report contains only the map label; the source now contains map and kit; the separate copy also has pen.]

[Two adjacent statements are replaced in reverse order so kit is added before collection. Narration asks students to predict all four lines and allows a thinking pause before the second visible Run Code click. The canonical output is Reported: 2, Original result: 2, Editable copy: 3 and Fresh count: 2. The closing connects late binding, a fresh computation and a shallow collection copy to the separate roles of source, report and editable draft.]
