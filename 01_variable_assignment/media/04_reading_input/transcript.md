# Reading Input

## Narration

Welcome to this Java tutorial on reading input, where you'll create a text reader, choose line and numeric methods, trace each read, and use the returned values to calculate and display a result.

Reading input lets the same program work with changing information, such as names, order quantities, and measurements. A clear input format helps software interpret each piece correctly, so a calculation can use numbers instead of simply joining their text characters.

A campus workshop needs receipts for supply kits. Each record gives an attendee's name, a whole-number kit quantity, and a price in dollars per kit, in that order. We'll use complete records with dot-decimal prices, such as one point five. The program calculates a cost; it doesn't take payment.

Our goal is one receipt line containing the attendee's name and the amount owed. We'll supply repeatable text inside the program, so this demonstration won't wait for anyone to type an order. First we'll work through a practice record, then you'll predict a different receipt.

Let's open Main.java in the Workspace and give the workshop program a place to read and process its record.

Scanner is Java's ready-made text reader. An import lets this file use the short class name, Scanner; it doesn't create a reader or read any data. We'll put the import above Main, the class that holds our program. Its main method is where execution starts.

The structure is ready. A reader needs an input source, the place its data comes from. Our practice source gives Nora four kits at one dollar and fifty cents each. It also includes two spaces before and after her name, so we can check the cleanup you learned earlier.

The keyword new creates a Scanner connected to that String. The newline escapes are source notation for line breaks, so the reader receives three separate lines, not backslashes and letters. It starts before Nora's name. Let's read that whole name line and store its cleaned text for the receipt.

NextLine returns the name without the line ending, but keeps the outside spaces. Trim then operates on that returned String, and buyer stores Nora without those spaces. The reader has moved to the quantity. For a kit count, we need an integer. Parsing turns text into a typed value. We'll parse the next token: the piece of text between whitespace separators such as spaces and line endings.

NextInt turns the quantity text into the integer four and stops before its following newline. The price read will skip that whitespace and parse the next token as a double. NextInt cannot parse a decimal token such as one point five; a double receiving variable would not change that method's job.

ItemPrice now holds the numeric value one point five. We can multiply four kits by one dollar and fifty cents per kit to get six dollars. Let's store that cost, join it with Nora's cleaned name and the word owes, and complete the program structure.

The practice program now reads, cleans, calculates, and prints. Let's click Run to check the receipt made from those returned values.

The receipt says Nora owes six point zero. The name has no outside padding because we stored the trimmed result. The amount comes from multiplying the two parsed numbers. Each read continued from the reader's current position; none of them started the source again.

That reader position also explains a common surprise. Let's replace the receipt instructions with a small record that puts a count of three before the name Maya. We'll read the number first and inspect what the following line reads return.

The numeric read takes three, but leaves the reader before that line's ending. A line read now takes the remaining text on this same line, which is empty in this source, and moves past the ending. A second line read can then take Maya from the following line. We'll store both results so we can compare them.

Remainder holds empty text, and name holds Maya. Empty text is hard to see by itself, so we'll print square brackets around remainder. We'll also print the count and name on separate lines to make the reading order visible.

Let's click Run and check the three stored results. The brackets will help us recognize the empty line remainder.

We see three, an empty pair of brackets, and Maya. The first line call consumed only the empty remainder and its line ending. The next one reached the name. If text had followed the number on its line, that first call would return that text instead. Choose reads from the actual source layout; don't add an extra line read automatically.

With the read order explained, let's return to the workshop receipt. We'll replace this small check with the workshop record: Maya requests three kits at four dollars and fifty cents per kit. Her name has no outside padding, so this version stores the line directly. A newly created reader starts at the beginning of this record.

Customer receives Maya, and the reader passes the name line's ending. Quantity comes next, followed by price. Let's use the integer and double reads in that order, matching each value to its intended type.

The numeric calls turn the quantity and price text into values the calculation can use. The price read skips the newline left after the count. We'll multiply the stored numbers and build one receipt line from the customer name, the words and spaces in owes, and the total.

Before we run Maya's program, write the exact receipt line you expect. Trace the returned name, quantity, and price, then calculate the cost and include the spaces supplied by the output text. Use Nora's worked receipt as a model. Pause here if you'd like more time.

Let's click Run and compare the receipt with your prediction.

The program prints Maya owes thirteen point five. Three kits at four dollars and fifty cents each cost thirteen dollars and fifty cents. The printed double uses one fractional digit here. Compare that name and amount with your prediction. The program used the values returned by the reads to produce the receipt.

These examples didn't wait for typing because their input was already supplied. Java's standard input stream, called System.in, is another possible source; an interactive program can read typed responses from it. Keep the supplied text for this exercise. Running the complete program again creates a fresh reader, while repeating a read on a consumed reader does not restart it.

We've connected input to the workshop's result. The import made the reader's class name available, and new created a reader for the supplied source. Newline escapes organized that text. Matching line and numeric reads advanced through it, while parsing produced usable numbers. Your earlier text and arithmetic skills then assembled the receipt.

Now build the notebook's Luis receipt. Use its exact padded source and variable names, read the name and numbers, and store the cleaned name before making the receipt for five kits at two dollars and fifty cents each. After the first run, predict a change to six kits, test it, and restore five. Explain why each complete run starts a fresh reading.

## Visual description

[Four code-free BHCC opening scenes show a vertical learning agenda, a horizontal text-to-values process, a campus workshop beside its input record, and one central receipt. The Workspace appears after this overview.]

[Main.java is opened and built in short groups while the camera follows the active line. A Scanner reads the supplied Nora record. A whole name line is read and trimmed, numeric tokens become an integer count and a double price, and multiplication calculates the bill. The pointer clicks the actual Run control. The output is Nora owes 6.0.]

[A second program reads the integer 3 before a line read. That line read returns an empty String because the reader remains before the quantity line ending. Brackets make the empty result visible. The pointer clicks Run; three output lines show 3, [], and Maya.]

[The body is replaced with the canonical receipt program below. Students predict the result before the third actual mouse Run click. The output is Maya owes 13.5. The closing connects each input operation to its purpose and directs students to the padded Luis record in the notebook: predict five kits, change to six, run and compare, then restore five.]

## Canonical program

```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner orderInput = new Scanner("Maya\n3\n4.5\n");
        String customer = orderInput.nextLine();
        int quantity = orderInput.nextInt();
        double price = orderInput.nextDouble();
        double orderTotal = quantity * price;
        System.out.println(customer + " owes " + orderTotal);
    }
}
```

## Exact canonical output

```text
Maya owes 13.5
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Concept icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Sources and licenses are retained in production evidence.
