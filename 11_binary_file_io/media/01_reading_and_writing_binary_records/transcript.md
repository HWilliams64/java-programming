# Transcript: Reading and Writing Binary Records

This CSC-239 demonstration uses Java 21 in the Workspace. A temporary file holds a room record containing a seat count, price and open flag. The recording shows the complete Main.java program and its actual output.

Gray labels beside some method arguments show parameter names. They are editor hints, not extra source. The source below preserves the exact Java characters.

## 0:00–0:18 — Goal

**On screen:** A title card names Reading and Writing Binary Records and emphasizes matching field type, order and meaning. The Workspace then shows an empty Main.java editor while the goal is introduced. No result is shown.

We will save a room record in a temporary file, then recover its seat count, price and open flag. The goal is to make the writer and reader agree on what each stored value means.

## 0:18–1:11 — Write an agreed record

**On screen:** The complete 27-line program is typed and saved. Lines 8–14 select the temporary file path, writer creation and three write calls. All source lines remain readable above the bottom captions.

The complete source is:

```java
import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.nio.file.Files;
import java.nio.file.Path;

public class Main {
    public static void main(String[] args) throws Exception {
        Path file = Files.createTempFile("seat-record-", ".bin");
        try {
            try (DataOutputStream writer = new DataOutputStream(Files.newOutputStream(file))) {
                writer.writeInt(4);
                writer.writeDouble(2.5);
                writer.writeBoolean(true);
            }
            try (DataInputStream reader = new DataInputStream(Files.newInputStream(file))) {
                int seats = reader.readInt();
                double price = reader.readDouble();
                boolean open = reader.readBoolean();
                System.out.println("Seats: " + seats);
                System.out.println("Price: " + price);
                System.out.println("Open: " + open);
            }
        } finally {
            Files.deleteIfExists(file);
        }
    }
}
```

A byte stream moves a sequence of bytes, small units of stored data, without treating them as text. Files opens that byte connection. DataOutputStream adds typed binary output: it writes each value according to its Java type. Our binary record schema is the agreed field types and order: an int count, a double price, then a boolean flag. These writes store values without field names or type labels.

## 1:11–1:44 — Read matching fields and clean up

**On screen:** Lines 15–24 select reader creation, the three reads, print statements and finally deletion. The complete source remains visible as the narration explains matching field order and cleanup.

Typed binary input uses DataInputStream to interpret those bytes. Each read must match the corresponding write in type, order and meaning. Swapping two fields of the same type can silently give them wrong meanings. Try with resources closes each stream, including its file connection. The writer closes before reading begins, and finally removes the temporary file. An incomplete record ends before a required field is fully read. EOFException reports that unexpected end of file. It does not supply a default value.

## 1:44–1:55 — Predict the result

**On screen:** The selection clears and all 27 source lines remain visible. The terminal is closed, and no output has been shown. A three-second pause follows the prediction prompt.

Predict the three printed lines. Match each read to its write, then follow which variable each print uses. Pause here before running.

## 1:55–2:11 — Run and interpret the result

**On screen:** The view moves closer to the terminal. The exact command and all three output lines are readable. The first import and part of the second are above the cropped view. Top captions briefly cover portions of the class and main headers. The path creation, writer and reader operations, print statements and finally deletion remain clear. Earlier and later full-source views show the cropped headers and imports. This complete program is run once. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Seats: 4
Price: 2.5
Open: true
```

The reader recovers four seats, a price of two point five, and true for open. The matching reads interpret the stored values in the agreed order. The streams close and the temporary file is deleted after this complete run.

## 2:11–2:28 — Change and test the record

**On screen:** The wider view restores all 27 source lines and keeps the original output visible. Lines 11–18 select the written values and corresponding reads. The learner is asked to change the price and investigate a missing final flag. Neither edit is performed in the recording. A short hold ends on the unchanged program.

Change only the written price, then predict which printed line changes. Next, remove the final boolean write. Which read would fail, and why should the program report an incomplete record instead of treating the room as closed?

