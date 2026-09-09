# Protecting Shared State — video transcript

## Narration

Welcome to this Java tutorial, where you'll protect a shared counter with synchronized methods and wait for both workers before reporting its final value.

Synchronization helps applications preserve shared inventory and reservation totals across overlapping requests, while completion waits establish when a final report is ready.

A campus supply desk receives counts from two preparation jobs. The first models one thousand completed checks, and the second models two thousand. Every check should add exactly one to the same counter. These loop iterations model work; they do not inspect supplies or measure real processing speed.

We expect a final total of three thousand, with every requested check included. We'll give both workers the same counter, protect each increment, start both workers, and join both before printing one total. Later, you'll predict the total when the requested counts change. The final number will tell us about preserved updates, not which worker ran first or how often they alternated.

Let's open Main.java in the Workspace. We'll first define the object that owns the shared value, then define the work that updates it.

The main method starts the caller's execution. It declares InterruptedException because our later joins can be interrupted. The expected final report follows the normal path where both joins finish successfully.

Let's create SharedCounter with a private total that begins at zero. Private controls direct access to the field. It does not, by itself, prevent two workers from interfering with an update.

An increment reads the old total, adds one, and writes the replacement. If unsafely shared, two executions could read the same old value and both write the same replacement, losing an update. We'll make the entire increment method synchronized so cooperating calls on this counter cannot perform that transition at the same time.

This instance method uses the counter object's intrinsic monitor, its built-in mutual-exclusion mechanism. A caller must acquire that monitor before entering the synchronized method. Another synchronized call using this same object must wait until the monitor is released; this does not promise fair turns or a particular worker order.

Let's make the getter synchronized too, then close the counter class. Both methods will use the same object's monitor, so reads and updates follow one coordination rule. A synchronized getter alone would not repair an unprotected increment.

Now we'll define IncrementJob. Each job needs a reference to the counter it should update and a count specifying how many increments to request. The constructor records those two inputs; it does not copy the counter object.

The private counter field belongs to each job, but both fields can refer to the same counter. This is shared mutable state: one changeable object is reachable by both workers. Let's implement Runnable's run method to request the assigned number of increments.

Each loop iteration calls increment and therefore participates in the counter's monitor rule. The protection covers one complete read, add, and write transition per call. It does not reserve the counter for an entire job's loop, and it does not turn the Java expression into a promise about one processor instruction.

Let's construct exactly one SharedCounter for this run. Its total begins at zero. We will deliberately share this object because both preparation jobs contribute to one combined result.

Now let's create two workers. The first job requests one thousand increments and the second requests two thousand. Passing counter to both constructors gives their jobs references to the very same protected object.

Constructing a Thread prepares an execution path but does not start its work. Let's start both workers before waiting for either. Scheduling may let their calls interleave in different ways, but each completed protected increment must preserve the previous total and add one.

Protection and completion solve different problems. Synchronized prevents cooperating updates from overlapping inside the protected transition; it does not tell the caller that all requested work is finished. Let's join both started workers before reading the final result.

A normal join establishes that its worker has terminated and makes that worker's earlier actions visible to the caller. Joining only one would not establish that the other had finished. Now let's read through the synchronized getter, print the total, and close the program.

The counter started at zero, and the two jobs request three thousand increments in total. Both use the same protected counter, and both joins precede the report. Let's click Run and compare that reasoning with the output.

Total is three thousand: one thousand plus two thousand, with each update preserved. The joins establish that both jobs finished before this read. The single output line does not reveal worker order, fairness, simultaneous execution, or a speed improvement.

Let's change only the requested counts: two thousand for the first job and three thousand for the second. The next complete run will create a fresh counter starting at zero and fresh workers, while keeping the same synchronization and completion rules.

Before running, predict the new output. Explain separately why no increment is lost and why the caller can treat the reported value as final. Use the shared object, the protected transition, and both normal joins in your reasoning.

Let's click Run to test your prediction with the two new job counts.

Total is now five thousand, matching two thousand plus three thousand on a fresh counter. Synchronizing the whole update preserves each increment, and waiting for both workers makes this a completed total. One successful run of an unprotected counter would not prove that its updates were safe; our explanation depends on the program's coordination rules.

You used one shared object, one monitor rule for its operations, and two completion waits before reporting. For a transfer task, describe a shared reservation count where checking availability and decreasing the remaining amount must stay together. Explain what belongs inside the protected transition and why the caller still needs a completion rule before a final report.

## Visual description

[Four designed opening scenes introduce a shared object, protected transitions and completed reports; connect these skills to inventory and reservation requests; state 1,000 and 2,000 modeled supply checks; and present the initial expected Total: 3000 with protection and completion criteria.]

[In the real Workspace, Main.java defines SharedCounter with a private zero total and synchronized increment/getter methods. IncrementJob stores a reference to the counter and requests increments in its run loop. Both workers receive the same counter object, start, and are joined before the caller reports.]

[The pointer clicks native Run Code. The initial output is Total: 3000. The narration separates preserved updates from completed work; the single total does not reveal scheduling, fairness or a speed gain.]

[Two input lines change the requested increments to 2,000 and 3,000. A prediction pause precedes the second native Run Code click. The canonical output is Total: 5000. The closing asks what belongs in one protected availability-check-and-reservation transition and why a final report also requires completion.]
