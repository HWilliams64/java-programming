# Transcript: Starting and Joining Threads

This CSC-239 demonstration uses Java 21 in the Workspace. Two counting jobs own separate totals. The caller starts both threads, joins both, then reports their completed results. The printed order does not establish which worker finished first.

Gray parameter names beside some arguments are editor hints. They are not part of the exact source below.

## 0:00–0:18 — Goal

**On screen:** The title card says Starting and Joining Threads, followed by a blank Main.java editor in the Workspace.

We will start two counting jobs, then wait until both results are ready. A thread is a separate path of execution within a Java process.

## 0:18–0:52 — Give each worker its own state

**On screen:** The complete program is typed. A highlight selects CountJob, its separate limit and total fields, its counting loop and getTotal reader. All source lines remain visible.

The complete source is:

```java

public class Main {
    public static void main(String[] args) throws InterruptedException {
        class CountJob implements Runnable {
            private int limit;
            private int total;
            public CountJob(int limit) { this.limit = limit; this.total = 0; }
            @Override
            public void run() {
                for (int index = 0; index < limit; index = index + 1) {
                    total = total + 1;
                }
            }
            public int getTotal() { return total; }
        }
        CountJob first = new CountJob(3);
        CountJob second = new CountJob(2);
        Thread firstWorker = new Thread(first);
        Thread secondWorker = new Thread(second);
        firstWorker.start();
        secondWorker.start();
        firstWorker.join();
        secondWorker.join();
        System.out.println("First: " + first.getTotal());
        System.out.println("Second: " + second.getTotal());
        System.out.println("Workers alive: " + (firstWorker.isAlive() || secondWorker.isAlive()));
    }
}

```

Runnable supplies work through its run method. Each CountJob owns a separate total. Its loop increases that total until it reaches the job's limit.

## 0:52–1:09 — Start both, then join both

**On screen:** A highlight selects the two job objects, their Thread objects, both start calls and both join calls. The caller prints the results below those joins.

Each start schedules work on a new thread. Calling run directly would be an ordinary call on the current thread. We start both workers before joining either. Each join waits for its own target to finish. The execution paths may take turns or run at the same time.

## 1:09–1:23 — Predict the result

**On screen:** The complete code remains visible with no program output yet. A pause gives you time to predict the results before the command runs.

Predict the two totals and whether either worker is alive when the last line prints. Does the first printed result prove that worker finished first? Pause before running.

## 1:23–1:42 — Run and interpret the result

**On screen:** The terminal shows the completed command and the three exact output lines. A closer view keeps both join calls and the output readable. The prompt has returned. The terminal runs:

```text
javac Main.java && java Main
```

It reports:

```text
First: 3
Second: 2
Workers alive: false
```

The totals are three and two, and neither worker is alive. Both joins returned normally before the caller read the results. The caller prints First before Second. This output does not establish which worker finished first or show a speed advantage.

## 1:42–1:54 — Create new workers for another attempt

**On screen:** The two Thread declarations, both starts and both joins are highlighted while the completed output remains visible.

A Thread can be started once. A new attempt needs new Thread objects. Rerunning this complete program creates both jobs and their workers again, so each total begins at zero.

## 1:54–2:06 — Transfer the reasoning

**On screen:** The job limits and the caller code are highlighted. The completed original output remains visible while the final question asks you to reason about changing only the second limit.

If only the second limit becomes five, which output lines would change, and which would stay the same? Explain why both join calls still matter.

