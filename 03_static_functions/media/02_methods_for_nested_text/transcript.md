# Methods for Nested Text

## Narration

Welcome to this Java tutorial, where you'll use String positions and ranges, track nested delimiters—paired boundary symbols—and write a method that returns the right section of text.

These text-processing skills help applications extract usable information from notes and files, while a clear method contract—the rules for accepted inputs and returned results—lets other code interpret the result and test difficult inputs.

A workshop coordinator stores color notes inside square brackets. Some notes contain another bracketed section, which must stay in the selected text. We'll build a helper that reads the note one position at a time, counts openings that still need a close, and selects the inside of the first completed outer pair.

The caller should receive the entire marked section with only its outer brackets removed. Later groups won't be included. An empty pair or a note with no completed pair will produce an empty String. We'll learn the position rules first, then build and test that selection method.

Now that we're in the Workspace, let's open Main.java and try the two String operations our helper will need.

Main is the class holding our program, and its main method is where the application starts. We'll put a short marked word there. String positions start at zero: in this six-character input, the opening bracket is at zero and the closing bracket is at five.

To recognize a boundary, the scan needs one character rather than a whole String. The charAt method selects the value at a position. We'll select position zero and store it in a char variable named symbol. Single quotes write a character literal; double quotes write a String.

Symbol contains the opening bracket, so its character comparison should be true. Equality compares these char values; it isn't a replacement for equals when comparing String content. Next we need the text between two positions. Substring includes its start and excludes its end, so the range from one to five selects the four letters of blue.

The second substring call has equal boundaries. No position belongs to that range, so it returns an empty String. The labels and angle brackets come from the caller and make both results visible. Let's click Run and compare them.

The output shows the bracket, true, the selected word, and an empty labeled result. Neither operation changed the source String. These ordinary letters and brackets each occupy one position; Java actually counts UTF-sixteen code units, so some displayed symbols need more than one position. We'll stay with these simple characters while we build the delimiter scan.

We can select a range now, but a nested note has more than one closing bracket. Stopping at the first close would cut the outer section short. Let's replace the small trial with TextTools, a class containing our reusable selection method. It accepts a String, including empty text, and returns a String to its caller. We won't pass null, the value that means no String object was supplied.

Start remembers where the outer group's content begins. Minus one means that we haven't found an opening yet. Depth counts openings that still need closing brackets. We'll move through valid positions, starting at zero and stopping before the String length, selecting one char at each position.

At an opening bracket, depth tells us whether this is a new outer group or a smaller group inside it. Only an opening seen at depth zero should record a new start. We store the next position so the eventual substring leaves that outer bracket out.

Every opening increases depth, but an inner opening leaves start alone. For the short note with m, an inner bracketed n, and p, start stays one while depth rises from one to two. A closing bracket should count only when an opening is active; that guard also ignores a stray closing bracket before any group begins.

A closing bracket decreases depth. The inner close in our short note changes two to one, so scanning must continue. Only the outer close changes one to zero. At that moment we know both range boundaries: the recorded start and the current closing position, which substring excludes.

This early return finishes the entire method, including its loop. Java won't perform another loop update or scan a later group. But an input might end before any outer group completes. Outside the complete loop, we'll return an empty String for that case.

The helper now has both return paths. It doesn't print or change the original text; display remains the caller's choice. Let's call it with our short nested note so we can trace the result before trying a longer note.

The opening at zero records start one. The inner opening at two raises depth to two, and its close at four lowers depth to one. The close at six finally makes depth zero. The selected positions one through five contain m, the complete inner bracketed n, and p. Let's run that call.

The caller prints m, bracketed n, and p. The inner pair survived because it was inside the selected range. Start stayed at the outer content boundary throughout the scan, and only the outer close allowed the return. Now let's examine the rule for empty or incomplete input before using the helper on the coordinator's longer note.

We'll keep the helper unchanged and replace the caller with four separate tests. The first input has two completed groups; the method should return only the first group's a. An empty pair should return empty immediately. Plain text and an unfinished group should reach the final empty return after the loop.

The same selection rule is in place. Each test now needs its own call, and each caller will print angle brackets around the result. This makes an empty return visible without pretending that the helper printed anything itself.

Let's run the four calls in their displayed order: two groups, an empty group, no group, and an unfinished group.

Only the first line contains a. That early return skipped the later group. The next three lines all contain empty results, but their causes differ: the empty pair completed a zero-length range, while plain text and the unfinished group reached the final return. An empty result alone doesn't tell a caller which cause occurred; that limitation belongs in the method's contract.

The boundary checks match the stated rules. We'll keep the helper and replace those four calls with the coordinator's longer color note. This time, use the depth rule yourself before running it.

The helper is unchanged. The new input contains an outer color section with an inner bracketed color. The caller will print exactly the String returned by the method, with no extra labels.

Pause here and predict the printed text. Which opening records start, and which closing bracket first brings depth back to zero? Decide which brackets belong inside the selected range before you continue.

Let's click Run and compare your prediction with the actual result.

The output is red, bracketed blue, then green. The outer opening records start at six. The inner pair raises depth to two and lowers it to one, so it doesn't end the selection. The outer close at twenty brings depth to zero, and the range from six to twenty keeps the inner brackets while excluding the outer pair.

We built a reusable method that extracts the coordinator's complete marked section. String positions let us inspect characters, the depth counter identified the matching outer boundary, substring selected the range, and early return stopped work once the answer was known. The caller handled output, while boundary tests made the empty-result rule explicit.

For a transfer check, imagine that the notes use parentheses instead of square brackets. Which comparisons would change, and which parts of the range and depth logic would stay the same? Explain how you would test both a nested section and an unfinished one.

## Visual description

[Four code-free BHCC opening scenes introduce String positions and ranges, nesting depth, and returned results; connect text selection to application data processing; establish a workshop coordinator's marked notes; and illustrate keeping the contents of the first completed outer bracket pair.]

[In Main.java, the camera follows small typed code blocks. A marked word demonstrates charAt, character literals, and substring ranges. An actual mouse click on Run Code produces an opening bracket, true, Slice: <blue>, and Empty: <>.]

[The trial is replaced with TextTools. Its helper records the outer start, counts nested openings, ignores closes when no opening is active, and returns the selected substring as the first outer group completes. An empty String is returned after the loop when no complete group was found. The worked caller uses [m[n]p]; an actual Run click produces m[n]p, preserving the inner brackets.]

[Only Main is replaced, retaining the helper. Four calls use [a] [b], [], plain, and [open. An actual Run click displays Inside: <a>, followed by three Inside: <> lines. The explanation distinguishes a successfully selected empty range from failure to find a completed group.]

[The final Main uses Note [red[blue]green] end. Students predict the returned text before the fourth actual Run click reveals red[blue]green. The review connects the stored start, nesting depth, exclusive substring end, and early return to the opening task. Students then transfer the selection rules to parentheses in the notebook.]

## Canonical program

```java
class TextTools {
    static String insideOuterBrackets(String text) {
        int start = -1;
        int depth = 0;
        for (int index = 0; index < text.length(); index = index + 1) {
            char symbol = text.charAt(index);
            if (symbol == '[') {
                if (depth == 0) {
                    start = index + 1;
                }
                depth = depth + 1;
            } else if (symbol == ']' && depth > 0) {
                depth = depth - 1;
                if (depth == 0) {
                    return text.substring(start, index);
                }
            }
        }
        return "";
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(TextTools.insideOuterBrackets("Note [red[blue]green] end."));
    }
}
```

## Exact canonical output

```text
red[blue]green
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Concept icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Sources, licenses and original hashes are retained in production evidence.
