**Code cell** - An editable notebook box used for runnable instructions. A Java cell can contain `System.out.println("Hello");`. A text-response cell collects your explanation instead of a program.

**Program** - Instructions that a computer carries out to perform a task. Our notice program displays a welcome followed by an instruction. The computer follows the instructions we supply; it does not decide whether their wording meets the task.

**Statement** - An instruction written in Java source code. `System.out.println("Hello");` is one output statement, including its ending semicolon. In the straight sequences taught here, changing the statement order changes the order of their effects.

**String literal** - Text written directly between double quotation marks, such as `"Hello"`. The quotes mark the text's boundaries in the source; printing this literal displays `Hello` without them. Spaces and punctuation inside those boundaries belong to the text.

**System.out.println** - The name of a Java operation that displays a value and then ends the output line. `System.out.println("Hello");` displays one message, allowing the next message to start on a new line. `println` is a method name, not a reserved Java keyword.

**Syntax** - The rules that determine whether code is correctly formed. A string literal needs its opening and closing quotation marks, and an output statement needs its parentheses and semicolon. Correct syntax does not guarantee that a program displays the message the user requested.

**Console output** - Text a running program sends to its output area. The notebook shows the result below its Java cell. Output is the result of executing instructions, rather than a copy of all the source code and punctuation.

**Tracing** - Following instructions in order and recording their effects. For two output statements, record the message each one adds. Use the current code order, even when a different order would make a better notice.

**Source file** - A text file containing program instructions, such as `Main.java`. Editing it changes the source that will be used on a later run. The file is distinct from the console area that displays the program's results.

**Frame** - In the first lesson, the supplied starter structure around the output statements. Its class, main method, and braces show where those statements belong in `Main.java`. This teaching term does not name a Java keyword or a graphical window.

**Class and `class`** - A class is a named container for related code; the keyword `class` introduces one. In `public class Main`, `Main` is the class name. The first lesson uses this supplied container; designing classes and objects comes later.

**Main method** - The method named `main` that serves as the starting point in the supplied Java application. Its braces contain the two notice statements. Lowercase `main` is different from the class name `Main`, and neither name is a reserved keyword.

**`public`** - A Java keyword that makes the supplied class or method accessible from outside its containing code. It appears in the starter declarations for `Main` and `main`. It controls access, rather than causing a message to print.

**`static`** - A Java keyword that lets the starting method belong to the class rather than requiring a separate object of that class. This lets the supplied `main` method run without creating a `Main` object first. It does not mean that statements or variable values cannot change.

**`void`** - A Java keyword saying that a method does not return a value to its caller. The supplied `main` method uses it and still produces console output. Returning a value and displaying text are different actions.

**Kernel** - The running language process that handles code sent from notebook cells. This course's Java kernel accepts small snippets without the full `Main.java` frame. It can retain variables between cells, so the lessons recreate needed values when a fresh start is required.

**Compilation** - Checking and translating Java source into a form the Java runtime can execute. A missing closing quotation mark can prevent this step from succeeding. Compilation checks code rules; it does not decide whether a notice is useful to its audience.

**Execution** - Carrying out a program's instructions. Executing two `println` statements produces their messages in the shown sequence. An unchanged program can execute again and produce the same result.

**Comment** - A note in source code that Java ignores during execution. In these exercises, `//` begins a comment that continues to the end of its line. A cell containing only a comment gives you a place to write code but does not yet perform the task.

**Debugging** - Finding and correcting a problem in a program. Restoring a missing quotation mark repairs one syntax problem; moving a complete statement can repair a wrong message order. Check the result after a repair rather than assuming that the absence of an error proves success.

**Variable** - A named place for a value used by a program. After `int tickets = 3;`, reading `tickets` supplies the stored count. A variable stores a value, not a permanent formula linking it to other variables.

**Type** - The kind of value a variable can hold and the operations that are allowed on it. For example, a count can use `int` and a true-or-false fact can use `boolean`. Digits inside quotes are text, so `"3"` is different from the number `3`.

**Primitive type** - A built-in Java value type, such as `int`, `double`, or `boolean`. These types represent numbers or other basic values directly. Java's `String` type also comes ready-made, but it is a class rather than a primitive type.

**`int`** - The Java keyword for a primitive type that stores whole numbers. `int tickets = 3;` records a count of three tickets. An `int` cannot directly hold a fractional count such as `3.5`, and its range is finite.

**`double`** - The Java keyword for a primitive floating-point type, used for numbers that may include fractional parts. `double ticketPrice = 4.5;` stores the example's price per ticket. Some decimal values are only approximated, so this type does not promise exact results for arbitrary money calculations.

