# Transcript: Layout and Readable Styling

This CSC-239 demonstration uses JavaFX in the Workspace and shows the actual application in the Workspace Desktop. A room notice combines a title, room row and wrapping instruction. The window is resized with native keyboard actions and then closed.

## 0:00–0:19 — Goal

**On screen:** The title card introduces Layout and Readable Styling. The Workspace editor is ready for Main.java.

Build a room notice that keeps its information readable when the window changes size. We will arrange its title, room and instructions, then test the real window in the Workspace Desktop.

## 0:19–1:11 — Arrange and style the notice

**On screen:** The complete program is typed and saved. The teaching view emphasizes the title, horizontal room row, wrapping instruction and vertical container. The row has 8 pixels between its children; the vertical container has 12 pixels between its children and 20 pixels of inner padding. Gray argument labels in the editor are hints, not extra source.

The complete source is:

```java
import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.layout.VBox;
import javafx.scene.layout.HBox;
import javafx.geometry.Insets;
public class Main extends Application {
    @Override
    public void start(Stage primaryStage) {
        Stage stage = primaryStage;
        Label title = new Label("Study Room");
        title.setStyle("-fx-font-size: 22px; -fx-font-weight: bold;");
        Label place = new Label("Room:");
        Label room = new Label("Lab A");
        HBox row = new HBox(8, place, room);
        Label note = new Label("Bring your course notes and leave the table ready for the next group.");
        note.setWrapText(true);
        VBox root = new VBox(12, title, row, note);
        root.setPadding(new Insets(20));
        stage.setTitle("Room Notice");
        stage.setScene(new Scene(root, 440, 220));
        stage.show();
        System.out.println("Room: " + room.getText());
        System.out.println("Wrapping: " + note.isWrapText());
    }
    public static void main(String[] args) {
        launch(args);
    }
}
```

A VBox arranges children vertically; an HBox arranges them horizontally. Spacing separates adjacent children. Padding, supplied by Insets, leaves space inside the container's boundary. The title's inline style is a Java String of CSS presentation declarations: each property has a colon, value and semicolon. Here they set font size and weight.

## 1:11–1:30 — Predict before running

**On screen:** The scene setup and two print statements are emphasized. The 440 by 220 values request the scene content area. The prediction pause occurs before the application starts.

The scene requests a content area of four hundred forty by two hundred twenty. Window borders and the title bar are separate. Predict the two console lines. When we narrow this window, will the note's line breaks stay in the same places? Pause and decide.

## 1:30–2:00 — Read the first window

**On screen:** The editor Run button starts the standalone application. The console shows the two initial lines below. The Workspace Desktop then shows the real Room Notice window. Study Room appears larger and bold; Room: and Lab A share a horizontal row. The complete instruction is visible in two lines: the first ends with “the”, and the second reads “next group.”

The standalone command represented by the Run action is:

```text
javac Main.java && java Main
```

The initial console output is:

```text
Room: Lab A
Wrapping: true
```

The console reports Lab A and wrapping enabled. In the notice, the horizontal room row sits between the title and instructions. Wrapping allows long text to use multiple lines within its available width. The title's larger, bold text marks its role without relying on color.

## 2:04–2:24 — Resize and inspect the full instruction

**On screen:** The native window is resized with Alt+F8, ArrowLeft, twelve ArrowRight presses and Enter. The measured native client width changes from 440 to 320 pixels. The full instruction still uses two lines, now breaking after “the” in “leave the”; the second line reads “table ready for the next group.” The word breaks change while all instruction text stays visible. After inspection, Alt+F4 closes the window and the process exits successfully. These later GUI actions do not add console output.

The native window is now narrower. The containers recalculate their layout, and the note breaks at different words. Its full instruction remains visible. Spacing still separates the sections, while padding keeps their content away from the edges. Resizing changes the view; it does not print a new construction report.

## 2:28–2:40 — Transfer and test

**On screen:** The Desktop view closes and the editor returns. The final question asks the learner to change the room text and test readability at a narrower window width.

If this notice moved to another room, which text would you change, and how would you test that the instructions remain readable in a narrower window?

