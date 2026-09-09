Concurrency lets a program manage activities whose progress overlaps. You will start independent Java workers, wait for completed results, and protect operations on shared data. You will then coordinate a producer and consumer before moving slow work out of a JavaFX interface thread. The examples connect each coordination rule to an observable result, including completion, cancellation, and closing a window.

Study these lessons in order. Each notebook includes explanations, demonstrations, practice, and hidden answers. Use the [module glossary](terms.md) to review the terms.

1. [Starting and Joining Threads](01_starting_and_joining_threads.ipynb) — Start independent jobs and join them before reporting their results.
2. [Protecting Shared State](02_protecting_shared_state.ipynb) — Explain a lost update and protect a complete shared operation with one lock discipline.
3. [Producer and Consumer Coordination](03_producer_consumer_coordination.ipynb) — Transfer a finite ordered sequence through a bounded queue and finish both cooperating roles.
4. [Background Tasks and Responsive Interfaces](04_background_tasks_and_responsive_interfaces.ipynb) — Keep a real Workspace Desktop window responsive while background work succeeds, fails, or is cancelled.

## Required Course Resources

Use these resources alongside the notebook explanations. The JavaFX example provides background for the course examples; follow the notebooks for the current Workspace procedure.

- [Introduction to Threads](<https://bhcc.techsmithrelay.com/rovY>) — Required course-plan resource.
- [Producer and Consumer Example](<https://bhcc.techsmithrelay.com/PKD6>) — Required course-plan resource.
- [What is Parallelism?](<https://en.wikipedia.org/wiki/Parallel_computing>) — Required course-plan resource.
- [What is a Thread?](<https://en.wikipedia.org/wiki/Thread_(computing)>) — Required course-plan resource.
- [Defining and Starting a Thread](<https://docs.oracle.com/javase/tutorial/essential/concurrency/runthread.html>) — Required course-plan resource.
- [Multi-Threading with JavaFX](<https://examples.javacodegeeks.com/desktop-java/javafx/javafx-concurrency-example/>) — Required course-plan resource.
- [The Producer and Consumer Problem](<https://en.wikipedia.org/wiki/Producer%E2%80%93consumer_problem>) — Required course-plan resource.
