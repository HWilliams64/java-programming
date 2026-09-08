**File path** - A representation of a location in a file system; it does not prove that a file exists.
**Relative path** - A path interpreted from a base location, such as the current working directory.
**Absolute path** - A path that includes its starting location.
**Path resolution** - Combining a directory path with a relative child path or interpreting a path against its base.
**Temporary practice directory** - A new directory used for one example’s controlled file data; it still needs explicit cleanup.
**Fixture** - Controlled starting data for a demonstration or test.
**I/O** - Input/output: receiving data from a source or sending it to a destination.
**IOException** - A checked exception used by file operations to report an input/output problem.
**Character encoding** - A rule for converting text into stored bytes and converting those bytes back into text.
**Byte** - A small unit of stored data used when text is encoded in a file.
**Library constant** - A named value a library provides for reuse.
**Whole-file writing** - Writing a String as file contents; the default operation replaces existing contents.
**Whole-file reading** - Loading all text from a small file into one String.
**Append mode** - Adding text after a file’s existing contents instead of replacing them.
**Character stream** - A source or destination that supplies or accepts decoded text characters over time.
**Buffering** - Holding a group of data in memory to reduce small underlying input/output operations.
**Buffered text writer** - A writer that collects character output before sending it to its destination.
**Buffered line reader** - A reader that returns each line’s text without its line-ending characters.
**End of file** - The condition in which no further input remains; readLine reports it with null.
**Prefix match** - A check that a String begins with a specified sequence of characters.
**File existence and type check** - An observation of whether a path currently exists or currently names a regular file.
**File copy** - Creating another file with the source data while retaining the original.
**File move** - Relocating or renaming a file so its old path no longer names it after success.
**File deletion** - Removing a file or an empty directory entry.
**File metadata** - Information about a file, such as its stored byte size or last-modified time, apart from its contents.
**long** - A primitive whole-number type with a larger range than int; Files.size returns its byte count in this type.
**FileTime** - An object representing a file timestamp, such as its recorded last-modified time.
**Content snapshot** - A retained read of a file’s contents used as a comparison baseline.
**Polling** - Checking state at separate moments to notice differences between observations.
