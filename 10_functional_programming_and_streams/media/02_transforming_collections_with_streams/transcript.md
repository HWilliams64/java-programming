# Transforming Collections with Streams — video transcript

## Narration

Welcome to this Java tutorial, where you'll learn how stream pipelines use mapping, filtering, and a terminal operation to transform collection entries into an ordered report. A pipeline describes a sequence of operations over the source's entries.

Reports often need cleaned data and a clear selection rule. Keeping those steps separate makes their order easier to inspect and change, while the original collection remains available to other features. A pipeline builds on the small rules you've already supplied through lambdas and method references.

A registration desk needs a report of names with at least four characters after surrounding spaces are removed. Its entries can contain padded names, short names, or empty text. We'll keep qualifying entries in their original relative order, with repeated matching entries allowed.

The report should display each retained name and then the number selected. First we'll trace a worked input. Then you'll predict the report for a different input before we run it. The original list and the completed report have different jobs.

Now that we're in the Workspace, let's open Main.java and set up the two list types used by our report.

We'll import ArrayList for the source and List for the result. Main is the class holding our program, and its main method is where the program starts. The collection setup and report statements will go inside that method.

List is an interface for an ordered sequence that can contain repeated entries. We'll use it to read the completed report. First, let's create the source ArrayList with padded Nora, Kim, padded Bo, and empty text, in that order.

The four add calls establish the source order. Nora has two spaces on each side; Bo has one. Empty text is a String with no characters. We need to remove surrounding spaces before deciding whether a name meets the report's length rule.

Let's request a stream over names and add a mapping stage that supplies cleaned text. The selected variable will hold the final result once we complete the pipeline.

A stream describes processing over the collection; it isn't another list of copied entries. Map accepts the String trim method reference. Each processed String becomes the receiver of a trim call, and the returned cleaned String reaches the next stage. This doesn't replace the original entry or edit a String in place.

Cleaning alone doesn't decide which names belong in the report. We'll add a filter that keeps an entry only when the cleaned value has at least four characters.

The lambda receives the value from the preceding map. Its Boolean result controls whether that value continues. Nora has four characters after cleaning and passes. Kim has three, Bo has two, and empty text has zero, so those entries fail. Filtering selects entries; it doesn't store true or false in the report.

The intermediate stages now describe the work. Let's complete the expression with the terminal operation that processes the pipeline and produces our list.

To list collects the retained values. The semicolon ends the whole declaration and assignment; the earlier line breaks only make its stages readable. This result preserves the surviving ArrayList order, including repeated matches. It is unmodifiable, so our report will read its entries and size rather than add, remove, or replace entries.

The completed result still needs to be displayed. We'll use an enhanced for loop to print each selected name, then print the result's size. These statements read selected after the pipeline completes.

The loop prints one line for each retained entry. The final line labels the count as Selected. It measures the result list, not the original four-entry source. Let's click Run and inspect the worked report.

The report shows Nora and a selected count of one. Mapping removed the surrounding spaces, filtering kept the cleaned four-character name, and the terminal operation produced the list that the loop read. The original list still contains all four source entries; the report didn't remove rejected entries from it.

Let's keep the pipeline and printing statements unchanged. We'll replace just the first three inputs with padded Maya, Li, and padded Luis. The last input will remain empty text. This changes the data while keeping the same report rules.

Before running, predict every printed line, including the count. For each original entry, identify the value after trimming and the result of the length check. Which entries reach the result, and what order should they have? Pause here to trace the pipeline.

Let's click Run and compare your prediction with the actual report.

The output shows Maya, then Luis, then Selected two. Both retained names have four characters after trimming. Li and empty text fail the same condition. Maya stays before Luis because that is their relative order in the source. The count belongs to the completed result, not to the original input.

You built a stream pipeline that maps input values, filters the mapped results, and collects an ordered report with a terminal operation. The position of each stage determines what its rule receives. For a transfer question, imagine checking product codes that may contain surrounding spaces. Give one input for which testing length before cleaning would change the report, and explain the order your rules should use.

## Visual description

[Four designed opening scenes introduce stream pipelines, mapping, filtering and a terminal operation; connect separate reporting rules to an application that retains its source collection; describe a registration desk that cleans names and selects cleaned lengths of at least four; and present a variable-length report with a blank count. No later prediction output is revealed.]

[The real Workspace appears and Main.java opens. The camera follows typing of the ArrayList and List imports, Main class and main method, the ordered names source, the map and filter stages, the toList terminal operation, and a later printing loop and count line. Narration separates describing stages, processing entries, obtaining a completed result, and printing that result.]

[The pointer clicks the native Run Code button. The worked source contains padded Nora, Kim, padded Bo and an empty String. The terminal shows Nora followed by Selected: 1. Cleaning happens before the length rule, and the later printing reads the result list.]

[Three input literals are edited to the retained canonical values: padded Maya, Li and padded Luis. The empty String, pipeline and printing remain unchanged. A prediction question and thinking pause precede the second native Run Code click. The terminal shows Maya, Luis and Selected: 2 on separate lines. The closing connects ordered reporting to the separate source and result roles and asks how cleaning before a length check could affect product-code selection.]
