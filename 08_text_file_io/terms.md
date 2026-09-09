**File system** - The organization of stored files and directories. A file system lets an operation locate data by a path. Describing a location does not establish that a file exists there.

**Directory** - A container for entries such as files and other directories. A practice directory keeps one example’s files separate. Creating the directory does not also create every child file named later.

**File path** - A value describing a location in a file system. Java uses a `Path`, such as `Path.of("roster.txt")`, to represent that location. A path is separate from any contents stored there.

**Path** - The Java library type that represents a file-system path. Methods such as `getFileName()` inspect the path value; `resolve("roster.txt")` produces a child path. These operations do not create or read the file itself.

**import** - A Java keyword that lets source code use a type’s short name. After `import java.nio.file.Path;`, code can write `Path` instead of its fully qualified name. An import does not create a Path object or perform a file operation.

**Relative path** - A path interpreted using a base location, such as the current working directory. `Path.of("roster.txt")` is relative and reports `false` from `isAbsolute()`. The path form does not indicate whether its file exists.

**Absolute path** - A path with its starting location specified. On this system, an absolute path starts from `/`. It removes the need to infer a relative starting point but does not guarantee that a later file operation succeeds.

**Temporary practice directory** - A newly created directory used for an example’s controlled starting state. `Files.createTempDirectory("csc239-start-")` returns its Path and generates a distinct location. Java does not automatically delete the directory when the cell finishes.

**Fixture** - Controlled data or state used by a demonstration or test. A new directory containing a known text file is a fixture. A repeatable fixture gives a known starting point without requiring earlier kernel variables.

**Path resolution** - Combining a base path with a child path. `directory.resolve("notes.txt")` returns the path for that fixed relative child inside the directory. It does not create notes.txt, and this pattern alone is not validation for an untrusted name.

**I/O** - Input/output: communication with a source or destination of data. Reading text from a file is input; writing text to it is output. Printing to the console and writing a file use different destinations.

**IOException** - A checked Java exception type used to report an input/output failure. A file operation may throw it instead of returning its normal result. A handler should report the problem rather than silently treating it as successful empty output.

**try** - A Java keyword introducing a block whose failures may be handled by following catch blocks. In a file example, normal operations proceed in order until completion or a thrown exception. After a failure, remaining statements in that block are skipped.

**catch** - A Java keyword introducing a handler for a matching exception type. `catch (IOException problem)` gives the handler access to the actual exception object. Finishing the handler does not resume the failed file operation.

**Character encoding** - A rule for converting text to stored bytes and decoding those bytes back to text. Matching rules on both sides support an exact text round trip. String length is not a general measurement of encoded file size.

**Byte** - A small unit of stored data. UTF-8 encodes text as bytes; some characters need more than one byte. A count of visible characters or Java String positions can differ from the number of file bytes.

**UTF-8** - The character encoding used for this module’s text files. Passing `StandardCharsets.UTF_8` to both `Files.writeString` and `Files.readString` gives them the same rule. The rule preserves text only when reading uses the encoding that actually wrote the bytes.

**Library constant** - A named value a library provides for reuse. `StandardCharsets.UTF_8` chooses an encoding; `StandardOpenOption.APPEND` chooses a write option. These names are library members, not Java keywords.

**UTF-16 code unit** - One storage position counted by a Java String’s `length()`. Each plain English letter and each newline in `"Maya\n"` occupies one position, giving a count of five. Some visible symbols occupy more than one position, and UTF-8 byte size is a different measurement.

**Whole-file writing** - Storing a String as the complete contents of a small file. A default `Files.writeString` creates a missing file or replaces existing contents, including removal of old trailing text. It adds no newline beyond those supplied in the String.

**Whole-file reading** - Loading the complete decoded contents of a small file into one String. `Files.readString` retains stored line endings and closes its resource. A very large file can require too much memory for this approach.

**Append mode** - Adding text to the existing end of a file while preserving its earlier contents. `StandardOpenOption.APPEND` selects this mode; our programs create the file with a normal write first. Appending an empty String adds nothing, whereas a normal write of an empty String replaces all contents.

**Character stream** - A source or destination that supplies or accepts text characters over time. A file reader supplies decoded text; a file writer accepts text for encoding and storage. A sequence of character operations does not mean that each request causes a separate underlying file operation.

**Reader** - An object that provides text characters from an input source. A BufferedReader can return a file’s successive lines. Reading a line does not change the saved file, and the text still depends on the encoding used to decode it.

