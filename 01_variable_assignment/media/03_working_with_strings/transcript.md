# Working with Strings

## Narration

Welcome to this Java tutorial on strings, where you'll use named operations called methods to clean and join text, measure its length, and compare its contents while preserving the original entry.

These operations help applications display names consistently, compare search terms, and process records, while keeping the original entry available to explain how a cleaned result was produced.

A campus workshop volunteer needs a greeting built from a participant's name. The supplied name has two ordinary spaces before it and two after it. We'll keep that entry, prepare a version without the outside spaces, and use the cleaned text in the greeting.

The finished program should display the greeting, report the cleaned name's length, and check its contents against an expected spelling. We'll first work through a different practice name so you can predict the final program's three output lines yourself.

Let's open Main.java in the Workspace and build that practice example.

We'll use the familiar starter structure. Main is the class containing our program, and its main method is the named operation where execution begins. The text-processing statements will go inside that method.

Our practice participant is Leo. String, with a capital S, is Java's ready-made class for text. We'll store the entered name with two spaces on each side so the program has an original value to preserve.

Those spaces are inside the quotation marks, so they're part of the stored text. To prepare the name for display, we'll call trim on that text and store its returned result in a separate variable called cleanName. For these ordinary spaces, trim removes only the ones at the boundaries.

Trim is a method, a named operation supplied by String. The empty parentheses mean this call needs no extra input. Its returned text goes into cleanName. Strings are immutable: their existing text doesn't change in place, so enteredName still keeps the spaces. We'll make that difference visible when we print the results.

With a cleaned name available, we can build the greeting. Joining text is called concatenation. Here the plus operators combine a greeting label, the cleaned name, and an exclamation mark. The space after the comma belongs to the first piece; Java doesn't add it for us.

Greeting now holds the combined text, while cleanName still holds the cleaned name. Let's print the original entry between brackets so its boundary spaces are visible, then print the greeting on the next line. The brackets are display markers we add here, not characters stored in the original name.

These two lines will let us compare the preserved input with the new message. We also want a measure of the cleaned name. Calling length returns a whole-number count. For the ordinary English letters in Leo, that count is three. More complex text can use more than one Java text position for a displayed symbol; this example stays with ordinary letters.

The length call inspects cleanName without changing it. To inspect the actual spelling, we'll use equals. This method takes an argument, the value we supply for comparison, and returns true or false. Our practice comparison uses uppercase LEO, which differs from the capitalization of the cleaned name.

Equals compares the text exactly, including letter case, so this practice comparison will be false. We'll close the starter structure, then use the completed program to check the preserved entry, the greeting, the count, and the comparison.

The practice program is complete. Let's click Run and see how the returned text differs from the original entry.

Inside the brackets, Leo still has its original spaces. The greeting uses the cleaned name, and the next line reports three, the cleaned name's length. False tells us that the cleaned spelling doesn't exactly match uppercase LEO. Together, these results show that the methods returned useful information without editing the original text.

Now we can apply that pattern to the workshop's actual participant, Maya. We'll replace the practice statements while keeping the class and main method. The new entry again includes two spaces on each side, and we'll keep the original and cleaned values separate.

The new entry and the call that prepares it are in place. We'll build the greeting from the returned text and display that greeting first. The extra bracketed diagnostic from the practice run isn't part of the workshop's three-line result.

The greeting statement is ready. We'll finish with the same length operation and a content comparison using the spelling shown in this call. Neither check changes the text it inspects.

Before we run this version, write its three output lines in order. Use the practice example to trace the returned trimmed text, the pieces joined into the greeting, the length, and the exact comparison. Pause here if you'd like more time.

Let's click Run to compare your prediction with the workshop program's actual result.

The greeting is Hello, Maya! It has the space supplied after the comma and no extra spaces around the name. Four is the cleaned length. True means the cleaned text exactly matches Maya with the same capitalization. Check those three lines against your prediction. The original enteredName still holds the padded entry, just as it did in our practice example.

We've built the volunteer's greeting and two checks of its cleaned name. Trim returned text we could store, concatenation built a new message, and length and equals reported information about that text. Preserving the entry separately lets us explain how the displayed result was produced. An exact spelling comparison checks text, not a person's identity.

For your next experiment, change only the entered name to lowercase maya, keeping the surrounding spaces. Leave the comparison text unchanged. Which output lines should change, and which should stay the same? Explain your prediction before you run that version.

## Visual description

Four code-free opening scenes show the learning goals as three text-operation strips; a branching text-preparation diagram connects readable names, search terms, and stored records; a workshop entry with two spaces on each side leads to a volunteer's greeting badge while a separate note preserves the entry; a numbered checklist introduces the greeting, length, and exact comparison. The real Workspace appears after these scenes.

Main.java opens in the real editor. The familiar class and main method form the starter structure. Small groups of statements are typed with the view following the active line. The first worked example stores the padded name Leo, stores the result of trim separately, builds a greeting, prints the original entry between brackets, and reports length and equality with uppercase LEO. The actual Run control is clicked, and the terminal shows:

```text
[  Leo  ]
Hello, Leo!
3
false
```

The original spaces are visible between the brackets. The brackets are display markers added by the print statement. The greeting uses the cleaned name. The method calls return results without changing the original text.

The practice statements inside main are replaced with the workshop program below. Learners predict its three output lines before the second actual Run click. The terminal then displays the exact canonical output. The closing connects each operation to the workshop task and asks learners to predict what changes if the supplied name becomes lowercase maya while the comparison stays unchanged.

## Canonical program

```java
public class Main {
    public static void main(String[] args) {
        String enteredName = "  Maya  ";
        String cleanName = enteredName.trim();
        String greeting = "Hello, " + cleanName + "!";
        System.out.println(greeting);
        System.out.println(cleanName.length());
        System.out.println(cleanName.equals("Maya"));
    }
}
```

## Exact canonical output

```text
Hello, Maya!
4
true
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Concept icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Sources and full licenses are retained with the composition.
