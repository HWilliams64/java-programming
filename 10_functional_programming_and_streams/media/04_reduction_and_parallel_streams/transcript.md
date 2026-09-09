# Reduction and Parallel Streams — video transcript

## Narration

Welcome to this Java tutorial, where you'll combine values with a reduction and explain why an identity and an associative rule support correct sequential and parallel results.

Applications use reductions to turn individual contributions into totals and other summaries. A valid combining rule also lets an application combine partial results without changing the meaning of its report.

Today we'll make a supply report for a campus clerk. Three deliveries contain two, four, and one item. Every quantity counts once, and the report must total the items using separate sequential and parallel computations.

Both results should be seven items. We'll connect that agreement to zero and addition, then change the delivery quantities and predict another report. The comparison checks the results; it does not measure which mode is faster.

Now that we're in the Workspace, let's open Main.java and set up our supply report.

We'll use ArrayList to hold the delivery quantities. The program's statements go inside the main method of our Main class, where this application starts.

Let's record the three deliveries in counts. Each Integer entry measures items in one delivery, so the total must include each entry exactly once.

Counts now holds two, four, and one. We need one total from those values. That's the job of a reduction. Let's request a fresh sequential stream and give reduce zero and an addition rule.

The two lambda parameters receive values to combine, and the expression returns their sum. This is the BinaryOperator pattern: two inputs and a result of the same type. One sequential trace starts at zero, adds two to get two, adds four to get six, and adds one to get seven. Reduce returns that total before the assignment finishes.

Zero is an identity because adding it leaves a value unchanged. It contributes no extra items and gives the result when there are no entries. Starting at one would invent an item that no delivery supplied.

Now let's calculate the same report from a fresh parallel stream. We'll keep both the identity and the addition rule unchanged.

Parallel processing may divide the work and combine partial results. One possible grouping could total two and four to get six, then combine that with one. Another could combine four and one first. Addition gives seven either way. Preserving the result under regrouping is called associativity. This explanation describes valid groupings, not the schedule Java necessarily used.

The rule also stays independent of changing shared state. It returns the sum of its inputs instead of updating a separate shared total. And it leaves counts unchanged while processing, which satisfies noninterference. Each computation creates a fresh stream because its terminal reduction consumes that stream.

Let's print the two completed totals with clear labels and finish the program.

The report is ready. Let's click Run and compare the returned totals with the seven items we expected.

Both lines report seven. Each calculation includes all three deliveries, and neither adds an extra contribution. The caller prints Sequential first because the print statements run in their written order. These lines show complete results, not the order in which parallel work processed individual entries.

Let's change only the delivery quantities to five, zero, and six. Keeping the two computations unchanged lets us check their rules with another input, including a delivery that contributes no items.

Before running, predict both output lines. Explain the difference between the zero entry in counts and the zero identity supplied to reduce. Then give two possible groupings of the quantities that preserve their order and check whether those groupings agree.

Let's click Run and compare your prediction with the new report.

Both totals are eleven. The zero list entry describes a delivery with no items, while the identity is the neutral value used by the reduction. Neither changes the sum of five and six. Grouping five with zero first or zero with six first still gives eleven. The inputs changed, but the valid combining rule did not need to change.

You used reduction to make one result, checked the neutral identity and associative combination, and kept the source and processing rules independent of changing shared state. Equal totals support this result, but they do not establish a speed improvement. For your next design, choose a numerical report and explain its contributions, combining rule, and empty-input result before deciding whether parallel processing is appropriate.

## Visual description

Four opening scenes introduce reduction, identity, associativity, and parallel results; connect these skills to application summaries; establish a campus clerk's deliveries of two, four, and one item; and show the expected sequential and parallel totals of seven.

In the real Workspace, Main.java opens and the camera follows typed code. The program stores the quantities in an ArrayList, computes two reductions using zero and addition, and prints labeled totals. Narration explains the lambda inputs and returned result, the neutral identity, valid regrouping, stateless processing, and an unchanged source.

The pointer moves to and clicks the Run Code button. The console prints Sequential: 7 and Parallel: 7. Narration distinguishes completed totals from unobserved parallel scheduling.

The three entries change to five, zero, and six. A pause lets students predict the two outputs and distinguish a zero input from the neutral identity. The pointer clicks Run Code again. Both printed totals are eleven. The conclusion reviews the reduction requirements and explains that matching results do not measure speed.