**Writer** - An object that accepts text characters for an output destination. A BufferedWriter can accept one word and then a line separator. Accepting text does not promise that every character is immediately visible to another reader.

**Buffering** - Holding a group of data in memory to reduce small underlying input/output operations. A reader may read ahead; a writer may retain pending output. The examples verify recovered text without promising an exact buffer size or count of file operations.

**Buffer** - A temporary holding area for data. A text writer may keep recently supplied characters in its buffer before sending them onward. A successful close sends remaining output onward; a buffer is not permanent storage or a replacement for the file.

**Buffered text writer** - A writer that collects character output before sending it to its destination. Java’s `BufferedWriter` type supports `write`, `newLine`, and `close`. It may retain pending output, so finish its resource block before reading the completed file.

**Files.newBufferedWriter** - A Java library method that opens or creates a file and returns a BufferedWriter. `Files.newBufferedWriter(file, StandardCharsets.UTF_8)` selects the location and encoding. With no additional option it replaces existing contents; this factory call is not a Java keyword.

**write** - A writer method that supplies exactly the requested text. `writer.write("cat")` supplies three letters. It does not add a newline automatically, and buffered text may remain pending until it is sent onward.

**newLine** - A BufferedWriter method that supplies the platform’s line separator. Calling `writer.newLine()` after `writer.write("cat")` ends that line. Calling it twice creates a blank line between later text; the separator can use different characters on different platforms.

**Line separator** - The character or characters that end a line of text. A Linux newline is one separator; other platforms can use another form. `readLine()` returns the line’s text without these ending characters, so a returned empty String can represent a real blank line.

**Try-with-resources** - A Java try form that declares a resource in parentheses and automatically closes it when control leaves the block. A BufferedWriter in `try (...)` closes before the following read when their blocks are ordered that way. Automatic closure does not mean that opening, reading, writing, or closing cannot fail.

**close** - A resource operation that finishes its use. A successful BufferedWriter close sends any remaining buffered output onward and closes the resource. The example relies on this order before reading; a close failure is still an I/O failure and can reach a handler.

**Buffered line reader** - A reader that returns each line’s text without its line-ending characters. Java’s `BufferedReader` type supplies `readLine()`. It distinguishes a real blank line from end of file and must still be closed after use.

**Files.newBufferedReader** - A Java library method that opens a file and returns a BufferedReader using the chosen encoding. `Files.newBufferedReader(file, StandardCharsets.UTF_8)` decodes the bytes as UTF-8. A failed open throws an exception instead of supplying an empty dictionary.

**readLine** - A BufferedReader method that requests the next line’s text. It returns an empty String for a real blank line and returns final text even without a trailing separator. A later read returns null when no further line is available; an I/O failure instead throws.

**End of file** - The condition in which no further input remains, also called EOF. `readLine()` reports it with null when no characters were read for another line. A blank String and final text without a newline are still line values, so neither should be used as the loop’s end test.

**null** - Java’s literal for the absence of an object reference. After `readLine()` reaches EOF, `line` receives null and `line != null` is false. An empty String is an existing object with zero-length text, not null; calling a String method on null is invalid.

**while** - A Java keyword that repeats a block while its condition is true. In `while (line != null)`, each available line enters the body. The next read must update line on every body execution; otherwise the same non-null value can be processed repeatedly.

**!=** - Java’s not-equal operator. The test `line != null` checks that a line reference exists before using its text. This null test does not ask whether the String is empty or whether two Strings have different contents.

**Dictionary loading rule** - The chosen rule for turning file lines into stored entries. This tutorial keeps every nonempty line exactly as written and places it in a set. Other dictionary formats may specify different treatment of spaces or case; changing them silently would change the data contract.

**Unique membership** - A set’s property of keeping equal values as one member. Adding `cat` twice to a HashSet leaves one cat member. The set’s size therefore counts retained distinct words rather than input lines, and it does not establish a traversal order.

**if** - A Java keyword that runs a block only when its condition is true. The loader uses `if (line.length() > 0)` to decide whether to add a line. This addition decision belongs inside the null-guarded reading loop and must not prevent the next read.

**Exact-text matching** - Comparing text while preserving its actual characters, including letter case and spaces. `cat`, `Cat`, and ` cat ` are different dictionary entries under this lesson’s rule. A String of spaces is nonempty; skipping empty lines does not automatically trim or normalize other text.

**Complete-word membership** - A query asking whether an exact String is a stored dictionary member. A set containing only `cart` reports true for `contains("cart")` and false for `contains("ca")`. Finding the requested text at the beginning of a longer word is a different query.

