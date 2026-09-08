# While Loops and Validation

## Narration

Welcome to this Java tutorial, where you'll trace a while loop's repeated body, use a new input value to make progress, and explain why the loop stops when a valid value arrives.

Repeated checks let applications handle different numbers of attempts without duplicating source code, while a clear stopping rule keeps the program from processing more input than the task needs.

A workshop assistant is recording a request for supply kits. A valid request is a positive whole number of kits; zero and negative quantities must be rejected. The assistant needs to report the first valid request.

The input is fixed text containing integers and a positive value. Our program will print each rejection, report the first accepted quantity, and stop reading. After a worked example and a request that's valid right away, you'll predict a new sequence.

Let's open Main.java and build the quantity check.

Main is the class containing our program, and its main method is the named operation where execution begins. We'll add our statements inside that method. The import makes Scanner's short name available for reading our supplied text.

The starting structure is ready. For the first worked case, the supplied entries are negative five and six kits. We'll create a Scanner to read them in order and store its first integer in quantity, so the condition has a request to check.

That first read stores negative five. Scanner has moved past that token, but six has not been read. The condition checks the stored quantity; it doesn't choose another input by itself. Let's add a while body that runs only while the current request is zero or negative.

The while keyword introduces a test before every possible body execution. Parentheses enclose the Boolean comparison, and braces mark the repeated body. When the comparison is true, the body rejects that request. One body execution is an iteration.

The rejection message alone leaves quantity unchanged. Without another read, the loop would keep testing the same invalid request. We'll assign the next integer to quantity inside the body. That read makes progress by advancing through the supplied entries.

The body now prepares the next condition check. After rejecting negative five, the read will store six, and execution returns to the while condition with that new value. It does not recreate Scanner or repeat the first declaration. We still need to report the quantity that ends the loop.

The accepted print is outside the loop. When quantity is positive, the comparison is false, so Java skips the body and reaches that print. This is termination: the repetition ends, while the rest of the program continues. Let's click Run to check our worked case.

The output shows one rejection and Accepted: 6. Negative five makes the first test true, so the body prints once and reads six. Six makes the next test false. There is one iteration but two condition checks, including the check that stops repetition.

The stored quantity changes because the next read is assigned to it. Our supplied data includes a positive value, so this run reaches its stopping condition. Each required token must exist and be an integer; handling missing or nonnumeric input is a later problem.

A while loop can also skip its body. Let's replace the supplied text with seven alone. Seven already meets the positive-quantity rule, so the first condition will be false. The program should accept that value without a rejection or another read.

Only the input text has changed. Running the complete program will create a fresh reader and perform the first read again. The same condition will decide whether the body is needed. Let's run this boundary case.

Only Accepted: 7 appears. The first condition is false, giving zero iterations and one condition check. No second read happens, which matters because there is no second token. A while loop tests before its body, even on the first visit.

We have checked a rejected request followed by acceptance and a request that is valid immediately. Now change only the supplied text to zero, negative two, and three. Keep the reading order and condition the same.

The new sequence is in place. Before clicking Run, predict every output line and count the body executions. Trace the quantity used by each condition check, including the final false check. Also identify the last input read. Pause here if you want more time.

Let's run the changed program and compare its output with your trace.

There are two rejection messages, then Accepted: 3. The first read stores zero. One iteration rejects zero and reads negative two; the next rejects negative two and reads three. The final test is false, so the accepted print runs. That's two iterations and three checks, with no read after three.

Our quantity check meets the assistant's rule. The while condition decides whether to repeat, each read prepares a new value for the next test, and the final false check leads to the accepted result. Keeping the starting read, repeated work, and stopping decision clear helps us explain both repeated rejection and immediate acceptance.

For a different rule, suppose a request must be at least two kits. How would you change the invalid condition, and which two neighboring quantities would test that boundary? Explain why the read still belongs inside the body.

## Visual description

Four distinct opening scenes show a repeating test-and-read process; different numbers of attempts reaching one shared rule; a workshop assistant requesting supply kits; and a report sheet requiring rejection messages followed by the first valid request. The opening does not reveal the canonical output.

The real Workspace shows Main.java. Small groups of source are typed while the camera follows the editor. The program reads one integer before testing the while condition. Its body prints a rejection and reads a replacement value. A final print follows the loop. The actual Run Code toolbar button is clicked for each of three complete programs.

### Worked reject then accept

Supplied integer text: `-5 6`.

```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner quantities = new Scanner("-5 6");
        int quantity = quantities.nextInt();
        while (quantity <= 0) {
            System.out.println("Try a positive quantity.");
            quantity = quantities.nextInt();
        }
        System.out.println("Accepted: " + quantity);
    }
}
```

Actual output:

```text
Try a positive quantity.
Accepted: 6
```

### Worked positive first

Supplied integer text: `7`.

```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner quantities = new Scanner("7");
        int quantity = quantities.nextInt();
        while (quantity <= 0) {
            System.out.println("Try a positive quantity.");
            quantity = quantities.nextInt();
        }
        System.out.println("Accepted: " + quantity);
    }
}
```

Actual output:

```text
Accepted: 7
```

### Canonical prediction

Supplied integer text: `0 -2 3`.

```java
import java.util.Scanner;
public class Main {
    public static void main(String[] args) {
        Scanner quantities = new Scanner("0 -2 3");
        int quantity = quantities.nextInt();
        while (quantity <= 0) {
            System.out.println("Try a positive quantity.");
            quantity = quantities.nextInt();
        }
        System.out.println("Accepted: " + quantity);
    }
}
```

Actual output:

```text
Try a positive quantity.
Try a positive quantity.
Accepted: 3
```

Only the supplied input line changes between the complete runs. Before the canonical third run, an eight-second prediction pause leaves the source visible without the answer. The closing explains the first test, repeated input progress and final valid value, then asks how a minimum request of two kits would change the condition and boundary test. That transfer answer stays hidden.

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0). Full license and source evidence are retained with the composition.
