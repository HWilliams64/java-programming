# Transcript: JUnit Behavior Tests

This CSC-239 demonstration uses Java 21 and JUnit Jupiter 5.13.4 in the Workspace.

A JAR is an archive file containing library code. This recording uses the pinned `junit-platform-console-standalone-1.13.4.jar`, which includes the JUnit test tools. It was copied from a retained local file into the Workspace. The terminal verifies its SHA-256 checksum, a fingerprint of the file contents, before compilation. A relative link in the `lib` folder points the editor to the same file. The notebook loads the dependency in its separate setup cell.

The `-cp` option sets the classpath, where Java finds application and library classes. The run command includes `.` for the current folder and the JUnit JAR.

## 0:00–0:27 — Goal

**On screen:** A title card introduces JUnit Behavior Tests. The Workspace then shows an empty Main.java editor, the pinned JAR in the file tree, and a successful checksum check in the terminal. The caption defines a unit test. No test counts have been revealed.

A unit test is an automated check of a small behavior. We will check a label calculator with normal, zero, and negative inputs. JUnit Jupiter supplies the test tools. It is an external dependency, a library added beyond Java's standard library. The classpath tells Java where to find it.

## 0:27–1:32 — Read the calculator

**On screen:** The source is typed into Main.java. The view selects LabelTools on lines 10–17: the negative-input guard, exception message, and multiplication return are readable. Imports remain above it; part of the test class appears below.

The complete source is:

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.Assertions;
import org.junit.platform.engine.discovery.DiscoverySelectors;
import org.junit.platform.launcher.Launcher;
import org.junit.platform.launcher.LauncherSession;
import org.junit.platform.launcher.LauncherDiscoveryRequest;
import org.junit.platform.launcher.core.LauncherDiscoveryRequestBuilder;
import org.junit.platform.launcher.core.LauncherFactory;
import org.junit.platform.launcher.listeners.SummaryGeneratingListener;
class LabelTools {
    public static int labelCount(int groups, int kits) {
        if (groups < 0 || kits < 0) {
            throw new IllegalArgumentException("Counts must be nonnegative.");
        }
        return groups * kits;
    }
}
class LabelToolsTest {
    public LabelToolsTest() { }
    @Test
    public void positiveCounts() {
        Assertions.assertEquals(6, LabelTools.labelCount(2, 3));
    }
    @Test
    public void zeroGroups() {
        Assertions.assertEquals(0, LabelTools.labelCount(0, 3));
    }
    @Test
    public void negativeGroups() {
        try {
            LabelTools.labelCount(-1, 3);
            Assertions.fail("Expected IllegalArgumentException");
        } catch (IllegalArgumentException problem) {
            Assertions.assertEquals("Counts must be nonnegative.", problem.getMessage());
        }
    }
}
public class Main {
    public static void main(String[] args) {
        LauncherDiscoveryRequest request = LauncherDiscoveryRequestBuilder.request()
            .selectors(DiscoverySelectors.selectClass(LabelToolsTest.class)).build();
        SummaryGeneratingListener listener = new SummaryGeneratingListener();
        try (LauncherSession session = LauncherFactory.openSession()) {
            Launcher launcher = session.getLauncher();
            launcher.registerTestExecutionListeners(listener);
            launcher.execute(request);
        }
        System.out.println("Succeeded: " + listener.getSummary().getTestsSucceededCount());
        System.out.println("Failed: " + listener.getSummary().getTestsFailedCount());
    }
}
```

LabelTools multiplies the two counts and rejects negative inputs. The tests below describe what callers should observe.

## 1:32–2:00 — Read the behavior tests

**On screen:** The view scrolls to and selects the complete LabelToolsTest class on lines 18–37. All three test methods, their inputs, assertions, the fail call, specific catch and message check are readable. Earlier calculator lines are partly outside the view. The caption sits below the editor focus.

The Test annotation marks a method for JUnit to discover and run. These public, nonstatic methods check separate behaviors. An assertion reports failure when behavior differs from the expectation. In assertEquals, the expected value comes first and the actual result second. For the negative input, fail reports failure if the call returns normally. The catch handles only IllegalArgumentException and checks its message. Each test supplies its own inputs.

## 2:01–2:24 — Follow the supplied runner

**On screen:** The view selects the complete Main runner on lines 38–51. The class selection, summary listener, launcher session, registration, execution and both final print statements are readable. The earlier tests are partly outside the view.

A test runner finds selected tests, executes them, and collects results. LabelToolsTest dot class is a class literal: it refers to the class itself. The request selects that class, and a summary listener collects outcomes. The supplied launcher runs the request inside a session that closes automatically. The final print statements read the passed and failed counts.

## 2:25–2:36 — Predict the summary

**On screen:** The view returns to all three selected test methods and asks the learner to predict both counts. A three-second pause follows. The terminal still shows only the earlier checksum result; the JUnit summary has not appeared.

Predict both counts before running. Trace each test, including what happens if the negative call returns normally. Pause here.

## 2:36–2:54 — Run and interpret the summary

**On screen:** The terminal displays the compilation and run command, then Succeeded: 3 and Failed: 0. Both output lines remain readable. The terminal-focused zoom crops earlier source, and the upper result caption briefly overlaps the test-class heading and constructor; all three test bodies remain readable and were shown fully in the preceding view. The terminal runs:

```text
javac -cp junit-platform-console-standalone-1.13.4.jar Main.java && java -cp .:junit-platform-console-standalone-1.13.4.jar Main
```

It reports:

```text
Succeeded: 3
Failed: 0
```

The summary reports three successes and zero failures. The exception check counts as a successful test because the expected exception occurred and its message matched. Read both counts: this runner can return normally even when a test fails.

## 2:54–3:15 — Check that a test can fail

**On screen:** The view returns to the selected complete test class while the successful summary remains below. The narration asks the learner to change the first expected value, predict and run, restore it, and rerun. These edits are a learner task and are not performed in this recording. The final hold retains the tests and actual summary.

A regression test cycle keeps a behavior check, confirms it can fail, and reruns it after repair. Change the first expected value from six to seven. Predict both counts, run it, then restore six and run again. What evidence shows this check detects the wrong expectation?

