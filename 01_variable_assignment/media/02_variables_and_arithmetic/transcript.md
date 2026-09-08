# Variables and Arithmetic

## Narration

Welcome back! In this Java lesson, you'll choose types, or kinds of values, for variables, the names that hold your program's data. You'll calculate a total and trace an assignment, which replaces a variable's stored value.

These skills let software keep track of changing information, from available seats to order totals, while choosing the right kind of value for each job.

A campus club needs a small ticket record. We'll store a whole-number ticket count, a price in dollars for each ticket, and whether sales are open. The program will calculate a total, then record a changed count.

We want to see the calculated total, the updated ticket count, and the sales status in that order. The values will be supplied in the program, so no one needs to type an order while it runs.

Let's open Main.java in the Workspace and build a practice record before we try the club's order.

We'll use the starter structure from the last lesson. Main is the class that holds our code, and its main method is the named operation where this program starts. Our ticket instructions belong inside that method.

With a place for our instructions, we can name the information the club needs. The practice count is two tickets. We'll use int because a ticket count is a whole number.

This declaration introduces tickets with its type and name. Giving it two as a starting value is initialization. The next value is a price, which can include part of a dollar, so we'll give ticketPrice the double type.

The practice price is five dollars per ticket. A double can hold fractional values, though it approximates some decimals. The prices in this example can be represented exactly. Sales status is different: it answers a yes-or-no question. We'll use boolean, which holds true or false, and start this practice record with sales closed.

We now have a count, a price, and a sales status, each with a suitable built-in type. To find the cost of the tickets, we'll multiply the count by the price and store the result in total. That calculation is an arithmetic expression: it produces a value we can use.

For this practice record, two tickets at five dollars each make ten dollars. Total stores the result of that calculation. It isn't a live formula linked to tickets. To check that, let's replace the count with six before displaying total, the count, and the sales status.

This assignment reuses tickets without declaring it again. We'll print total after the update, so the output can show whether its stored value changed too. Let's close the starter structure to check the complete practice record.

The practice program is complete. Let's click Run and check whether total still holds ten dollars after the ticket count changes.

The first line is ten point zero. We printed total after changing tickets, so this shows that total kept the ten-dollar result calculated earlier. The second line is six, the updated count. The last line is false because we left sales closed. Assignment changed tickets without repeating the multiplication or changing the other stored values.

That practice run gives us a pattern for the club's actual record. We'll replace the instructions inside main while keeping the same class and method. This time the starting count is three, the price is four dollars and fifty cents per ticket, and sales are open.

The club's starting values are in place. We'll use the same multiplication to store the order total. This time, unlike the practice run, we'll display total before changing the count.

The total calculation comes before the update. Let's finish the record by assigning four to tickets, then displaying the count and sales status, just as we did in the practice program.

The club's program is ready. Before we run it, write the three output lines in order. For each print statement, ask which value is stored at that point. Use the practice run to decide whether the later assignment changes the earlier calculation. Pause here if you'd like more time.

Let's click Run to check your prediction against the club's actual record.

The total is thirteen point five dollars: three tickets multiplied by four dollars and fifty cents. Four is the updated count, and true means sales are open. Compare those three lines with your prediction. The update replaces tickets after the total was calculated; it doesn't change the earlier printed result.

We've built the club's ticket record. Int kept the count as a whole number, double held the price and total, and boolean represented whether sales were open. The expression calculated a cost, and assignment changed one stored value. Tracing the statements in order explains why the output contains both an earlier total and a later count.

For your next experiment, change only the starting ticket count to five. What total should appear, and which other output lines should stay the same? Explain your reasoning before you run the program again.

## Visual description

[Four code-free BHCC opening scenes show a central variable with different kinds of values, a horizontal software process, a campus ticket desk, and a single numbered ticket record. The Workspace appears only after the overview.]

[Main.java is opened. The class and main method are introduced. The program is typed in short groups with the camera following the active line. The practice record uses two tickets, a five-dollar price, closed sales, and a later count of six. Total is printed after the assignment; the pointer clicks the actual Run control and the console shows 10.0, 6, false on separate lines.]

[The body of main is replaced with the canonical club record below. Students predict three output lines before the second visible Run click. The output shows 13.5, 4, true. The closing connects types, arithmetic and assignment to the record, then asks students to try a starting count of five.]

## Canonical program

```java
public class Main {
    public static void main(String[] args) {
        int tickets = 3;
        double ticketPrice = 4.5;
        boolean salesOpen = true;
        double total = tickets * ticketPrice;
        System.out.println(total);
        tickets = 4;
        System.out.println(tickets);
        System.out.println(salesOpen);
    }
}
```

## Exact canonical output

```text
13.5
4
true
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Concept icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Sources and full licenses are retained with the composition.
