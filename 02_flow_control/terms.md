**Condition** - An expression whose Boolean result determines whether an action should run. With `age` set to `19`, the condition `age >= 18` produces `true`. Java requires a Boolean condition here; the number `1` is not a substitute for `true`.

**Relational operator** - An operator that compares the sizes of values, such as `<`, `<=`, `>`, or `>=`. The comparison `age >= 18` includes age 18, while `age > 18` does not. Equality uses `==`, and inequality uses `!=`; do not confuse these comparisons with the assignment operator `=`.

**Equality operator** - An operator that tests whether two values are equal or unequal. With `age` set to `19`, `age == 18` is false and `age != 18` is true. These comparisons produce Boolean results without changing age; the single equals sign in `age = 18` instead assigns a value. For String contents, use the `equals` method taught in Module 1 rather than applying this numeric comparison rule.

**Conditional branch** - A path through code selected by a condition. The keywords `if` and `else` form choices such as adult admission or a referral to the event desk. One connected `if`/`else if`/`else` chain runs its first matching branch; separate `if` statements make separate decisions and can run more than one body.

**Block** - Statements grouped between an opening brace `{` and a closing brace `}`. An admission branch can contain both a price declaration and a print statement. Indentation helps people see the grouping, but Java uses the braces to identify the block.

**Logical operator** - An operator that combines or reverses Boolean values. `age >= 18 && hasStudentId` requires both facts; `||` requires at least one, and `!hasStudentId` reverses the ID value. Java's `||` includes the case where both sides are true; it does not mean exactly one is true.

**Short-circuit evaluation** - Skipping the right side of `&&` or `||` when the left side already settles the result. A false left side settles `&&`; a true left side settles `||`. With `divisor` set to zero, `divisor != 0 && 10 / divisor > 2` is false without performing the division. Put the prerequisite first: reversing these two expressions would attempt the unsafe division before checking its divisor.

**Scope** - The part of source code in which a declared name can be used. A variable declared inside an admission branch is available from its declaration through the rest of that block, including any nested blocks. Running the branch does not make that local name available after its closing brace; declare a shared result before the branch if later code needs that name.

**Boundary test** - A test at or near a limit where behavior changes. For the rule `age >= 18`, ages 17 and 18 check the two sides of the admission threshold. A test using only 19 cannot distinguish the correct `>=` from an incorrect `>`; test relevant ID values as well as ages.

**Switch statement** - A statement that selects an entry point by matching a supplied value to a label. The keyword `switch` introduces a choice such as the library commands `"borrow"` and `"renew"`. In the colon-style switch taught here, matching a label does not automatically stop execution before the next label; use `break` when one action should finish the selection.

**Selector** - The value a switch uses to select its entry point. In `switch (command)`, the selector is the current value stored in `command`. A String selector matches by text contents and letter case, so `"renew"` and `"Renew"` choose different paths unless the program prepares the text first.

**Case label** - A marker for a possible switch match, introduced by the keyword `case`. In `case "renew":`, the fixed String value names the match and the colon ends the label. The label itself does not create a new block or a separate local scope, and this form does not accept an age-range condition in place of the String value.

**Break statement** - A statement introduced by the keyword `break` that exits its enclosing switch in the library examples. After `break;`, execution continues after that switch's closing brace. An ordinary, unlabeled break can also exit its innermost enclosing loop; it does not mean that the whole Java program stops.

**Default case** - The switch entry selected when none of its explicit cases matches the supplied value. The keyword `default` appears without a value, as in `default:` followed by a help message. It handles an unmatched command in these examples; it does not also run after every successful match that has already reached a `break`.

**Fall-through** - Continuing from one colon-style switch case into the statements under a later label without testing that label again. If the borrow action lacks its `break`, the program can print both the borrow and renew messages. This can be deliberate in some programs, but it violates the library example's rule of one action per command.

**Iteration** - One execution of a loop's repeated body. Printing one countdown value and decreasing the stored count make up one iteration in the countdown example. A final condition check that ends the loop does not count as another body iteration.

**While loop** - A loop introduced by the keyword `while` that checks its condition before each possible body execution. With `remaining` starting at three, `while (remaining > 0)` can print 3, 2, and 1 as the body decreases the value. If it starts at zero, the first check is false and the body runs zero times.

**Loop progress** - A change that moves a loop toward its stopping condition. A countdown decreases its counter, while the quantity validator reads another supplied integer. Repeating a print statement alone does not change the value being tested; identify the particular update or read that can change the next decision.

**Termination** - The end of a loop's repetition. The countdown terminates when its condition becomes false at zero, then execution continues after the loop. Merely intending a loop to finish is not enough: its updates and supplied input must make a stopping path possible.

**Infinite loop** - A loop that continues without reaching a stopping path. If `remaining` stays at three inside `while (remaining > 0)`, the same true check keeps allowing another iteration. A missing update can cause this problem, but a loop that is slow or waiting for input is not automatically an infinite loop.

**Do-while loop** - A loop that runs its body before checking whether to repeat. The keywords `do` and `while` surround the body and its ending test, as in `do { ... } while (condition);`. The body therefore runs at least once, and the final semicolon is required; this does not justify placing a semicolon between a regular while condition and its intended body.

**Sentinel value** - An input value chosen to signal the end of a sequence. In the supplied quantities `"2 4 -1"`, the program processes two and four, then stops when it reads `-1`. The sentinel is a control signal rather than a quantity to pack, and the test must recognize it before the processing body runs.

**For loop** - A loop introduced by the keyword `for` that groups initialization, a condition, and an update in its header. In `for (int kit = 1; kit <= 3; kit = kit + 1)`, initialization happens once, while the condition and update control repeated work. Execution follows initialization, condition, body, update, then condition again; it does not follow the header's written order on every iteration.

**Accumulator** - A variable that keeps a combined result across iterations. A `labelsPrinted` count starts at zero before the loop and increases after each label is printed. Resetting it to zero inside every body execution discards earlier progress; its meaning also differs from a loop counter that tracks which kit is being processed.

**Nested loop** - A loop inside another loop's body. For each group in the label report, the inner loop visits that group's kits, starting again at kit one for the next group. Two groups with two kits produce four ordered pairs, not two; verify the actual pairs as well as the total count.

**Outer loop** - The enclosing loop in a nested pair. In the label report, its `group` variable chooses one group, and that iteration includes the complete inner kit loop. The outer loop advances to the next group after the inner loop finishes; the two counters do not advance together after each label.

**Inner loop** - The loop placed inside another loop's body. In the label report, it visits kit one and kit two for the current group. Each new outer iteration reaches the inner declaration again and starts a new kit sequence at one. The shared accumulator is declared outside both loops, so restarting the inner sequence does not reset the report total.

**Continue statement** - A statement introduced by the keyword `continue` that skips the rest of the current loop body. In the lesson's for loop, `continue;` for kit two skips that print but still leads to the update and the next condition check. It does not exit the whole loop; in a while loop it goes directly to the condition and can therefore skip a needed update later in the body.
