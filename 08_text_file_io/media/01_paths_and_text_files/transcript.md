# Transcript: Paths and Text Files

This CSC-239 demonstration uses Java 21 in the Workspace. It writes and reads a small roster using UTF-8, a rule for converting text into small units of stored data called bytes and back. The program creates a new temporary practice directory each time it runs. Its file remains there when the program ends.

Gray labels beside some method arguments are editor hints for parameter names. They are not extra source text. The complete source below preserves exactly what the program runs.

## 0:00–0:22 — Goal

**On screen:** A title card introduces Paths and Text Files. The Workspace then shows an empty Main.java editor while the narration previews saving and reading a roster. No result is shown.

We will save a small roster, add text, and read it back. File I O means file input and output. A path represents a location. Naming a path does not create a file. Our practice file will stay inside a newly created directory, or folder.

## 0:22–1:04 — Locate the practice file

**On screen:** The complete 20-line source is typed into Main.java. Lines 9 and 10 are selected: creating the temporary directory and resolving roster.txt inside it. All source lines remain visible. The lower caption stays below the code.

The complete source is:

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.StandardOpenOption;
import java.nio.charset.StandardCharsets;
import java.io.IOException;
public class Main {
    public static void main(String[] args) {
        try {
            Path directory = Files.createTempDirectory("csc239-text-");
            Path roster = directory.resolve("roster.txt");
            Files.writeString(roster, "Maya\nLuis\n", StandardCharsets.UTF_8);
            Files.writeString(roster, "Nora\n", StandardCharsets.UTF_8, StandardOpenOption.APPEND);
            String text = Files.readString(roster, StandardCharsets.UTF_8);
            System.out.print(text);
            System.out.println("Characters: " + text.length());
        } catch (IOException problem) {
            System.out.println("File problem: " + problem.getMessage());
        }
    }
}
```

An absolute path starts from the file system root. A relative path needs a base. Here, resolve combines the new directory with the relative name roster dot text. The temporary directory is a distinct practice location. It is not automatically deleted when this program ends.

## 1:04–1:30 — Write and read text

**On screen:** Lines 11 through 17 are selected while the narration explains the two writeString calls, explicit UTF-8, readString, output, and the IOException catch. The complete source is readable, including the APPEND option at the end of the second write.

Character encoding is the rule for turning text into stored bytes and back. Both directions use UTF eight. By default, writeString creates a file or replaces existing contents. APPEND adds text to an existing file. These calls do not add newlines. The strings supply them. readString brings the whole small file into a String. These helpers close their own resources. The catch handles an input or output failure.

## 1:30–1:41 — Predict the result

**On screen:** The selection clears and the complete source remains visible. The learner is asked to predict every output line and count the newlines. A three-second pause follows. The program has not run and no result is visible yet.

Predict every output line, including the character count. Remember to count each newline in the strings. Pause here.

## 1:41–1:59 — Run and interpret the result

**On screen:** The terminal opens and shows javac Main.java && java Main, followed by Maya, Luis, Nora, and Characters: 15 on four lines. All four output lines remain clear. The terminal-focused zoom crops the first imports at the top; its upper caption briefly overlaps the remaining imports and the Main and main headings. The path operations, write/read statements, catch, and complete terminal output stay readable. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Maya
Luis
Nora
Characters: 15
```

The output shows Maya, Luis, and Nora on separate lines, then fifteen characters. Each name has four characters, and each newline adds one. The appended text followed the existing text. String length is not a general measure of stored file size.

## 2:00–2:17 — Try a writing change

**On screen:** The view returns to the complete source with both writeString calls selected. The successful output remains below. The learner is asked to remove the APPEND option from the second write and predict the effect. This change is not performed in the recording. The final hold keeps the selected statements and actual result visible.

Remove only the APPEND option from the second write, keeping the file path, text, and encoding. Predict the new file contents and character count, then run the program. What does this reveal about writing again to an existing file?

