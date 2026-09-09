# Starting and Joining Threads — video transcript

## Narration

Welcome to this Java tutorial, where you'll describe independent work with Runnable, start separate threads, and join them before reading their results.

Clear ownership and completion rules let larger applications prepare independent parts of a report while ensuring the caller uses finished results.

A campus welcome desk needs two preparation counts. One job models two badge checks; the other models four supply checks. Each loop iteration adds one completed check to that job's own count. These are small model counts, not actual badge inspections or file operations.

We'll start both workers, wait for both to finish, and then report the first count, the second count, and whether either worker is still alive. The caller will print in that fixed order. After the worked run, you'll predict the report for different job limits; the output will still not tell us which worker finished first.

Let's open Main.java in the Workspace and give this program a starting point. Then we'll define the work before creating the workers that execute it.

Main is the class containing the program, and its main method starts the caller's execution. Waiting with join can throw the checked InterruptedException, so this small demonstration declares that possibility. Our expected report follows the normal path where both waits complete.

Each preparation job needs its own limit and result. We'll define CountJob here inside the main method, using Runnable to specify its work operation. The constructor records the requested checks and starts that object's total at zero.

The two fields belong to each CountJob object. Private limits direct field access, but it does not by itself keep threads from sharing an object. Our design will give each worker a separate job. Let's supply the run method that performs that job's counting work.

The loop begins at zero and adds one for each index below the limit. Override checks that this public method implements the interface operation. Defining run has not started a worker; it only describes what a later invocation will do.

The caller will need to read the completed total, so let's add a getter and finish the job definition. The getter returns a value; it will not wait for the work on its own.

Now let's create separate jobs for the two badge checks and four supply checks. Each receives its own limit and zero result, which keeps their changing totals separate.

First and second identify the work objects. To request separate execution, we also need two Thread objects, each associated with its corresponding job. Constructing those workers still does not run the counting loops.

We have two jobs and two prepared execution paths. Let's start both before waiting for either, so both requests exist before the caller begins its first wait.

Start requests that a worker execute its run method while the caller can continue. Calling a job's run method directly would instead be an ordinary call on the caller's thread. Starting allows concurrent progress; it does not guarantee simultaneous execution, faster completion, or a particular finishing order.

The report needs finished values, so let's join each started worker. Joining the first concerns only that worker; the second may keep progressing while the caller waits.

When an untimed join on a started worker returns normally, that worker has terminated and its earlier writes are visible to the caller. Both joins are needed before treating both totals as final. If a join exits through interruption, that exception does not establish completion and this expected report does not follow.

Let's print each job's finished total, then ask whether either worker is alive. This observation is meaningful after the starts and joins: false by itself could also describe a thread that was never started.

The caller's print statements fix the report order. Each worker changed only its own job's total, and both waits now establish completion. Let's click Run to see the completed counts.

First is two because that job performed two increments. Second is four because its separate job performed four. Workers alive is false after both workers have terminated. These lines come from the caller; listing First before Second does not tell us which counting job finished first.

Let's change the two job limits to three badge checks and two supply checks. The ownership, starts, joins, and print statements stay the same. Running the complete program again will construct fresh jobs and fresh Thread objects; a Thread object itself cannot be started a second time.

Before running, predict all three report lines for the new limits. Then decide whether the report can establish which worker finished first. Use the loop counts, each normal join, and the caller's print order as separate parts of your explanation.

Let's click Run and compare your prediction with the actual report from these new work objects.

First is now three and Second is two, matching the two new limits. Neither worker is alive after both joins. The values changed because the requested work changed, while the same ownership and completion rules kept the results ready for the caller. The report still does not establish worker finish order.

You separated work descriptions from execution paths, started independent workers, and waited before reading their results. Each worker owned its changing total, and a normal join established completion and visibility. For a transfer task, describe two independent jobs in a report you might build. Identify each job's state, where the caller must wait, and why the final report order would not prove simultaneous execution or finishing order.

## Visual description

[Four designed opening scenes distinguish work descriptions, worker execution and completed results; explain completion and ownership; introduce two badge checks and four supply checks at a campus welcome desk; and present blank report criteria without revealing the later prediction.]

[The real Workspace opens Main.java. The camera follows construction of CountJob with its own limit and total, a run loop that increments its total, and a result getter. Two separate jobs are associated with separate threads. The caller starts both workers and joins both before printing.]

[The pointer clicks native Run Code. The three output lines are First: 2, Second: 4, and Workers alive: false. The caller fixes report order; the output does not establish worker finish order, simultaneous execution, or a speed gain.]

[Two constructor input lines are visibly changed to three and two. A prediction and thinking pause precede the second native Run Code click. The canonical output is First: 3, Second: 2, and Workers alive: false. The closing connects separate mutable state and normal completion waits to reading finished results, then asks students to describe two independent report jobs, identify their state and completion waits, and explain why final report order does not prove simultaneous execution or finishing order.]
