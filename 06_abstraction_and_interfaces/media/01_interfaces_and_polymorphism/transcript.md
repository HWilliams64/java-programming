# Transcript: Interfaces and Polymorphism

This CSC-239 demonstration uses Java 21 in the Workspace. It calls two implementations through the Labelled interface and traces how a shared default method obtains each object's label.

## 0:00–0:19 — Goal

**On screen:** The opening title reads Interfaces and Polymorphism, with the subtitle One contract, different label behavior. The Workspace then shows Main.java before typing begins. The title and opening narration state the goal without giving the output.

A campus sign can describe a room or a course through one shared operation. An interface names that contract, leaving each class to supply the details. This separation is abstraction.

## 0:19–1:00 — Define a contract and its implementations

**On screen:** Main.java is typed in the Workspace, starting with the interface and its default method, followed by RoomLabel and CourseLabel. A blue underline appears briefly while a private declaration is still incomplete during typing; it is gone in the completed source. The model view shows all 34 lines, with lines 1 through 26 selected while the interface and both implementations are explained. The required label declaration, default announcement body, matching public methods and Override annotations are readable. Bottom captions are below the source. Gray room: and code: labels next to constructor arguments are editor hints, not source text. The completed editor shows zero errors and zero warnings.

```java
interface Labelled {
    String label();
    default String announcement() {
        return "Ready: " + label();
    }
}
class RoomLabel implements Labelled {
    private String room;
    public RoomLabel(String room) {
        this.room = room;
    }
    @Override
    public String label() {
        return "Room " + room;
    }
}
class CourseLabel implements Labelled {
    private String code;
    public CourseLabel(String code) {
        this.code = code;
    }
    @Override
    public String label() {
        return "Course " + code;
    }
}
public class Main {
    public static void main(String[] args) {
        Labelled[] signs = {new RoomLabel("Lab A"), new CourseLabel("CSC-239")};
        for (Labelled sign : signs) {
            System.out.println(sign.announcement());
        }
    }
}
```

Labelled declares a public label operation without a body. Each class uses implements and supplies its own matching public method. The Override annotation asks the compiler to check that match. A default method includes a body that these classes share.

## 1:01–1:18 — Predict the two announcements

**On screen:** The highlight moves to lines 29 through 31: an array with a RoomLabel and a CourseLabel, followed by one enhanced for loop calling announcement. The source briefly softens as the highlight changes, then stays clear through the prediction and pause. All 34 lines remain visible, including the interface and both label implementations. The bottom captions leave the caller and source unobscured. No terminal output appears before the learner prediction. The three-second pause holds the selected caller with the caption cleared.

The array holds Labelled references to different kinds of objects. The same announcement call uses each object's label implementation. That is polymorphism. Predict both output lines in array order, then pause.

## 1:18–1:36 — Execute and compare

**On screen:** The terminal opens, and the camera moves toward the successful compile-and-run result. Both announcement lines and the returning command prompt are clear. The top of the editor is partly outside the enlarged view, but the default announcement body, both label method bodies, constructor arguments and caller loop remain visible. Top captions overlap part of the RoomLabel class declaration and its room field, leaving the method bodies and terminal output clear. The complete source was unobscured during modeling and prediction. No compilation error or stale source diagnostic is visible. The terminal runs `javac Main.java && java Main`. It succeeds and prints:

```text
Ready: Room Lab A
Ready: Course CSC-239
```

The first announcement names Room Lab A. The second names Course CSC-239. Both begin with Ready because they share the default method. Each call inside that method reaches the label implementation of the current object.

## 1:36–1:49 — Change the room argument

**On screen:** The full Workspace view returns with the terminal still open. The interface, default body, both implementing classes, constructor arguments and loop are readable above the same two output lines. Only the three closing-brace lines at the end of Main.java are below the shortened editor pane; the complete source appears earlier and is reproduced here. The bottom caption does not cover the source or results. Compiled class files now appear in the explorer. After the final question, the caption clears and the view holds for two seconds. The status counters show zero errors and zero warnings.

Change the room's constructor argument to Lab B. Predict which announcement changes. Why can the same loop still announce both objects without checking their classes?

