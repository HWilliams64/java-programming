**Concurrency** - Separate activities make progress during the same period. Starting two jobs permits that progress to overlap. It does not prove the jobs execute simultaneously or finish faster.

**Parallel execution** - Activities execute at the same time on available computing resources. Two started Java threads permit concurrency, but this lesson does not measure whether their instructions ran simultaneously.

**Runnable** - The Java interface whose run method supplies a job. CountJob implements Runnable so a Thread can execute it. Constructing or directly calling the job is separate from starting a new thread.

**Thread** - A path of execution in a Java process. new Thread(job) constructs a worker for a Runnable. Construction alone does not start the worker, and its completion order is not guaranteed.

**start versus run** - Calling start requests execution on the new worker; calling run directly is an ordinary call on the current caller. The same behavior can therefore execute in different contexts.

**Thread lifecycle** - A Thread is constructed, started once, and eventually terminates when its work returns. A second start is invalid even after termination; create a new Thread for another run.

**Interleaving** - An ordering in which actions from separate threads occur among one another. One observed ordering is not a guarantee for later runs. The caller’s print order can be fixed even when worker finish order varies.

**join** - A Thread method that lets the caller wait for a specified worker to finish. In these examples, the worker has been started and join has no timeout. When that join returns normally, the worker has terminated and its earlier writes are visible to the caller. An interrupted join does not establish completion, and joining one worker does not wait for every other worker.

**Worker confinement** - An ownership rule in which one worker uses mutable state and the caller inspects it only after completion. Separate CountJob totals follow this rule; merely making a field private does not establish confinement.

**Shared mutable state** - Changeable state reachable by more than one thread. Passing one SharedCounter object to two jobs shares its total. Private access alone does not coordinate their method calls.

**Data race** - Conflicting accesses in different threads without the needed ordering, including at least one write. A lucky expected result does not prove the absence of a race.

**Lost update** - A change that disappears when separate updates use the same earlier value. If two operations both read seven, each can calculate eight and then store eight. Two intended increments have increased the total only once. This is an illustrative ordering, not a measurement of a particular thread schedule.

**Atomic state transition** - Related operations protected from conflicting cooperating access as one unit. Checking and reserving a ticket must stay together. Protecting only the final decrement leaves the decision unprotected.

**synchronized** - A Java keyword used here on instance methods to acquire the receiver’s monitor for the method. Both callers must follow the same lock discipline. Synchronizing unrelated objects does not protect one shared transition.

**Intrinsic monitor** - The lock associated with a Java object. A synchronized instance method uses its receiver’s monitor. The monitor is not a promise of fairness or an assigned winner.

**Mutual exclusion** - Only one cooperating caller at a time enters code guarded by the same lock. It prevents overlapping protected transitions; callers that bypass that lock rule are not protected.

**Synchronization visibility** - Ordering that makes earlier relevant writes visible after a later acquisition of the same monitor. Use the common discipline for related reads and writes, then join workers before final reports.

**Producer** - A role that supplies items for another role to process. WordDelivery puts the fixture words into a queue. Its input stays unchanged while delivery runs.

**Consumer** - A role that receives and processes supplied items. WordCollector alone changes its received list. The caller reads its completed report only after joining it.

**BlockingQueue** - A Java interface for a queue that coordinates concurrent item handoff. Blocking operations can wait for an item or room. It provides neither an automatic end-of-work rule nor broadcast delivery.

**ArrayBlockingQueue** - A bounded queue implementation constructed with a positive capacity. Capacity two limits stored items to two; it does not guarantee which worker runs next.

**Blocking coordination** - Waiting for a condition through a coordinating operation rather than repeatedly checking in a busy loop. take may wait for an item; this does not make waiting appropriate on the UI thread.

**Backpressure** - A full bounded queue can make a producer wait until space is available. A larger capacity changes buffering, not the agreed completion count.

**FIFO** - First in, first out: the single-producer items are received in their insertion order. This does not order the workers’ completion or send an item to every possible consumer.

**Completion protocol** - An agreement about when normal work is finished. The queue examples agree on the number of delivered items before starting. A wrong count can leave a role waiting.

**Interrupt** - A cooperative stop request to a thread. An interruptible queue operation may report InterruptedException. The request does not forcibly stop arbitrary computation.

**InterruptedException** - A checked exception reported by interruptible waiting operations. These workers restore their flag and return from run. Catching it and continuing the same loop would not implement their shutdown rule.

**Cooperative cancellation** - A worker responds to a stop request using its defined protocol. The owner interrupts both ongoing queue roles before joining either. Their false alive reports prove termination, not how many items were processed.

**Task** - A JavaFX work object that computes a result through call and reports state. Task<Integer> can supply an integer result. Its work belongs on a chosen background thread, not in a UI callback.

**call** - The Task extension method implemented for background computation. Live control updates belong in UI callbacks. Calling the computation directly is not the demonstrated Task lifecycle.

**protected** - A Java access modifier that allows access within the declaring package and qualified access through subclasses. Our Task subclass uses it when overriding call, following the library’s method declaration. It does not make call a public operation that any unrelated class can invoke.

**offer** - The queue operation used here to try insertion without waiting. It returns whether the item was inserted. A false result is not permission for the UI thread to block until room appears.

**Success handoff** - The successful Task result is read with getValue in its success callback on the UI thread. This is a completed value, not a blocking wait for unfinished work.

**Failure handoff** - The recorded Task exception is read with getException in its failure callback and shown as useful text. Failure is not silently replaced by an invented successful value.

**Task cancellation** - A cooperative request that this Task stop. A waiting take responds to interruption, and call checks isCancelled. A canceled state label alone does not prove arbitrary worker termination.

**Window ownership** - The window is responsible for requesting shutdown of its unfinished task when hidden. Actual named-worker checks establish cleanup separately from the disappearance of the window.

**Single-use Task lifecycle** - A Task represents one execution. After completion or cancellation, another run creates a new Task and Thread. Disabling repeated Start supports this rule but does not replace the underlying lifecycle contract.
