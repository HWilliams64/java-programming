# Transcript: Buffered Files and Prefix Queries

This CSC-239 demonstration uses Java 21 in the Workspace. It prepares a small dictionary file using the familiar writeString helper, reads its lines with BufferedReader, a reader that supplies one line of text at a time, and checks whether a fragment begins any stored word. Both text operations use UTF-8. The program creates a new temporary practice directory each time it runs. Its file remains there when the program ends.

Gray labels beside some method arguments are editor hints for parameter names. They are not extra source text. The complete source below preserves exactly what the program runs.

## 0:00–0:22 — Goal

**On screen:** The title reads Buffered Files and Prefix Queries with the subtitle Load unique words and check a fragment. Main.java is empty while the goal is introduced. A brief editor suggestion is visible above the empty area. No result is shown.

We will load a small dictionary one line at a time, then ask whether a fragment begins any stored word. This supports a Ghost turn without requiring a complete word. The familiar writeString call prepares our practice file before reading begins.

## 0:22–1:19 — Check a prefix

**On screen:** The source is visibly typed into Main.java. The complete forty-line program is visible, and WordChecks with its hasPrefix method is selected for the prefix explanation. The bottom captions are below all source lines. The method tests startsWith and returns immediately for a match, or false after the loop.

The complete source is:

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.charset.StandardCharsets;
import java.io.IOException;
import java.io.BufferedReader;
import java.util.HashSet;
class WordChecks {
    public static boolean hasPrefix(HashSet<String> words, String prefix) {
        for (String word : words) {
            if (word.startsWith(prefix)) {
                return true;
            }
        }
        return false;
    }
}
public class Main {
    public static void main(String[] args) {
        try {
            Path directory = Files.createTempDirectory("csc239-words-");
            Path file = directory.resolve("words.txt");
            Files.writeString(file, "cat\ncart\n\ndog\ncat\n", StandardCharsets.UTF_8);
            HashSet<String> words = new HashSet<String>();
            try (BufferedReader reader = Files.newBufferedReader(file, StandardCharsets.UTF_8)) {
                String line = reader.readLine();
                while (line != null) {
                    if (line.length() > 0) {
                        words.add(line);
                    }
                    line = reader.readLine();
                }
            }
            System.out.println("Words: " + words.size());
            System.out.println("Prefix ca: " + WordChecks.hasPrefix(words, "ca"));
            System.out.println("Prefix zz: " + WordChecks.hasPrefix(words, "zz"));
        } catch (IOException problem) {
            System.out.println("File problem: " + problem.getMessage());
        }
    }
}
```

A prefix is a sequence at the start of a String. The hasPrefix method checks each stored word with startsWith and returns as soon as one matches. If no word matches, it returns false. A contains check would instead look for a complete stored value.

## 1:19–1:47 — Read dictionary lines

**On screen:** The complete source remains visible. The inner try-with-resources statement, first readLine call, loop condition, blank-line check, set insertion and next read are selected. The caption stays below the source. The editor draws the two characters != as a joined not-equal symbol; the complete source in this transcript uses the actual Java characters.

A character stream supplies decoded text characters over time. BufferedReader holds groups in memory to reduce repeated small file operations. readLine returns the next line without its ending. A blank line produces an empty String. Null marks end of file when no characters remain. The loop reads before its condition and again at the end. The length check skips blank lines. HashSet keeps unique words, and try with resources closes the reader.

## 1:47–1:57 — Predict the result

**On screen:** The selection clears and the complete source remains visible. The caption asks for the word count and both prefix results. A three-second pause follows with no terminal output. The file text includes a blank line and repeated cat for the learner to trace.

Predict the word count and both prefix results. Trace the blank line and repeated word carefully. Pause here.

## 1:57–2:16 — Run and interpret the result

**On screen:** The terminal opens and the view enlarges the actual command and its three output lines. At the beginning, the upper caption overlaps parts of the imports and hasPrefix declaration, while the prefix loop and reader body remain visible. The lower print statements initially fall below the editor divider. As the view moves toward the query statements, those statements become visible and selected; the upper caption briefly overlaps part of the file setup and reader declaration. The complete source is available in the earlier model and prediction views. The command and all three terminal outputs stay unobscured. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Words: 3
Prefix ca: true
Prefix zz: false
```

The dictionary contains three unique words. The repeated cat adds no second entry, and the blank line adds nothing. The prefix c a matches the start of cat and cart. No stored word starts with z z. A prefix can match without being a complete stored word.

## 2:16–2:32 — Try a query change

**On screen:** The view returns to the wider Workspace framing with the reader and the three print statements visible above the terminal. The print statements are selected. Bottom captions ask the learner to change only the first queried prefix from ca to cats, predict its result and the word count, then run again. The video makes no such edit and leaves the original output visible. The final hold shows these same statements and output after the captions end.

Change only the first queried prefix from c a to c a t s. Predict that result and whether the word count changes, then run again. What evidence separates a prefix query from changing the dictionary?

