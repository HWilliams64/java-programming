# Buffered Files and Prefix Queries — video transcript

## Narration

Welcome! In this Java tutorial, you'll read text a line at a time with a buffered reader, which holds groups of text in memory, and build a dictionary that checks whole words and prefixes, the beginnings of words.

Buffered line processing and clear resource lifetimes help applications load saved lists, reports, and word dictionaries, while separate whole-word and prefix queries let a game reuse that data without repeating its file-reading code.

Our word-game developer has a dictionary file containing cat, cart, a blank line, dog, and cat again. We'll keep each nonempty line exactly as written and retain each distinct word only once.

The completed load should report three distinct words. A query for the prefix c a should succeed, while z z should find no match. We'll read until the file ends and close the reader before reporting these results.

Now that we're in the Workspace, let's open Main.java and build the dictionary helper.

We'll begin with the types for file locations, UTF-8 text, the buffered reader, and a set of unique words. IOException gives the handler a specific type for failures while opening, reading, or closing the file.

These imports supply the types' short names. Files performs the file operations, while HashSet will retain distinct words. Before loading the file, let's define the question that this set will answer: does any stored word begin with the supplied prefix?

WordChecks groups our helper method. The method receives the set and the requested prefix as two inputs, and returns a Boolean result. Because the method is static, the application will call it through the WordChecks class name. We need to search until a word matches or no words remain.

The loop checks each word's beginning. A match returns true immediately. A failed comparison only moves the search onward; false belongs after the loop, once no word matched. This result does not depend on the set's traversal order. Complete membership is different: a set containing cart can satisfy prefix c a without containing c a as a whole word.

With the query helper ready, let's add Main, the class containing the application entry point. Its main method is where execution starts. We'll put our fixture creation and dictionary load inside a try block so an I/O failure reaches a matching handler.

The helper is defined above, but it will not run until we call it. First, the main method needs a controlled file to read. We'll create a new practice directory and write the developer's five lines there using UTF-8.

The new directory separates this run from earlier files. Resolving words dot text describes its child location; the write actually creates the file. Two adjacent newline characters leave the blank line between cart and dog. The repeated cat remains in the file even though the dictionary will retain it only once.

Now we'll create the empty set and open a buffered reader with the same UTF-8 encoding. Declaring the reader in try-with-resources gives it a clear lifetime. The first read must happen before the loop can decide whether a line exists.

The reader may read ahead into its buffer, while each readLine call returns one line's text without its ending characters. The first value here is cat. At the end of the file, a later read will return null, meaning there is no next line. An empty String is a real line value, so it must not end the loop.

We'll separate the decision to keep reading from the decision to store the current line. The outer condition checks for null. Inside it, a length check allows only nonempty text into the set.

Cat and cart pass both checks and become members. The blank line passes the null test but fails the length test, so only its addition is skipped. We preserve case and spaces rather than silently changing the text. The remaining step must advance the reader even when nothing was added.

Each body execution reads the next line. That lets the loop reach dog and the repeated cat after the blank line. The set adds dog, but the equal cat adds no new member. Once a read returns null, the next guard ends the loop without another body execution. Leaving the resource block then closes the reader; the words already stored in the set remain available.

The load is complete, so we'll report the number of retained words and call our helper for the two prefixes. These prints come after the reader closes successfully. A load failure will therefore skip these normal reports rather than look like an empty dictionary.

The size report counts distinct nonempty words, not all five input lines. Each prefix call receives the same loaded set and its own requested beginning. Let's finish the handler so a failed file operation reports its actual exception message.

Our complete program creates the file, reads and filters every line, closes the reader, and queries the retained set. Let's click Run and check the developer's expected count and prefix results.

The count is three: cat, cart, and dog. The blank line did not stop reading, and repeated cat did not increase membership. Prefix c a succeeds because a stored word begins with it. Prefix z z fails after every stored word has been considered. These reports follow a successful load and close.

Apply those same rules to a different file. We'll use map, a blank line, moss, mud, mint, and map again, with no newline after the final word. We'll also change the first query from c a to m i. The loader and helper will stay the same.

Before running, predict all three output lines. Track what happens after each returned line, including the blank line and the final repeated word. Decide whether the absence of a final newline changes what the reader returns. Pause here and work out the count and both prefix results.

Let's click Run and compare your prediction with the actual dictionary load.

The count is four. Map, moss, mud, and mint are distinct; the blank line adds nothing and repeated map adds no member. Final map is still returned without a following newline. Only the next read returns null. Mint supplies the successful m i match, while z z matches none.

You used a buffered reader and a progress step to process the whole file, automatic cleanup to finish the read, and a set to retain unique exact words. The helper then answered whether any of those words began with a requested prefix. These observed results give the game a reusable dictionary behavior; the notebook extends it into an object with separate complete-word and prefix methods.

For a transfer question, suppose a dictionary stores only book. What should a whole-word query for b o report, and what should a prefix query for the same text report? Explain which operation each query needs, then use that distinction as you build your dictionary in the notebook.

## Visual description

[Four designed opening scenes establish buffered line reading and whole-word versus prefix queries, connect reusable loaded data to game questions, show a word-game developer with a five-line file containing cat, cart, a blank line, dog, and cat again, and display the worked-case expected reports with three numbered rules.]

[The real Workspace appears and Main.java opens. The camera follows actual typing of the imports and WordChecks helper. The helper scans stored words and returns true when startsWith succeeds; it returns false only after the loop finishes without a match. The main program creates a temporary dictionary file and an empty HashSet. A BufferedReader reads each line. The loop skips only empty strings, adds other lines without changing their text, and reads the next line every time. The resource block closes the reader before the reports.]

[The pointer clicks the native Run Code button. The terminal reports Words: 3, Prefix ca: true, and Prefix zz: false. The explanation distinguishes the blank line from end of file and repeated cat from a new distinct word.]

[The imports are replaced with the complete prediction-case import set. The file text is edited to map, a blank line, moss, mud, mint, and map again, without a final newline, and the first query becomes mi. A prediction question and pause precede the second native Run Code click. The terminal reports Words: 4, Prefix mi: true, and Prefix zz: false. The closing connects read progress, close, unique exact membership, and separate prefix queries, then asks how whole-word bo and prefix bo differ when the only stored word is book.]
