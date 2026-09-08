# Transcript: JavaFX Windows in the Workspace

This CSC-239 demonstration connects a JavaFX window to its visible content in Grader Than Workspace. It shows a real Desktop window, closes it, then starts a new standalone process to reopen it. The notebook uses its supplied runner to keep the JavaFX runtime available between examples.

Gray parameter labels in the editor are hints, not extra source. The exact Java appears below.

## 0:00–0:20 — Goal

**On screen:** The title card names JavaFX Windows in the Workspace. The IDE opens Main.java with the generated starter cleared; the goal caption appears below the empty editor.

We will build a graphical user interface: a visible window with content. Our goal is to connect its parts, then close and reopen it in Workspace Desktop.

## 0:20–0:57 — Connect the window and its content

**On screen:** The recording types the complete 22-line Main.java source. All imports, the Application subclass, start method, window construction and main method are visible. Lines 8–15 are highlighted to connect the Stage, Scene, StackPane and Label.

The complete source is:

```java
import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.layout.StackPane;
public class Main extends Application {
    @Override
    public void start(Stage primaryStage) {
        Stage stage = primaryStage;
        Label message = new Label("Welcome to CSC-239");
        StackPane root = new StackPane(message);
        Scene scene = new Scene(root, 420, 220);
        stage.setTitle("Course Welcome");
        stage.setScene(scene);
        stage.show();
        System.out.println("Window: " + stage.getTitle());
        System.out.println("Message: " + message.getText());
    }
    public static void main(String[] args) {
        launch(args);
    }
}
```

A Stage is the native window. A Scene connects it to its content. The Label displays text, and StackPane is the layout container that places that label. Together, the parent and child form a scene graph, a tree of visible elements.

## 0:57–1:08 — Predict the visible result

**On screen:** The complete saved source remains visible without output. Captions ask about title text, label text and placement, followed by a quiet prediction pause.

Predict which text appears in the title bar and which appears inside the window. Where will the label appear? Pause before running.

## 1:08–1:32 — Inspect the Desktop window

**On screen:** The view switches from the IDE to the actual Workspace Desktop. A decorated window titled Course Welcome contains the centered text Welcome to CSC-239. Bottom captions remain below the window and do not cover its title or label. The Run Java control starts the standalone program. The verified compile-and-run command is:

```text
javac Main.java && java Main
```

The initial console output is:

```text
Window: Course Welcome
Message: Welcome to CSC-239
```

The output describes the initial state; the Desktop shows the actual window.

Course Welcome is the window title. Welcome to C S C two thirty-nine is the label. StackPane centers that child in the scene. The console reports this initial state. The visible window is on the Desktop.

## 1:32–1:41 — Close the standalone program

**On screen:** After the close prompt, Alt+F4 removes the window. The empty Desktop is visible briefly, then the IDE returns with the two expected console lines and a returned prompt.

Close the native window. This standalone application's process finishes when its last window closes.

## 1:41–2:13 — Reopen in a new process

**On screen:** Running again opens a new Course Welcome window with the same centered welcome label. The narration explains the standalone Application/start/launch lifecycle and contrasts its process lifetime with the supplied notebook support. The new process reports the same two initial output lines. Alt+F4 closes this window too, and the process exits successfully.

Running the command again starts a new process and creates a new window. Application supplies the runner: launch begins it, and start builds the interface on the JavaFX Application Thread, its sequence for interface work. Notebook examples instead use the supplied Fx support, which keeps JavaFX available after a window closes.

## 2:13–2:25 — Choose what to change

**On screen:** The IDE returns with both completed output pairs. The source lines that create the Label and set the Stage title are highlighted for the learner question. The brief close-up keeps all source lines visible; lower terminal history is partly outside that close-up and is visible again in the final full view.

Which object would you change to replace the welcome message, and which object would you change to rename the window? Explain your choices before editing.