**`boolean`** - The Java keyword for a primitive type with the values `true` and `false`. `boolean salesOpen = true;` records a yes-or-no fact. The spellings `true` and `false` are Boolean literals, not string values or Java keywords.

**Declaration** - Introducing a variable with its type and name. `int tickets` is the declaration portion of `int tickets = 3;`. Give the type when introducing that variable; a later assignment uses the existing name without repeating its declaration.

**Initialization** - Giving a variable its starting value. In `int tickets = 3;`, the initial value is `3`. Initializing a total performs its calculation at that moment; it does not keep recalculating when an input changes.

**Arithmetic expression** - A calculation that produces a value. `tickets * ticketPrice` multiplies the current count by the current price per ticket. Parentheses can control grouping, and the operand types affect operations such as division.

**Operand** - A value used by an operator, a symbol for an operation. In `5 / 2`, five and two are operands of division. Their types matter: replacing `5` with `5.0` changes the division from integer arithmetic to floating-point arithmetic.

**Assignment** - Evaluating a value on the right of `=` and storing it in the variable on the left. After `tickets = 4;`, later uses of `tickets` read four. Assignment changes the named variable; it does not automatically update a previously stored `total`.

**Operator precedence** - The rules for which operations Java evaluates first within an expression. Multiplication comes before addition in `2 + 3 * 4`, giving `14`; parentheses in `(2 + 3) * 4` make addition happen first, giving `20`. Choose grouping to match the task rather than relying on a left-to-right reading of every symbol.

**Integer division** - Division of integer operands that discards any fractional part toward zero. `5 / 2` produces `2`; assigning that result to a `double` afterward produces `2.0`, not `2.5`. At least one operand must already be floating-point to perform the fractional division shown in the lesson.

**Remainder** - The amount left after integer division, computed with `%` in these examples. Sharing five whole supplies between two tables gives two per table and `5 % 2`, or one, left over. Remainder answers a different question from the quotient given by `/`.

**Floating-point approximation** - Representing some decimal values by nearby values because a floating-point type has limited precision. Java prints `0.30000000000000004` for `0.1 + 0.2`, showing the effect of those approximations. Prices such as `4.5` in the lesson are exactly representable, but that does not make every decimal price exact.

**String** - Java's ready-made class for text values. `String enteredName = "  Maya  ";` stores a reference, a value identifying the text object. That text includes its surrounding spaces. A `String` is not a primitive type, and its existing text cannot be edited in place.

**Object** - A value created from a class that can provide operations associated with that class. A String object provides operations such as `trim()` and `length()`. Using a ready-made object does not require designing a class of your own.

**Method call** - Requesting a named operation and supplying any needed arguments. In `enteredName.trim()`, the dot selects the operation on the text and the empty parentheses mean no extra arguments are supplied. A call that returns text does not necessarily replace the variable you called it on.

**`trim()`** - A String method that returns text with leading and trailing characters at or below ordinary space removed. `"  Maya  ".trim()` produces `"Maya"`, while spaces between words remain. The method does not edit the original String, and it is not a general rule for every spacing character.

**Argument** - A value supplied as input to a method call. In `cleanName.equals("Maya")`, the literal `"Maya"` is the argument to compare with the stored text. The argument supplies a value; it does not name a new variable.

**Return value** - A result produced by a method call for other code to use. In `String cleanName = enteredName.trim();`, the assignment stores the returned text in `cleanName`. Producing a result does not automatically replace the variable before the dot, and returning a value differs from printing it.

**String immutability** - A String object's existing text does not change. Calling `enteredName.trim()` returns cleaned text, which you can store in `cleanName` or assign back to `enteredName`. Discarding that returned value leaves later reads of `enteredName` unchanged.

**Concatenation** - Joining text to build a larger string. `"Hello, " + "Maya" + "!"` produces `Hello, Maya!`; the programmer supplies the space. When text and numbers are mixed, grouping determines whether an addition calculates a number or joins its displayed form to text.

**`length()`** - A String method that returns the number of Java text positions occupied by the value. `"Maya".length()` returns the integer `4`. Some visible symbols use two such positions, so this is not always a count of the symbols a person sees.

**String comparison** - Comparing text contents, using `equals` in these lessons. `"Maya".equals("Maya")` is `true`, while comparing with `"maya"` is `false` because letter case differs. Use `equals` for this job; `==` checks reference identity for String variables and can give misleading results in small literal examples.

**`equals(...)`** - A String method that compares the contents with the supplied argument and returns a Boolean result. `"Maya".equals("maya")` returns `false` because the initial letter case differs. This method checks existing contents; it does not remove spaces or change capitalization.

