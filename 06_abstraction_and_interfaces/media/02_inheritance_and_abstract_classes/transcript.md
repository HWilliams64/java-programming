# Transcript: Inheritance and Abstract Classes

This CSC-239 demonstration uses Java 21 in the Workspace. It shares a name and initialization through an abstract superclass, then traces overridden behavior in a ReadingJob object.

## 0:00–0:20 — Goal

**On screen:** The title reads Inheritance and Abstract Classes, with the subtitle Share initialization and specialize behavior. The demonstration then opens Main.java in the Workspace.

A job planner can share a name and description while each kind of job defines its own time calculation. An abstract class holds that shared state and behavior, but cannot be constructed directly.

## 0:20–1:07 — Share state and specialize behavior

**On screen:** Main.java is typed in the editor. The completed 40-line source is visible. The selection highlights NamedJob and ReadingJob while the narration explains shared initialization and specialized behavior. Gray name: and pages: labels beside the constructor arguments are editor hints; they are not Java source text. Captions sit below the code during this explanation.

```java
abstract class NamedJob {
    private String name;
    public NamedJob(String name) {
        this.name = name;
    }
    protected String getName() {
        return name;
    }
    public String description() {
        return getName();
    }
    public abstract int minutes();
}
class ReadingJob extends NamedJob {
    private int pages;
    public ReadingJob(String name, int pages) {
        super(name);
        this.pages = pages;
    }
    @Override
    public String description() {
        return super.description() + " reading";
    }
    @Override
    public int minutes() {
        return pages * 2;
    }
    public String heading() {
        return "Job: " + getName();
    }
}
public class Main {
    public static void main(String[] args) {
        ReadingJob reading = new ReadingJob("Guide", 3);
        NamedJob job = reading;
        System.out.println(reading.heading());
        System.out.println(job.description());
        System.out.println("Minutes: " + job.minutes());
    }
}
```

ReadingJob extends NamedJob, making it a subclass. NamedJob is its superclass. The super constructor call initializes the name before pages is set. The description reuses superclass behavior. The heading reads the private name through a protected getter accessible here.

## 1:07–1:28 — Predict the three output lines

**On screen:** The selection moves to the object construction, shared reference and three print calls. All 40 source lines remain visible. The terminal has not opened, and no computed output appears. The request to predict is followed by a three-second pause with the caller still selected.

The abstract minutes declaration requires ReadingJob to supply a body. Both variables refer to the same object. The NamedJob reference can call its declared operations, and the object supplies overridden behavior. Predict the three lines, then pause.

## 1:28–1:45 — Execute and compare

**On screen:** The terminal opens beneath the source and the view enlarges the result. The command and all three output lines are clear. At the start of this explanation, the top caption overlaps part of the protected getter shown earlier. The ReadingJob methods and their bodies remain visible. The caller below the Main declaration is outside the smaller editor pane; it was fully visible during prediction. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
Job: Guide
Guide reading
Minutes: 6
```

The heading uses the stored name, so it prints Job: Guide. The overridden description adds reading to the superclass description. Three pages at two minutes each produce six minutes. Calls through job still use ReadingJob's implementations.

## 1:45–1:57 — Change the page count

**On screen:** The view returns to the full Workspace with the original output still visible. NamedJob and ReadingJob remain on screen; Main.main is below the editor pane. A bottom caption asks for a new prediction after changing the page count to zero. No code is changed and no answer to that prompt is shown. The final image holds for two seconds after the narration.

Change the page count to zero. Predict all three output lines. Explain which methods depend on the name and which method depends on pages.

