# Producer–Consumer Coordination — video transcript

## Narration

Welcome to this Java tutorial, where you'll coordinate a producer and consumer through a bounded queue and use an agreed item count to complete their delivery.

Separating delivery from processing helps applications handle requests at different rates while limiting pending work and establishing when a report is complete.

A campus supply desk passes item requests from one worker to another. Our first list contains tag, then map. The producer must send each name once, and the consumer must collect both in that order. The queue can hold two pending names; each removal makes space available again.

We expect the received list to contain tag, then map, and the completed queue to be empty. Both workers must finish before the caller prints those reports. Later, you'll predict a delivery with three names through the same capacity-two queue. We will distinguish what the queue guarantees from what the final output cannot tell us about scheduling.

Let's open Main.java in the Workspace. We'll build the two jobs, connect them to one queue, and have the caller wait for their completed report.

We need ArrayList for the consumer's result and two queue types for the shared handoff. BlockingQueue describes the operations; ArrayBlockingQueue supplies their fixed-capacity implementation. Let's add those imports and the main method. The caller declares InterruptedException because its later joins can be interrupted.

Let's define WordDelivery, the producer's job. It keeps the supplied queue reference and the array of names. Recording those references does not copy either object. Our example leaves the input array unchanged while the worker reads it.

The producer's run method will visit every name in array order and call put once for each. Put can wait when the bounded queue has no free slot, so we'll place the loop inside a try statement.

A full queue slowing delivery is backpressure. Put can proceed when a removal makes space, so the capacity limits pending names rather than the total names delivered. Let's also handle an interrupted queue operation by restoring this worker's interrupt flag and reaching the end of run.

InterruptedException reports a cooperative interruption and clears the flag. Restoring it records the request; leaving the work method is what ends this worker. The expected report follows normal delivery, so this exit path should not be mistaken for proof that every requested name was sent.

Now let's define WordCollector. It needs the same queue, an agreed number of items to receive, and its own ArrayList for the report. Only this consumer will change that result list.

Let's implement the collector's counted loop. Take removes and returns the next queued item, waiting if none is available. Java obtains that returned name before adding it to received; the add has not occurred while take is still waiting.

ArrayBlockingQueue uses first-in, first-out order. With one producer and one consumer, the received names keep the producer's insertion order. A take transfers its item to one receiver; it does not broadcast it. Let's give the collector the same interruption response and a report method for its completed list.

The two roles own different surrounding state: the producer reads the unchanged input, and the consumer builds its own result. The queue coordinates their shared handoff. It does not automatically protect arbitrary objects elsewhere in the application.

Let's create the first input, tag followed by map, and a queue that stores at most two pending names. This number describes the queue's capacity, not a lifetime delivery limit.

Now let's connect both jobs to that one queue. WordDelivery receives the array, and WordCollector receives its length. This is the finite completion protocol: the number of successful takes must match the number of supplied names.

An empty queue between handoffs does not mean delivery is over; the producer might still have another name to send. The agreed count supplies the ending rule. An extra take could wait for an item that will never arrive, while too few takes could leave work uncollected. Let's wrap each job in its own Thread.

Both roles need a chance to make progress. Let's start both workers before joining either. Starting a producer and immediately waiting for it could prevent the caller from starting the consumer that would free space in a full queue.

Now let's join both workers. Normal returns establish that each has terminated and that the caller can observe its earlier work. The caller can then read the consumer-owned list and inspect whether this completed delivery left a queued item.

Let's print the received list and the queue's empty check, then close the program. Neither report will tell us whether a worker actually waited, which worker finished first, or whether the two roles ran simultaneously.

Before running, connect the rules: two names are put in order, two names are taken in order, and both joins precede the reports. Let's click Run to check the complete delivery.

The collector received tag, then map, and the queue is empty. The two handoffs match the agreed count. This is evidence of the completed finite delivery, while the final state alone does not reveal an earlier full or empty waiting period.

Let's change only the input array to pen, map, and book. Keep the queue capacity at two. Because the collector takes the array's actual length, the next fresh run will require three receives without changing either worker's implementation.

Predict both output lines before running. Explain how three items can pass through capacity two, and whether the report can establish that the producer actually waited. Use item order, removal making space, and the agreed receive count in your reasoning.

Let's click Run to test the three-name delivery through the same queue capacity.

All three names arrived in order, and the completed queue is empty. Removing names makes space available, so capacity two does not restrict total delivery to two. The output still does not establish an exact worker schedule or prove that either queue operation had to wait.

You coordinated two roles with one bounded queue and a finite completion rule. In an ongoing application, stopping one role can leave the other waiting. Its owner must request interruption of both before joining either, and both workers must respond by exiting. For a transfer task, describe an ordered request stream, choose what limits pending work, and distinguish a fully delivered report from a completed early shutdown.

## Visual description

[Four designed opening scenes introduce a producer, a bounded queue and a consumer; connect differing arrival and processing rates to bounded pending work; state the supply-desk tag/map delivery with capacity two; and show the initial expected received list and empty queue.]

[In the real Workspace, Main.java defines a WordDelivery producer that puts each input name and a WordCollector consumer that takes an agreed number into its own list. Each interruptible loop restores the interrupt flag when interrupted and then returns. The owner starts both workers and joins both before reporting.]

[The pointer clicks native Run Code. The initial report is Received: [tag, map] followed by Queue empty: true. The report confirms this finite delivery; it does not reveal a particular scheduling order or whether a worker waited.]

[One input-array line changes to pen, map and book while queue capacity remains two. A prediction pause precedes the second native Run Code click. The final report is Received: [pen, map, book] followed by Queue empty: true. The closing distinguishes bounded pending storage from total delivered items and asks why early shutdown must request both workers before joining either.]
