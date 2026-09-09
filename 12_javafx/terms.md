**Native JavaFX window** - A window displayed on the operating-system desktop. It has a title bar, can receive keyboard focus, and has a close control. Example: `Stage stage = new Stage()`. Notebook stdout cannot prove that a window is actually visible.

**Stage** - The top-level window object that owns a title and can show or close its content. Example: `stage.setTitle("Course Welcome")`. A Stage is not a child node in its scene graph.

**Scene** - The connection from a window to the root of its content. Example: `stage.setScene(scene)`. Attaching content and calling show are separate steps.

**Scene content dimensions** - The requested width and height of the content area, measured in pixels. Example: `new Scene(root,420,220)`. A decorated window also includes borders and a title bar.

**Scene graph** - The parent-child tree of visual nodes inside a Scene. Example: `StackPane root = new StackPane(message)`. Stage and Scene connect to the graph but are not child nodes in it.

**Node** - A visual object within the scene graph. Example: `Label message = new Label("Open")`. Not every object in a GUI program is a node; ordinary models are separate.

**Root node** - The node from which the Scene’s parent-child content tree begins. Example: `new Scene(root,420,220)`. Root names a position in this tree, not a required variable spelling.

**Label** - A control that presents text the user does not edit directly. Example: `message.getText()`. Its text is separate from the Stage title.

**Layout container** - A parent node that places its children in available space. Example: `new StackPane(message)`. Constructing a layout does not itself show a native window.

**StackPane** - A layout that can stack children; this lesson centers one Label. Example: `StackPane root = new StackPane(message)`. The one-child example does not teach overlapping multi-child layout.

**JavaFX runtime lifecycle** - Starting the toolkit, using its windows and ending its runtime. Example: `Fx.start()`. Closing the last window differs from ending the toolkit in this supplied notebook setup.

**Fx.start** - A supplied course method that initializes the notebook toolkit if needed and keeps it available after windows close. Example: `Fx.start()`. This is course support, not a JavaFX API method.

**Fx.closeWindows** - A supplied course method that hides currently showing windows owned by this notebook kernel before another example. Example: `Fx.closeWindows()`. Use a dedicated lesson kernel; the helper does not identify unrelated tutorial windows by name.

**Thread** - A path of execution that carries out program instructions. JavaFX uses a particular thread for live interface work. Recognizing the interface thread does not require creating a background worker in this lesson.

**JavaFX Application Thread** - The execution path responsible for live JavaFX interface work. Example: `Fx.run(() -> { stage.show(); })`. Keep live reads as well as writes on this thread and keep work short.

**Runnable** - An interface for an action whose run method takes no arguments and returns no result. A compatible lambda supplies the action passed to the course Fx.run helper. Example: `Fx.run(() -> { System.out.println(message.getText()); })`. Creating a lambda does not execute its action. The helper arranges execution on the JavaFX Application Thread; Runnable alone does not choose a thread.

**Fx.run** - A supplied course method that runs a short interface operation on the application thread and waits for that operation to finish. Example: `Fx.run(() -> { System.out.println(message.getText()); })`. Completion does not mean later user interaction has been tested.

**VBox** - A layout container that arranges its children from top to bottom. Example: `new VBox(12, title, row, note)`. A nested HBox counts as one direct VBox child.

**HBox** - A layout container that arranges its children side by side in the specified order. A nested layout places one layout container inside another, as when this row becomes one child of the outer VBox. Example: `new HBox(8, place, room)`. The numeric gap is separate from the order of child arguments.

**Layout spacing** - The gap between adjacent children of one container. Example: `new VBox(12,title,row,note)`. Spacing is not space around the outside edges.

**Container padding** - Space between a container’s edge and its child content. Example: `root.setPadding(new Insets(20))`. Changing padding can reduce content width without directly changing interchild gaps.

**Insets** - A value object that holds the amounts of space at the top, right, bottom, and left edges. Example: `new Insets(20)`. This constructor supplies the same amount on each edge.

