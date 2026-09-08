# Decisions and Boolean Logic

## Narration

Welcome to this Java tutorial on decisions and Boolean logic, or true-or-false reasoning, where you'll compare values, combine conditions, choose one possible path called a branch, and test where a program's decision changes.

Comparisons and logical conditions help software apply booking and borrowing rules consistently, while boundary tests catch mistakes where those rules change.

Today we'll build a campus event decision using a visitor's age in whole years and a Boolean fact recording whether the visitor has a student ID. Under this example's rules, visitors aged eighteen or older with an ID receive the five-dollar student price. Others who meet that age limit receive the eight-dollar general price, and younger visitors are directed to the desk.

The program should display exactly one admission instruction for the supplied visitor. We'll first work through equipment borrowing rules, where we can inspect comparisons and follow a choice. Then you'll use that reasoning to predict the event program's result. The supplied facts are repeatable examples; the program doesn't verify an ID or collect a payment.

Let's open Main.java in the Workspace. We'll start by making the yes-or-no results of our borrowing rules visible before we use them to choose an instruction.

At our equipment desk, the training requirement is at least four completed hours. This borrower has four hours and no badge. A condition is an expression that produces a Boolean result: true or false. We'll compare the stored count with that inclusive lower limit. A comparison evaluates the current value; it doesn't change the hours.

The greater-than-or-equal operator includes the limit itself. Greater than alone would exclude four. Less-than operators test the other direction. These size comparisons use relational operators. For numeric equality, Java uses two equals signs; one equals sign assigns a value. Let's now combine the training requirement with the separate badge fact.

AND requires both facts to be true. OR requires at least one, including when both are true. NOT reverses a Boolean value. The badge variable already supplies a Boolean, so we can use it directly. Now consider ten kits shared equally among groups. We'll use divisor for the group count, currently zero, and check whether each group gets more than two kits. Before attempting that division, we must check the group count to avoid dividing by zero. The AND condition asks whether a valid group count gives more than two kits per group; the OR condition flags either a missing group count or more than two kits per group.

The last two conditions show another feature of AND and OR. Integer division by zero cannot produce this quotient. In the AND expression, the left check is false, so both requirements cannot hold. In the OR expression, the left check is true, so at least one already holds. Java can skip the division in both expressions. Let's click Run to inspect all six Boolean results.

The training comparison is true at four hours. AND is false because the badge requirement fails; OR is true because training is sufficient for that different rule. NOT turns the false badge value into true. The final false and true results appear without an attempted division. This is short-circuit evaluation: Java skips the right side when the left side already settles the result.

That shortcut depends on the operator and the order. A true left side of AND still needs its right side; a false left side of OR still needs its right side. With a group count of five, the first guard would permit the division and then compare its quotient with two. Placing the unsafe division first would attempt it before the protective check. Now let's use a complete rule to choose an instruction.

Our equipment desk has three choices. Four or more training hours with a badge permits self checkout. Enough training without a badge requires staff checkout. Less training requires the training instruction. We'll store one instruction and print it after the choice. Declaring that name before the branches makes it available afterward.

Each possible path is a conditional branch. The keyword if introduces a condition in parentheses. If the condition is true, Java executes the statements in its block, the group inside braces. Here the first choice requires both training and a badge. We'll connect the other choices with else if and a final else, so they belong to the same decision.

Else if supplies another condition after the earlier one was false. The final else covers the remaining case. One connected chain executes the first matching branch and skips the others. Every path assigns instruction, and the print after the chain uses that chosen text. Let's click Run with four hours and no badge.

The program prints Staff checkout. Four hours meets the training limit, but the missing badge makes the first combined condition false. The next training comparison succeeds, so its assignment runs. The final branch is skipped. Execution then continues after the choice to the print statement; choosing a branch does not end the program.

Scope is the region of source code where a declared name can be used. Instruction was declared before this choice, so the print can use it. A new variable declared inside a branch's braces would be local to that block. Entering the branch would not make that name available outside its source-code boundary.

Now let's test the other side of the training limit. We'll change only the hours from four to three and keep the badge false. A boundary test checks a value at or near the point where the decision changes. Testing four and three can expose a mistake that testing a larger hour count would hide.

The same chain is ready with the changed input. Let's click Run and check which instruction the smaller count selects.

The result changes to Complete training. Three fails the training comparison, so the first branch is unavailable and the second comparison is also false. The final else supplies the instruction. We've checked both sides of this limit without changing the rule. The notebook will ask you to test both relevant facts in its event example.

Let's replace the borrowing program with the event program. For this visitor, age is nineteen and the student-ID fact is true. Begin with those two facts and the most specific condition, which requires both adulthood and an ID. Then we'll attach the event's other choices.

The first branch prints the student price in dollars under this example's rule. If that combined condition is false, the next condition checks the age requirement for general admission. The final else handles younger visitors. Let's attach those alternatives and complete the program.

Before we run, write the exact message you expect for this visitor. Start at the first condition, use the stored age and ID value, and decide whether a later condition is reached. Also predict how many lines appear. Pause here if you'd like more time.

Let's click Run and compare the actual admission instruction with your prediction.

One line appears: Student admission, five. Nineteen meets the inclusive age limit and the ID value is true, so the first branch runs. The later branches are skipped, even though the age-only comparison would also be true. Separate if statements would make separate decisions and could print conflicting instructions; this connected chain selects one.

We've turned supplied facts into Boolean results, matched logical operators to requirements, and used an ordered chain to choose one action. Braces grouped the branch statements, and local scope controlled where names were available. Short-circuit evaluation explained which expressions were attempted. Boundary tests checked where the selected result changed.

Now construct the notebook's admission program from the rules, starting with age eighteen and no student ID. Predict all four combinations of ages seventeen and eighteen with the two ID values. Change only the inputs for each run, compare every complete message with your prediction, and check that exactly one line appears. Restore the initial eighteen and no-ID case, then explain what each test checked.

## Visual description

[Four code-free BHCC opening scenes connect Boolean facts to a selected action, show booking and borrowing rules around a decision boundary, introduce a campus event desk with age and ID facts leading to an unresolved instruction, and reveal the inspect, trace, predict-and-compare steps.]

[Main.java is typed in short groups while the camera follows the active line. The first program compares four training hours with the required minimum and combines the result with a false badge fact. A zero group count then demonstrates two guarded division conditions. The actual Run button is clicked. Six Boolean lines print: true, false, true, true, false, true.]

[A fresh borrowing program stores its instruction before a connected conditional chain and prints the selected value afterward. Four training hours without a badge choose Staff checkout. The actual Run control produces that one line. The hours are changed to three and a third actual Run prints Complete training.]

[The source is replaced with the canonical event program below. An eight-second pause invites a prediction before the fourth mouse Run click. One output line reads Student admission: 5. The closing directs students to test age eighteen without ID and the four age-seventeen/eighteen and ID combinations, then restore age eighteen without ID.]

## Canonical program

```java
public class Main {
    public static void main(String[] args) {
        int age = 19;
        boolean hasStudentId = true;
        if (age >= 18 && hasStudentId) {
            System.out.println("Student admission: 5");
        } else if (age >= 18) {
            System.out.println("General admission: 8");
        } else {
            System.out.println("Ask the event desk.");
        }
    }
}
```

## Exact canonical output

```text
Student admission: 5
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Concept icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Sources and licenses are retained in production evidence.
