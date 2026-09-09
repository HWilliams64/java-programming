# Catching and Tracing Exceptions — video transcript

## Narration

Welcome! In this Java tutorial, you'll handle exceptions, the objects that describe interrupted operations, and use a stack trace, a record of method calls, to locate a failure.

Exception handling helps applications respond to failed requests without losing unrelated work, while diagnostic traces help developers locate the code that needs attention.

Today we'll build a calculator for campus staff comparing ways to divide twelve supply items among groups. The proposed group counts are three, zero, and four; each proposal starts with the same twelve items.

A valid proposal should report items per group. Zero groups should receive a clear failure message, and the next proposal should still run. We'll also trace where a failed method call began.

Now that we're in the Workspace, let's open Main.java.

The file is open. We'll separate calculating a share from deciding what to tell the user. Let's write RatioTools with a static share method that receives an item total and a group count.

Share returns whole items per group. With twelve items and three groups, it returns four. With zero groups, integer division raises ArithmeticException before a number can return. This is a failure during execution; the method's source is valid Java.

To examine a chain of calls later, let's add quote. Here a quote means a proposed share, not a price. This small helper requests twelve items divided among zero groups.

Quote calls share rather than doing the division itself. That gives us a caller to look for in the recorded trace. Our first comparison will call share directly, so quote does not run yet.

Now let's add the program's starting structure and its proposed group counts. Main is the class that contains this standalone program; its main method is where Java begins running it.

The array holds three independent proposals. The loop supplies one group count at a time, while the total stays at twelve. These are alternative plans, so we do not subtract items as we compare them.

Each proposal needs its own response if division fails. Let's put a try block inside this loop, containing the method call and the success messages.

Try marks the work whose failure the following handler can address. Java must finish the share call before it can assemble and print the Share message. If the call fails, that print never completes, and the Calculated message is skipped too. Leaving unfinished work this way is called abrupt completion.

We need to explain the failed proposal without pretending it produced a share. Let's add a catch block for ArithmeticException and print a clear message.

Catch is the handler. Its variable problem refers to the exception object produced by the failed division. The handler reports the problem; it does not invent a numeric answer. Because this handler belongs to one loop iteration, a zero count does not discard later proposals.

Finally, let's mark the end of each attempt inside the loop, then print Done once after all the inputs have been considered.

Next input is after the handler but still inside the loop. It can print after success or a handled failure. Done is outside the loop, so it prints once. Finishing catch continues after the try and catch statement; it does not retry the division. Let's click Run and examine the complete report.

The first proposal prints Share: four, then Calculated, because twelve divided among three groups succeeds. Next input finishes that attempt. Zero groups prints the failure message instead of either success line, then reaches Next input. Four groups still gets its turn and reports three items per group. Done appears after the loop.

We handled one failed proposal while preserving the remaining work. A handler around the entire loop would be reached only after that loop had been left, so it would not resume at the following input.

Let's test the same rule when the failure comes first. We'll change only the proposed counts to zero, six, and two, leaving the methods and all messages unchanged.

Before running, predict every output line in order. Decide which messages the zero count skips and whether both later proposals are processed. Remember that each proposal uses twelve items. Pause here to work through your prediction.

Let's click Run and compare the output with your prediction.

The first input reaches the handler, then Next input. Six groups receive two items each, and two groups receive six items each. Both successful proposals print Calculated. A failure at the beginning still does not prevent either later iteration, because recovery happens within each iteration.

That explains how processing continues. A developer also needs to locate the failed operation, especially when one method calls another. We'll keep RatioTools and replace the loop with a call to quote, followed by a diagnostic handler.

Quote calls share with zero groups. Share cannot return a quotient, and quote cannot finish its own return. Java leaves those unfinished calls to reach our handler. That outward search is stack unwinding. Quote completed is skipped because its preceding call never returns normally.

GetMessage reads the diagnostic message. GetStackTrace returns an array of recorded calls. Index zero selects the first entry, and getMethodName reads its method name; index one reads the next entry. Both exist in this example. General diagnostic code should check the length before selecting an entry. Let's click Run to inspect this failure.

The message identifies division by zero. Share appears first because that is where the division failed. Quote appears next because it called share. We entered quote before share, but the trace begins at the failure and works outward. No quotient traveled back through these calls; the exception reached the handler instead.

You used try and catch to give a failed request a defined response, placed the handler so independent work could continue, and used a stack trace to locate the failure and its caller. In another application, consider which failures should reject just one request and which should stop the whole operation. That requirement should guide where you put the handler.

## Visual description

[The opening contains four different code-free scenes in the BHCC red, blue, and white visual style. The first connects exception handling with responding to failures and diagnosing their source. The second shows why those capabilities matter for requests, independent work, and developer investigation. The third introduces campus staff comparing ways to divide 12 supply items among 3, 0, or 4 groups. These are independent proposals using the same total. The fourth previews successful shares, a response to zero groups, and continuation to later proposals.]

[The video moves into the real Workspace and opens Main.java. The view zooms toward the insertion point during typing. RatioTools contains share, which divides the item total by the group count, and quote, which calls share with zero groups for a later diagnostic example. The Main class and main entry method hold the caller. An enhanced for loop considers the group counts. Its try/catch is inside the loop so each proposal receives its own response.]

[The pointer moves to the native Run button and clicks. The view widens to show output. Three groups receive a share of 4 and a Calculated message. Zero groups produces Cannot divide by zero. without a share or Calculated message. Four groups receive a share of 3. Next input follows each attempt, and Done appears after the loop.]

[The group counts change to 0, 6, and 2. The video pauses for a prediction before the pointer clicks Run again. The zero-group response appears first. The remaining proposals report shares of 2 and 6. Each attempt still ends with Next input, and the loop finishes with Done.]

[The loop is replaced with a caller that invokes quote and catches its arithmetic failure. The handler reads the exception message and the first two recorded method names. The third visible Run click produces / by zero, share, and quote on separate lines. The explanation connects the failed division to the unfinished calls, distinguishes call-entry order from stack-trace order, and closes by reviewing handler placement and diagnosis of another failed request.]
