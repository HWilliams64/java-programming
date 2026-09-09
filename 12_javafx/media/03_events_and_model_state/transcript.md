# Transcript: Events and Model State

Welcome to this Java tutorial, where you'll learn to connect button actions to model state, refresh visible feedback, and check pointer and keyboard behavior.

These skills help applications respond consistently to user input while keeping their data and visible controls in agreement.

A campus workshop desk needs a booking counter. Each successful activation should reserve one available place. We'll begin with four places, then adapt the same behavior to the course's three-seat example.

We'll inspect the real window, use its button with both pointer and keyboard input, and try another activation at zero. The label should follow the model, and the button should stop offering reservations when no seats remain.

In the Workspace, we'll use Main.java and the supplied standalone JavaFX runner. The notebook uses the same kind of interface instructions inside its supplied Fx support. Here, closing the last window lets the separate program finish.

First, separate the booking rule from its display. SeatCounter will be our model: an ordinary Java object that owns the remaining count. Private state keeps other code from assigning the count directly. A getter lets the interface read it, and reserve provides the allowed update.

The constructor stores the starting number. The reserve method subtracts one only when remaining is greater than zero. That condition protects the model even if some caller invokes reserve without going through a button. The model contains no Label or other interface control.

The supplied Application runner gives us the start method and its primary Stage. Inside it, we'll create the model with four places, a Label that reads its initial value, and a Button labeled Book place.

These controls form the view: what the user sees and operates. Constructing a button does not reserve a place. The initial label reads the model once. It will not automatically reread the count whenever that count changes, so we must register behavior that refreshes it.

An action event notifies the program that a control was activated. setOnAction registers a callback, which is behavior JavaFX will call later. Our lambda receives the event and describes three steps: change the model, update the label, then update whether the button is enabled.

The arrow introduces the lambda body. Registering this body stores its behavior; it does not run these three statements now. The model and control references stay the same, while the objects they refer to can change. This uses the captured-reference rule from our earlier lambda lesson.

When called, reserve changes the model first. setText then builds the visible text from the updated getter value. Finally, setDisable receives whether the count equals zero. True disables this control; false leaves it enabled. Reversing these responsibilities can leave stale feedback even when the model changes correctly.

Arrange the label above the button in a VBox, using the spacing and padding from the preceding lesson. Attach that root to the Scene, set the separate window title, and show the Stage. The initial console report is outside the handler, so a later reservation will not print that report again.

Finish start and the supplied main entry point. The launch call begins this standalone application. Its short action handlers run on the JavaFX Application Thread, where our interface updates belong. We are not adding background work to this lesson.

Let's click Run to see the workshop counter. Four is the configured starting count. Registration should leave it unchanged until a person activates the button.

The window shows Places four above Book place. The console's initial report also says four. The handler is registered, but no reservation has occurred. We'll click the visible button once.

The label now shows three. That click requested an action; the handler changed the model, refreshed the label, and kept the button enabled. Keyboard focus identifies the control that receives keyboard input. After this click, Book place has focus, so Space can activate the same action.

Space reaches the same handler and leaves two. Focus and enablement answer different questions: which control receives the key, and whether that control permits an action. We'll activate twice more to reach the boundary.

The label reaches zero, and Book place is disabled. Let's try another pointer click on it. The visible zero should remain, because a disabled button does not dispatch this ordinary activation.

Zero remains. The disabled button prevents this user action, while the condition inside reserve protects the model if it is called directly at zero. These are two different checks. The visible window proves the control response; the direct-call rule comes from the model's condition.

We'll close this window before changing the starting inputs. The standalone process can now finish. A complete rerun constructs a fresh model and fresh controls; it does not continue the old counter.

For the original seat counter, start with three, use Remaining in the label, Reserve one on the button, and Seat Counter as the window title. The model class, handler order, layout, and scene size stay the same.

Before running, predict the initial report and label. Then trace one pointer click followed by two Space activations on the focused button. What should the label and button show afterward? What will another click attempt do? Pause and record your prediction before observing.

Now click Run and compare the actual three-seat counter with your prediction.

The window starts at Remaining three. No seat was used by registering the callback. We'll perform the pointer activation first, followed by the two keyboard activations.

Remaining is zero, and Reserve one is disabled. The label has followed the model after each action. Try the additional click and check whether any new reservation is allowed.

The disabled attempt leaves zero. The original console report is still the initial three, because it was printed during construction, outside the action handler. A useful check records both the visible states and which part of the program produces each report.

Close this window and run the unchanged program once more. A fresh model should restore three available seats and an enabled button.

The source is unchanged. Click Run again to check complete recreation.

The fresh Seat Counter is back at Remaining three with Reserve one enabled. The earlier disabled state belonged to the old controls. We'll close this last window after checking its initial display.

You connected an action event to an ordinary model, refreshed its view, and tested the disabled boundary with real input. For another limited resource, what belongs in the model's rule, and what feedback must the handler refresh? Explain how you would check the same action from the keyboard.
