# Transcript: Events and Model State

This CSC-239 Java demonstration runs a Seat Counter window in Workspace Desktop. It connects a reservation button to an ordinary Java object and shows the resulting label changes with pointer and keyboard input.

Gray parameter names beside arguments are editor hints, not extra source. The exact Java source is included below.

## 0:00–0:22 — Goal

**On screen:** The title introduces Events and Model State. Workspace opens Main.java with an empty editor while the goal is narrated. The source is then typed visibly.

We will connect a reservation button to an ordinary Java object and its visible count. Watch how an action changes the data, refreshes the label, and controls whether another reservation is available.

## 0:22–1:14 — Separate data and display

**On screen:** The complete 38-line source is readable. A selection covers the SeatCounter class and the construction of its model, Label and Button. The bottom captions leave the complete source unobscured. Gray argument hints are visible beside some values.

The complete Main.java source is:

```java
import javafx.application.Application;
import javafx.stage.Stage;
import javafx.scene.Scene;
import javafx.scene.control.Label;
import javafx.scene.control.Button;
import javafx.scene.layout.VBox;
import javafx.geometry.Insets;
class SeatCounter {
    private int remaining;
    public SeatCounter(int remaining) { this.remaining = remaining; }
    public int getRemaining() { return remaining; }
    public void reserve() {
        if (remaining > 0) { remaining--; }
    }
}
public class Main extends Application {
    @Override
    public void start(Stage primaryStage) {
        Stage stage = primaryStage;
        SeatCounter model = new SeatCounter(3);
        Label status = new Label("Remaining: " + model.getRemaining());
        Button reserve = new Button("Reserve one");
        reserve.setOnAction(event -> {
            model.reserve();
            status.setText("Remaining: " + model.getRemaining());
            reserve.setDisable(model.getRemaining() == 0);
        });
        VBox root = new VBox(12, status, reserve);
        root.setPadding(new Insets(20));
        stage.setTitle("Seat Counter");
        stage.setScene(new Scene(root, 380, 220));
        stage.show();
        System.out.println("Counter ready: " + model.getRemaining());
    }
    public static void main(String[] args) {
        launch(args);
    }
}
```

The model is the object that holds application state: SeatCounter owns remaining. The view displays that state through controls. A Button is a control that requests an action when activated. Here the Label displays the model’s count, and VBox places the label and button vertically.

## 1:15–1:37 — Register behavior for a future action

**On screen:** The editor selects lines 23 through 27: setOnAction and the three operations inside its lambda. All 38 source lines remain readable, with zero displayed errors or warnings. The editor joins the two characters of the lambda arrow into one visual arrow; the exact source in this transcript preserves its typed characters.

An action event is a notification that the button’s requested action occurred. Event-handler registration connects behavior to that future event. setOnAction registers our lambda; registration does not run its body. The lambda keeps references to the model and controls. Those local references stay the same while the objects can change.

## 1:37–1:52 — Predict before running

**On screen:** The selection clears and the complete source remains visible before the first run. The prediction caption appears below the source, followed by a quiet pause with no terminal result or window shown yet.

Predict the initial label and its value after three activations. What should happen on a fourth attempt? Trace the model update, label refresh, and button setting before running. Pause here.

## 1:52–2:16 — Observe the initial window

**On screen:** Workspace Run Java compiles and launches Main, then the view changes to Desktop. The decorated Seat Counter window shows Remaining: 3 above an enabled Reserve one button with a visible focus outline. Bottom captions sit below the window and leave both controls clear.

The verified command is:

```text
javac Main.java && java Main
```

Its initial console output is:

```text
Counter ready: 3
```

That message describes construction only. The later label changes are shown in the Desktop.

The window starts at Remaining three. Counter ready three is only the console’s initial report. The label will show later changes. This standalone Application uses start to build the interface; notebook examples use the supplied Fx support.

## 2:19–2:34 — Update and refresh

**On screen:** A native click on Reserve one changes the label to Remaining: 2. After the explanation, Tab is pressed while the count stays at two and the button remains outlined for keyboard focus. Captions stay below the window.

The first click leaves two. An event-driven update first changes the model, then setText refreshes the visible label. Keyboard focus selects the control that receives keyboard input. Use Tab to focus this button, then Space to activate it.

## 2:37–2:42 — Activate from the keyboard

**On screen:** A native Space activation changes the label to Remaining: 1. The button remains enabled. The following Space activation reaches Remaining: 0.

The keyboard activation leaves one. Activate again and check the boundary.

## 2:47–3:08 — Check the boundary

**On screen:** At Remaining: 0 the Reserve one button is visibly gray and disabled. A further native pointer attempt leaves zero unchanged. Tab and Space are then pressed and the label still shows zero. The separate source view explains the model condition as well as the button setting; the console message is not used to establish these later states. Alt+F4 closes the Seat Counter window, leaving the Desktop without it. The process completes with exit code zero before the recording returns to the editor.

Zero remains after further pointer and keyboard attempts. Control enablement allows or prevents an action according to state. setDisable blocks this button at zero, and the model’s own condition also protects its count. The event handler runs this short update on the JavaFX Application Thread, the sequence for interface work.

## 3:10–3:25 — Reflect on responsibilities

**On screen:** The view returns to the editor and selects the handler on lines 23 through 27. Lines 1 through 32 are visible above the terminal divider; the remaining six lines were visible in the earlier full-source views. The terminal displays the generated Java launch command and Counter ready: 3, followed by the returned prompt. Bottom captions briefly cover part of the generated launch command while the handler and initial output remain readable. The final quiet hold clears the caption. The question asks for reasoning about removing the label refresh; no code is changed.

If you removed only the label refresh, which state would still change and which display would become misleading? Explain why the model condition and button enablement serve different purposes.