**Prefix match** - A check that a String begins with a specified sequence of characters. `"cart".startsWith("ca")` is true, but `"cart".startsWith("ar")` is false because ar does not begin at index zero. Matching a prefix does not mean the prefix itself is a complete stored word.

**startsWith** - A String method that returns whether its text begins with the supplied prefix. It accepts the whole word as its own prefix and accepts the empty String. The dictionary helper must still find a stored word to test; an empty dictionary supplies none.

**Empty prefix** - A prefix containing no characters, written as `""`. Every String starts with it because it places no restriction on the starting characters. A hasPrefix search over an empty set still returns false because no stored word can satisfy the search.

**for** - A Java keyword used for loops. In `for (String word : words)`, the enhanced loop visits the set’s members; an indexed for loop can control separators between array entries. A HashSet loop does not promise a particular visitation order.

**return** - A Java keyword that ends the current method call, optionally supplying its result. The prefix helper returns true as soon as a word matches. Its false return belongs after the loop, so an early nonmatch does not hide a possible later match.

**throws** - A Java keyword used in a method or constructor declaration to identify exceptions that may reach the caller. `PrefixBook(Path file) throws IOException` allows a failed load to be handled by the caller. It does not handle the failure or turn it into a successful empty dictionary.

**File existence and type check** - An observation of whether a path currently exists or names a particular kind of entry. The notebook separately calls these a file existence check and a file type check. `Files.exists(source)` and `Files.isRegularFile(moved)` return Boolean observations; true cannot guarantee a later operation succeeds, and false can also mean the answer could not be determined.

**Regular file** - An entry that stores ordinary file data, unlike a directory that groups entries. `Files.isRegularFile(file)` asks whether the path currently names this kind of file. It is a type observation, not a promise that a later read will succeed.

**File copy** - Creating a separate destination with the source data while retaining the source. `Files.copy(source, copy)` leaves the original available and creates the other file after successful completion. Later changes to one file do not automatically update the other; the default operation can fail if its destination already exists.

**File move** - Changing where an existing entry is found, including renaming it within one directory. After `Files.move(copy, moved)` succeeds in the exercise, the old copy path no longer names that file. The separate original source remains; moving the copy does not move the source.

**File deletion** - Removing a file entry or an empty directory entry. The exercise deletes its known child files before their directory. These calls are not recursive cleanup, and a failure earlier in a try block can skip later normal-path deletions.

**deleteIfExists** - A Files library method that removes the named entry when present. It returns true when it removed the entry and false when the entry was already absent. Repeating deletion can therefore return true then false; other I/O failures still throw exceptions.

**File metadata** - Information about a file apart from its text contents, such as byte size and recorded modification time. It can help inspect saved data, but two different texts can share the same size or recorded time. Metadata equality alone does not establish text equality.

**Files.size** - A library method returning a file’s byte size as a long. `Files.size(file)` measures stored bytes, while String length counts UTF-16 code units. For UTF-8, café occupies five bytes even though that example String has length four.

**long** - Java’s primitive whole-number type with a larger range than int; long is a language keyword. `long beforeSize = Files.size(file);` keeps the returned size in its matching type. The number measures bytes here, not decoded characters or a date.

**Files.getLastModifiedTime** - A Files method that obtains a FileTime representing the recorded last-modified time. Calling it before and after a write yields two observations. Successfully obtaining them does not promise that they differ; rapid writes may share one recorded time.

**FileTime** - A library object representing a file-system timestamp, such as a recorded last-modified time. A variable can retain one value obtained from Files.getLastModifiedTime. It is not a Java keyword, and time resolution limits what comparisons can establish about rapid changes.

**Content snapshot** - Text retained from an earlier successful file read for comparison with a later read. The checker constructor stores ready, then a later check compares current text with that saved String. The retained String does not automatically track later file writes.

**Logical negation (!)** - The Java operator that reverses a Boolean value. In `!current.equals(previous)`, equals is true for matching contents and the negation is false, so true means the text differs. This is an operator, not a method or keyword; it does not change either String.

**Comparison baseline** - The saved value used as the reference for a later comparison. The snapshot checker compares before replacing its baseline with the successful new read. Replacing it first would compare the new text with itself, while a failed read must leave the earlier successful baseline intact.

**Polling** - Checking state at separate moments to notice differences between observations. Calling check after each rewrite can observe changes that one later call misses. A false result establishes matching successful reads, not that no write occurred between them; the tutorial creates no automatic timer or watcher.
