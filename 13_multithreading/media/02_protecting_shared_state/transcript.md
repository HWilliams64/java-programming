# Transcript: Protecting Shared State

This CSC-239 demonstration uses Java 21 in the Workspace. Two IncrementJob objects use the same SharedCounter, which protects its updates and reads with synchronized instance methods. The caller starts both workers and joins both before reporting the result. The supplied Main method contains the demonstration classes.

Editor parameter hints and rendered symbols are display aids; the complete source preserves the exact Java characters. The hypothetical lost-update explanation is a reasoning example, not an executed unsafe race.

## 0:00–0:21 — Goal

**On screen:** The title reads Protecting Shared State, with the subtitle Coordinate updates to one counter. Main.java is open in the Workspace. The editor is initially empty while the goal is explained.

We will protect a count that two workers update. Watch how both jobs use the same object, how synchronized methods control access, and why the caller waits before reporting the result.

## 0:21–1:23 — Share one object and one monitor

**On screen:** The program is typed into Main.java. A full view shows all 31 source lines, including the leading blank line. Lines 4 through 16 are selected: SharedCounter holds total and protects increment and getTotal; IncrementJob stores the shared reference and requested count. Below the selection, both jobs receive the same counter object. Captions sit below the source.

The complete source is:

```java

public class Main {
    public static void main(String[] args) throws InterruptedException {
        class SharedCounter {
            private int total;
            public SharedCounter() { total = 0; }
            public synchronized void increment() { total = total + 1; }
            public synchronized int getTotal() { return total; }
        }
        class IncrementJob implements Runnable {
            private SharedCounter counter;
            private int count;
            public IncrementJob(SharedCounter counter, int count) {
                this.counter = counter;
                this.count = count;
            }
            @Override
            public void run() {
                for (int index = 0; index < count; index++) { counter.increment(); }
            }
        }
        SharedCounter counter = new SharedCounter();
        Thread first = new Thread(new IncrementJob(counter, 2000));
        Thread second = new Thread(new IncrementJob(counter, 3000));
        first.start();
        second.start();
        first.join();
        second.join();
        System.out.println("Total: " + counter.getTotal());
    }
}
```

Shared mutable state means stored values that several threads can read or change. Both jobs keep a reference to this one SharedCounter. Its intrinsic monitor is the lock associated with that object. A synchronized instance method acquires that monitor. Mutual exclusion means only one cooperating thread at a time enters methods protected by this same lock.

## 1:23–1:51 — Protect the whole update

**On screen:** Lines 4 through 9 are selected while the full program remains visible. The entire read, addition and assignment appears inside synchronized increment, and synchronized getTotal returns total. The two job constructions, starts and joins are visible below. The selection identifies the code being explained; the source remains unchanged.

An increment reads a value, computes a new value, and writes it back. A data race involves conflicting accesses from different threads without the required ordering, with at least one write. Protecting the whole increment makes it an atomic state transition: these related steps cannot overlap with conflicting access that follows the same lock rule. Synchronization visibility means a later acquisition of that monitor observes writes ordered before an earlier release.

## 1:51–2:10 — Predict the total

**On screen:** The selection clears, leaving all 31 lines readable before the terminal is opened. The two requested counts, 2000 and 3000, and both joins are visible. A three-second pause follows the prediction prompt; no result is shown during that pause.

Predict the total after both jobs finish. The first requests two thousand increments and the second three thousand. What would change if each job received a different counter object? Trace the shared references and both joins before running. Pause here.

## 2:10–2:30 — Run and interpret the result

**On screen:** The view moves closer to the terminal, which displays Total: 5000 followed by a new prompt. Both job constructions, both starts, both joins and the final getTotal call remain readable above it. At this closer view, the Main class header is cropped at the top and top captions briefly cover portions of the SharedCounter declaration, constructor and increment. The counter had a complete unobscured view during its explanation and returns to view afterward. The terminal command and output stay clear. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
Total: 5000
```

The result is Total five thousand. Both starts happen before either join, and both joins complete before this read. The getter also follows the counter’s lock rule. This result does not reveal which worker finished first or whether using two workers made the job faster.

## 2:31–2:53 — Reason about a lost update

**On screen:** The full source and terminal result remain visible, with lines 4 through 9 selected again. Narration describes a possible unprotected lost update only as a reasoning example. No unsafe source is typed or executed; the displayed program still uses synchronized methods and still shows Total: 5000. Bottom captions do not cover the source or result.

A lost update means one write replaces another worker’s change because both computed from an earlier value. As a reasoning example only, two unprotected increments could both read zero and both write one. We did not run that unsafe case. With different counter objects, each job would update its own count; their separate locks would not coordinate one shared count.

## 2:53–3:10 — Transfer to seat reservation

**On screen:** The view moves closer to the selected SharedCounter while keeping the complete source and terminal result readable. The learner is asked to reason about a shared seat count; no seat-reservation program is typed or run. Captions appear below the result. The ending returns to a full source-and-terminal view for a short hold.

For a shared seat count, why should checking for a remaining seat and decreasing the count happen in one synchronized operation? Explain what could go wrong if they were separate calls, and why every caller must follow the same lock rule.

