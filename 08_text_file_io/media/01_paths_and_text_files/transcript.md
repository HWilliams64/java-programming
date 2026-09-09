# Paths and Text Files — video transcript

## Narration

Welcome! In this Java tutorial, you'll use file paths to describe locations, write and read text using UTF-8, a rule for representing text as bytes, and append new text while preserving what was already saved.

File paths, matching text encodings, and deliberate write modes let applications save rosters, settings, or word dictionaries that a later run can recover after its variables are gone.

Our club coordinator starts a roster with Maya and Luis, then adds Nora. We'll give this run its own practice directory and save one name per line, including a newline after the final name.

Success means reading the saved file back and seeing all three names in order. We'll also inspect the recovered String's length, counting the stored newlines along with these letters. That count measures the String, not a general file byte size.

Now that we're in the Workspace, let's open Main.java.

The file is open. We'll begin with the library types used for paths, file operations, encoding, the append option, and a checked I/O failure. These imports let the program use each type's short name.

Path represents a location. Files supplies operations that create, write, and read. StandardCharsets and StandardOpenOption provide named choices for those operations; IOException gives our handler a specific failure type.

Let's put the operations in the Main class and its main method, the entry point for this Java application. A try block will keep the attempted file work together before its matching handler.

This structure holds the same operations as the notebook. If an I/O operation fails, control will leave the remaining normal work and enter the handler. First, we need a separate location so this demonstration does not reuse an earlier roster.

Creating the temporary directory actually makes a new directory and returns its path. Resolving roster dot text then builds a child path inside it; that second line does not create the file. The generated parent name can change on every complete run. Temporary also does not mean the directory disappears when this program ends.

With the location ready, we'll store Maya and Luis as the starting contents. Each name includes a newline. We choose UTF-8 explicitly so the later read will use the same rule for recovering the text.

This normal write creates the missing roster file. If the file already existed, the same kind of write would replace its complete contents. It adds no line breaks beyond the newlines supplied in the String. The path identifies where to write; the String supplies what to store.

Nora arrives after the starting roster is saved. Replacing the file now would lose Maya and Luis, so the next write will select append mode and add Nora at the existing end.

The append option preserves the first two names and adds Nora with her newline. This option alone expects the file to exist, which is why the normal first write came earlier. All three names now have their own line ending. To inspect what was actually saved, we'll read from the file instead of printing a separate expected roster.

Reading with UTF-8 produces the recovered String, including its line endings. Print displays those stored characters. The following length report counts positions in that String. For these names, each letter and newline occupies one position. These whole-file helpers close the file resources they use; a much larger file may call for the line-by-line approach taught next.

Let's finish the failure handler. It will report the actual exception message, so a failed operation cannot look like a successful read of an empty roster.

The completed normal path creates a location, saves two names, appends one, and reads them back. Each of our three names has four letters; each also has one stored newline. Let's click Run and check both the recovered text and the count.

The read-back shows Maya, Luis, and Nora in order. Twelve letters plus three newlines give the reported length of fifteen. The final stored newline places Characters on its own line. We see normal output instead of a failure report, and the recovered text shows that append preserved the earlier names.

Now apply those same rules to a different roster. We'll change the first written text to Iris and Bo, then change the appended name to Eli. The operations and newline rule will stay the same.

Before running, predict every output line and the number after Characters. Follow the first write, the append, and the stored newline after each name. Pause here and work out the complete recovered String before you compare it with execution.

Let's click Run and compare your prediction with the actual saved-and-recovered text.

Iris, Bo, and Eli appear on their separate lines, followed by a length of twelve. The names and their newlines contribute five, three, and four positions. This complete run created a new directory before writing, so it did not append Eli to the earlier run's roster.

You used a path to identify a location, matching UTF-8 operations to store and recover text, and append to keep earlier contents while adding more. The observed results connect those operations to the coordinator's saved roster. In the notebook, you'll also compare the complete recovered String with the intended text, including every newline.

For a transfer question, imagine that the coordinator needs to correct the entire roster rather than add a new arrival. Which write behavior should you choose, and what exact read-back test would show that the correction replaced the old contents? Use that distinction as you begin the notebook practice.

## Visual description

[Four designed opening scenes establish file paths, UTF-8 and append; connect a saved record to a later program run; show a club coordinator with Maya and Luis plus arriving Nora; and describe the complete recovered roster and stored newline rule.]

[The real Workspace appears and Main.java opens. The camera follows actual typing of the library imports, Main class and main entry method, and try block. The program creates a new temporary directory, resolves roster.txt, writes Maya and Luis with UTF-8, appends Nora, then reads the text back with UTF-8. It prints the recovered names and the String length. An IOException handler reports a file problem.]

[The pointer clicks the native Run Code button. The terminal shows Maya, Luis, Nora, and Characters: 15 on separate lines. The explanation counts twelve letters and three stored newlines.]

[The first write is edited to Iris and Bo and the append is edited to Eli. A prediction prompt and pause precede the second native Run Code click. The terminal shows Iris, Bo, Eli, and Characters: 12. The explanation counts five, three and four String positions including the newlines and notes that the complete run created its own new directory. The closing connects paths, matching encoding and append to recovery, then asks which write behavior should correct the complete roster and what read-back test would confirm the replacement.]