**Text wrapping** - A setting that allows a Label to use extra lines when its allocated width is limited. Example: `note.setWrapText(true)`. The setting cannot guarantee all words fit at every possible window size.

**JavaFX inline style** - A Java String containing presentation settings for one node. Example: `title.setStyle("-fx-font-size: 22px; -fx-font-weight: bold;")`. The quoted CSS uses property:value; syntax, not Java assignment syntax.

**CSS declaration** - A presentation property, colon, value and semicolon inside the style String. Example: `-fx-font-weight: bold;`. These are JavaFX properties; no external stylesheet is required here.

**Resize-aware layout** - Containers recalculate placement and allocated size when the native window is resized. Example: `A Room Notice content area resized from 440 to 320 pixels wide`. Verify all original words in actual views; do not shorten text to hide clipping.

**Button** - A control whose activation requests an action. Example: `new Button("Reserve one")`. Construction does not execute the requested reservation.

**Action event** - A notification that a control’s requested action occurred. Example: `ActionEvent`. Pointer and keyboard activation can request the same action.

**Event-handler registration** - The step that connects behavior to a future event. Example: `reserve.setOnAction(event -> { model.reserve(); })`. Registration does not immediately run the lambda body.

**Callback** - Behavior that JavaFX calls when the matching event occurs. Example: `event -> status.setText(...)`. Its short body runs later on the application thread.

**Model** - An ordinary Java object that holds authoritative application state and operations. Example: `SeatCounter model = new SeatCounter(3)`. Do not recover the count by parsing a sentence from the Label.

**View** - Controls that present the model’s state to the user. Example: `Label status = new Label("Remaining: " + model.getRemaining())`. A model mutation does not automatically rewrite this Label’s text.

**Event-driven state update** - Change the model in response to an event, then refresh the interface from that state. Example: `reserve→setText→setDisable`. Updating only the model or only the Label can leave the program inconsistent.

**Control enablement** - A control setting that permits or prevents a user action according to the current state. Example: `reserve.setDisable(model.getRemaining() == 0)`. Keep the model guard too; disabled appearance is not the only boundary feedback.

**Keyboard focus** - The current destination of keyboard input. Example: `Shift+Tab moves focus back to Add two`. Focus is different from being enabled.

**Keyboard activation** - Request an action from a focused control. Example: `Space activates the focused button`. Pressing a key in the notebook editor is not native GUI interaction.

**TextField** - A single-line control holding editable text. Example: `new TextField("2")`. Digits in this field remain a String until parsed.

**Form submission** - A deliberate action that reads current field text and attempts to apply it. Example: `input.getText() inside submit`. Creating or editing the field alone does not save its contents.

**Candidate value** - A proposed parsed value checked before the saved field is changed. Example: `int candidate = Integer.parseInt(text.trim())`. A parse success does not establish that the number meets the allowed range.

**Validate before mutation** - A validation order that rejects an unacceptable candidate before replacing valid stored state. Example: `if (candidate < 1 || candidate > 5) return ...`. The initial zero marker is not a valid submitted quantity in this model.

**Saved model state** - The last accepted value held by the model’s private field. Example: `model.getQuantity()`. An error screenshot cannot establish which value remains saved.

**Visible validation feedback** - Text that confirms success or explains how to correct a request. Example: `Enter a whole number from 1 to 5.`. The status can change on rejection while the saved value stays unchanged.

**Control label association** - An explicit relationship between a visible descriptive Label and its input. Example: `fieldLabel.setLabelFor(input)`. The relationship alone is not proof of every accessibility feature or keyboard behavior.

**EventHandler<ActionEvent>** - The type of behavior that accepts an action-event notification. Example: `EventHandler<ActionEvent> submit = event -> ...`. EventHandler is an interface and ActionEvent is a class, not Java keywords.

**Shared submission handler** - One behavior registered for button action and Enter in the field. Example: `save.setOnAction(submit); input.setOnAction(submit);`. The handler must read current field text each time; separate registrations should not acquire different rules.
