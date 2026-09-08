# Transcript: File Operations and Change Checks

This CSC-239 demonstration uses Java 21 in the Workspace. It copies, moves, checks, and deletes files created in a new practice directory. It also compares two saved reads of a file's text. Every text read and write uses UTF-8. On this successful run, the program explicitly removes its remaining file and then its empty directory.

Gray labels beside some method arguments are editor hints for parameter names. They are not extra source text. The complete source below preserves exactly what the program runs.

## 0:00–0:21 — Goal

**On screen:** The title introduces file operations and change checks. The Workspace then shows an empty Main.java while the goal explains that every file belongs to a new practice directory.

We will manage a small game-state file and compare its text at two moments. Every file belongs to a newly created practice directory. This keeps copying, moving, and deleting focused on files made by this example.

## 0:21–1:34 — Manage file paths

**On screen:** The program is typed into Main.java. The complete 32-line source is visible. Lines 8–17 are selected to show the practice paths, initial write, copy, move, and file checks. The caption sits below the code.

The complete source is:

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.charset.StandardCharsets;
import java.io.IOException;
public class Main {
    public static void main(String[] args) {
        try {
            Path directory = Files.createTempDirectory("csc239-state-");
            Path state = directory.resolve("state.txt");
            Path backup = directory.resolve("backup.txt");
            Path archive = directory.resolve("archive.txt");
            Files.writeString(state, "ready\n", StandardCharsets.UTF_8);
            Files.copy(state, backup);
            Files.move(backup, archive);
            System.out.println("Source exists: " + Files.exists(state));
            System.out.println("Backup exists: " + Files.exists(backup));
            System.out.println("Archive is file: " + Files.isRegularFile(archive));
            String previous = Files.readString(state, StandardCharsets.UTF_8);
            long previousSize = Files.size(state);
            Files.writeString(state, "busy!\n", StandardCharsets.UTF_8);
            String current = Files.readString(state, StandardCharsets.UTF_8);
            System.out.println("Same size: " + (previousSize == Files.size(state)));
            System.out.println("Content changed: " + !current.equals(previous));
            System.out.println("Deleted archive: " + Files.deleteIfExists(archive));
            System.out.println("Deleted again: " + Files.deleteIfExists(archive));
            Files.deleteIfExists(state);
            Files.deleteIfExists(directory);
        } catch (IOException problem) {
            System.out.println("File problem: " + problem.getMessage());
        }
    }
}
```

A copy creates another file while keeping the source. A move changes its location or name. Our destination paths start unused. Existence and regular-file checks describe what the program can observe now. A regular file stores data. A directory groups files. A false check can also mean the status could not be determined. The catch handles input or output failures.

## 1:35–2:02 — Compare snapshots and clean up

**On screen:** The full source remains visible. Lines 18–27 are selected: the first saved text and byte count, a second write and read, comparisons, and deletion. The bottom caption leaves those lines clear. The editor may join the two equals signs in == visually; the source still contains both characters.

Metadata is information about a file, such as its stored byte size. A content snapshot keeps text from one read for later comparison. Here, previous saves the first text and previousSize saves its byte count. After writing again, current saves a second read. Comparing the strings asks whether their text differs. Deleting removes a file. deleteIfExists reports whether it removed one. A directory must be empty before deletion.

## 2:02–2:16 — Predict the result

**On screen:** The selection clears. All 32 source lines remain visible while the learner is asked to predict seven lines. A three-second pause follows before the terminal opens; the answer is not yet shown.

Predict all seven output lines. Track the three file paths, compare the saved text and sizes, then consider both attempts to delete the archive. Pause here.

## 2:16–2:40 — Run and interpret the result

**On screen:** The view moves closer to the terminal, where all seven output lines are readable. A top caption briefly covers parts of the earlier Main, main, and try headings. The first import and final closing brace are outside this closer editor view; earlier views showed the complete source. The file operations, text comparisons, and deletion statements remain visible. The saved-read comparison lines become selected near the end of this explanation. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Source exists: true
Backup exists: false
Archive is file: true
Same size: true
Content changed: true
Deleted archive: true
Deleted again: false
```

The source remains, the backup name disappears after the move, and the archive is a regular file. Both stored texts occupy six bytes in UTF eight, but their contents differ. The first archive deletion succeeds. The second reports that nothing was deleted. Finally, the program removes its state file and the now-empty practice directory.

## 2:40–3:03 — Try a content change

**On screen:** The view widens, showing source lines 1–31 and all seven original output lines. The final closing brace is below the editor divider. The selected lines contain the saved reads, byte-size check, and text comparison. The learner is asked to change only the second written text and predict the results. No change is performed in this recording; the original output remains on screen through the closing pause.

Polling means checking at separate moments. These two reads notice a difference between their snapshots. Change only the second written text back to ready followed by its newline. Predict both comparison results, then run again. Could a change from ready to another value and back entirely between reads escape these checks?

