# Transcript: Forms and Input Validation

This CSC-239 demonstration uses JavaFX in the Workspace and shows the actual application in the Workspace Desktop. A labeled quantity form explains rejected input and accepts a later valid submission. Button clicks and keyboard input use the same validation method.

## 0:00–0:24 — Goal

**On screen:** The title card introduces Forms and Input Validation. The Workspace editor is ready for Main.java.

Build an equipment quantity form that explains rejected input while preserving the last valid saved value. We will test the actual controls in the Workspace Desktop with both the button and keyboard.

## 0:24–2:33 — Validate before saving

**On screen:** The complete program is typed and saved. The teaching view highlights QuantityModel. Its quantity field starts at 0. The save method trims and parses the text into a separate candidate, returns an explanation for a value outside 1 through 5, and assigns quantity only after those checks. Gray argument labels in the editor are hints, not extra source.

The complete source is:

```java
import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.control.Button;
import javafx.scene.layout.VBox;
import javafx.geometry.Insets;
import javafx.scene.control.TextField;
import javafx.event.ActionEvent;
import javafx.event.EventHandler;
class QuantityModel {
    private int quantity;
    public QuantityModel() { quantity = 0; }
    public int getQuantity() { return quantity; }
    public String save(String text) {
        try {
            int candidate = Integer.parseInt(text.trim());
            if (candidate < 1 || candidate > 5) {
                return "Use a quantity from 1 to 5.";
            }
            quantity = candidate;
            return "Saved: " + quantity;
        } catch (NumberFormatException error) {
            return "Enter a whole number from 1 to 5.";
        }
    }
}
public class Main extends Application {
    @Override
    public void start(Stage primaryStage) {
        Stage stage = primaryStage;
        QuantityModel model = new QuantityModel();
        Label fieldLabel = new Label("Quantity (1 to 5)");
        TextField input = new TextField("2");
        fieldLabel.setLabelFor(input);
        Label status = new Label("Nothing saved.");
        status.setWrapText(true);
        Button save = new Button("Save quantity");
        EventHandler<ActionEvent> submit = event -> status.setText(model.save(input.getText()));
        save.setOnAction(submit);
        input.setOnAction(submit);
        VBox root = new VBox(12, fieldLabel, input, save, status);
        root.setPadding(new Insets(20));
        stage.setTitle("Quantity Form");
        stage.setScene(new Scene(root, 420, 280));
        stage.show();
        System.out.println("Saved quantity: " + model.getQuantity());
    }
    public static void main(String[] args) {
        launch(args);
    }
}
```

QuantityModel holds the saved state. The candidate is a proposed value, separate from that state. Trim removes surrounding spaces, and parseInt attempts a whole number. A parse failure produces a correction message. A parsed number outside one through five returns the range message before the assignment. Only an accepted candidate replaces quantity.

## 2:34–2:58 — Connect the labeled form

**On screen:** The teaching view highlights the label, input, status and shared handler. The visible label says Quantity (1 to 5), and setLabelFor associates it with the text field. The input starts with 2; the status starts with Nothing saved. Both controls use the same handler. A vertical container places the label, field, button and status in order, with spacing of 12 and padding of 20. The scene requests a 420 by 280 content area.

A TextField holds editable text. Its associated Label states the allowed range; setLabelFor connects that label to its input. Submission is the deliberate action that reads the current text and asks the model to save it. One EventHandler is registered with both the button and the field. Button activation and Enter therefore use the same validation and visible feedback.

## 2:58–3:16 — Predict before running

**On screen:** The complete program remains in the editor. A prediction pause occurs before the application starts. The question separates the text already in the field from the value saved in the model.

The field starts with two, but no submission has happened. Predict the initial console line. After saving two, should a word, zero or six replace the saved value? Trace the returns and assignment before running. Pause and decide.

## 3:16–3:39 — Read the initial form

**On screen:** The editor Run button starts the standalone application. The console shows the single initial line below. The Workspace Desktop then shows the real Quantity Form window. Its field contains 2, the button says Save quantity, and the visible status says Nothing saved.

The standalone command represented by the Run action is:

```text
javac Main.java && java Main
```

The initial console output is:

```text
Saved quantity: 0
```

The initial console reports saved quantity zero. The field contains two and the status says nothing saved. Text waiting in a field is not yet saved model state.

## 3:43–3:50 — Submit a valid value

**On screen:** A native click activates Save quantity. The field still contains 2 and the visible status becomes Saved: 2.

The button submission now displays Saved two. We will replace the input with a word and submit again.

## 4:02–4:13 — Reject a word

**On screen:** The input is selected and replaced with cat. A native button click changes the status to Enter a whole number from 1 to 5. The word remains visible so the learner can connect the rejected input with its explanation.

The form asks for a whole number from one to five. Parsing failed before the assignment, so the saved value remains two. Now test the two values just outside the allowed range.

## 4:24–4:26 — Reject zero

**On screen:** The input is replaced with 0 and the button is clicked. The visible status reads Use a quantity from 1 to 5.

Zero receives the range message.

## 4:37–4:53 — Reject six and return to the field

**On screen:** The input is replaced with 6 and the button is clicked. The same range message appears. A native Shift+Tab action then returns focus from the button to the field, where the text is selected. The saved value is not displayed separately in this form; the highlighted model code explains why the rejected values do not reach its assignment.

Six receives the same range message. Both inputs were numbers, but neither reached the assignment. The feedback changes while the saved value stays two. Shift Tab returns keyboard focus to the field. Replace its text with five and press Enter.

## 5:01–5:13 — Submit with Enter

**On screen:** The focused field is replaced with 5. A native Enter key press changes the status to Saved: 5. The field retains keyboard focus. Alt+F4 then closes the window, and the standalone process exits successfully. These later actions add no console lines.

Enter displays Saved five through the shared handler. A valid submission still works after the errors. The console remains the initial report; the status label shows these later results.

## 5:15–5:30 — Transfer and test

**On screen:** The Desktop view closes and the editor returns to the model. The validation checks and later assignment are highlighted. The final question asks the learner to reason about assignment order and choose a sequence of submissions to test it.

If you moved the quantity assignment before the range check, what saved value would survive an invalid attempt? Choose a valid, invalid, then valid sequence to test your explanation.