**Reference** - A value that identifies an object. A String variable holds a reference to its text object; assigning a cleaned result can change which object the variable identifies. Comparing references asks whether they identify the same object, while `equals` asks whether String contents match.

**Character index** - A numbered position used to select part of Java text, starting at zero. In the lesson's name `Maya`, `charAt(0)` gives `M` and `charAt(3)` gives the last `a`. Index `4` is outside this four-position string; some symbols, such as certain emoji, occupy more than one Java text position.

**`charAt(...)`** - A String method that returns the `char` at a supplied index. `"Maya".charAt(0)` selects the initial `M`, and index `3` selects its last `a`. An index must be at least zero and less than the length; an empty String has no valid index.

**`char`** - The Java keyword for a primitive type representing one Java text storage unit. The value returned by `"Maya".charAt(0)` is a `char` that displays as `M`. Some visible symbols require two units, so one `char` is not guaranteed to represent a complete visible symbol.

**Input source** - The place a program reads information from. The Scanner examples use supplied text so the results can be repeated. Reading that text and printing a message are separate actions: output does not automatically become new input.

**Library object** - An object providing ready-made operations from a library. A Scanner object reads supplied text and interprets its values. Creating a reader does not by itself read every value or decide the intended order.

**Scanner** - A Java library class whose objects read text as lines or tokens and can interpret numeric text. A reader can use `nextLine()` for a name and `nextInt()` for a count. Each read advances the reader, so repeated reads do not restart at the beginning.

**Import and `import`** - An import makes a class's short name available in source code. `import java.util.Scanner;` lets later statements use `Scanner`. The keyword does not create a reader, download a library, or read data.

**`new`** - A Java keyword used to create an object in expressions such as `new Scanner("Maya\n3\n4.5\n")`. Assigning that object to `orderInput` gives the program a name for the reader. This setup creates the reader; separate method calls read its values.

**Escape sequence** - Source notation beginning with a backslash that represents a character such as a newline. Inside a Java string literal, `\n` supplies one line-break character; the Scanner input does not contain an ordinary backslash followed by n. The notation belongs to Java source, while the reader consumes the resulting text.

**Newline** - A character marking the end of a line of text. The escape sequence `\n` represents one in a Java string literal, separating `Maya`, `3`, and `4.5` in the sample input. It is not the two printed characters backslash and n in that input.

**Delimiter** - A separator used to divide text into tokens. Scanner's default token-reading methods use whitespace as separators. Line-reading methods follow line boundaries instead, which matters when mixing `nextInt()` with `nextLine()`.

**Token** - A piece of input separated from other pieces by delimiters. In the supplied order data, `3` is a numeric token. A line and a token are not always the same: a full name can have spaces and therefore contain several tokens.

**Whitespace** - Spacing characters such as spaces, tabs, and line endings. Scanner's token-reading methods skip leading whitespace before the next token. Spaces inside a name can still matter when reading the full name as a line.

**Parsing** - Interpreting text as a value with a chosen type. Scanner's `nextInt()` can parse the token `3` into an integer. It cannot turn arbitrary words into numbers, and choosing the right parsing method depends on the input format.

**`nextLine()`** - A Scanner method that returns the remaining text on the current line and moves past its line ending. Reading the first line of the supplied receipt returns the attendee name, including any surrounding spaces. After a numeric token read, the remaining text can be empty; this method does not automatically skip to the next nonempty name.

**`nextInt()`** - A Scanner method that skips leading delimiters and interprets the next token as an integer. In the receipt source, the token `3` becomes the whole-number quantity three. It leaves the reader after that token rather than after the whole line, and it cannot parse the fractional token `4.5` as an integer.

**`nextDouble()`** - A Scanner method that skips leading delimiters and interprets the next token as a floating-point number. With the lesson's dot-decimal input and reader settings, `4.5` becomes the price four dollars and fifty cents per kit. The method must match the text format and locale; declaring a `double` variable does not change what a different read method can parse.

**Locale** - A setting for conventions such as numeric decimal separators. The course's supplied input uses a dot in `4.5`. A reader configured for different conventions may interpret that same text differently, so the format and reader settings must agree.

**Input order** - The agreement between a source's value sequence and the program's read sequence. The order examples supply a name, a quantity, and a price, then read those three values in that order. Changing the read order alone can make the program try to parse a name as a number.

**Input stream** - A source that supplies data for a program to read over time. `System.in` is Java's standard input stream; in an interactive terminal it can receive typed responses. Reading from it may wait for input, unlike reading the fixed Strings supplied by these notebook examples.

**Standard input** - The program input stream represented by `System.in`. In an interactive console, a Scanner connected to it can read typed responses. That can wait for a user, so the notebook's repeatable examples use supplied text instead.
