# Transcript: Forms and Input Validation

Welcome to this Java tutorial, where you'll learn to validate form input before saving state, explain errors clearly, and support consistent mouse and keyboard submission.

These skills help applications accept useful requests while protecting previously accepted data when a person makes an invalid edit.

A campus equipment desk accepts quantities from one through five. We'll build an order form that starts with a proposed three, then restore the course example's starting text of two.

We'll submit a valid request, inspect two kinds of rejection, and recover with a valid entry. The window should explain each result. The notebook's separate model checks will establish which quantity remains saved.

We'll write Main.java in the Workspace and use the supplied standalone JavaFX runner. The notebook uses its supplied Fx support for the same interface instructions. Start with the imports for the window, controls, layout, and event-handler types.

First define QuantityModel, the ordinary object that owns accepted state. Its private quantity starts at zero to mean nothing has been saved. Zero is an initial marker, not an accepted request. A getter exposes the saved number without allowing callers to assign the field directly.

The save method receives proposed text. A candidate is a temporary value we can check before changing accepted state. Inside try, trim the surrounding spaces and attempt integer parsing. A valid integer can still be outside the allowed range, so that decision comes next.

The outside-range condition uses or: reject a candidate below one or above five. Returning from this branch leaves the saved field unchanged. We have not assigned quantity yet. A parsed zero reaches this decision, while a word cannot reach it because parsing fails first.

Only an accepted candidate should replace quantity. Then return a success message. If integer parsing failed, catch NumberFormatException and return a whole-number correction instead. Neither rejection path should assign the saved field.

Validation before mutation means checking a proposal before replacing stored state. Here, one assignment sits after the range check. The catch handles text such as a word, an empty string, or an integer too large for int. The method expects non-null field text; it does not define a separate null-input policy.

Next enter the supplied Application start method and construct a fresh model. Add a persistent Quantity label and a TextField beginning with three. A TextField is an editable single-line control. Its value remains a String even when the visible characters are digits.

The field's initial three is only a proposed request; creating or editing it does not save that number. Associate the visible label with its field using setLabelFor. Then create wrapping status text and the Save quantity button. The label should remain visible after the person changes or clears the input.

Control label association records which input the label describes. It complements visible placement rather than replacing keyboard testing. The status begins with Nothing saved. Visible validation feedback will later show either success or a useful correction sentence, so the result does not depend on color alone.

Submission is the deliberate request to read current field text and try saving it. We'll create one submit handler. EventHandler is JavaFX's functional interface for event handling, and ActionEvent is the type of notification this handler accepts. The lambda reads the field when invoked, asks the model to save, and displays the returned message.

The declaration supplies behavior without submitting now. Both registrations refer to the same submit variable: button activation and Enter in the field call that same behavior. Each call reads current text. Reading the field only during construction would keep an old value and miss later edits.

Arrange the field label, input, button, and status in a VBox. Use gap twelve and padding twenty, then show the Equipment Order window with a four-hundred-twenty by two-hundred-eighty content area. The final print reports the initial model quantity; it is outside the handler.

Finish the supplied start and main methods. Launch begins this standalone program. Its short callbacks run on the JavaFX Application Thread. They perform the parse, model decision, and visible update without waiting for another operation.

Click Run and inspect the difference between proposed text and saved state. The field should display three while the status still says Nothing saved. The initial console report should be zero.

The real Equipment Order window shows the persistent Quantity label, proposed three, Save quantity, and Nothing saved. We'll click Save quantity to request submission.

The feedback is Saved three. The handler read the field at activation, and the model accepted the candidate. Now replace the proposed text with cat. Editing the field alone should leave the existing feedback until another submission.

The field now contains cat while the status still shows the earlier success. This separates editing from submission. Click Save quantity to ask the model to check the new text.

The whole-number correction appears. Integer parsing rejected the word before the range decision. The source returns from catch without assigning quantity. That explains preservation of the earlier value, but the error label alone does not inspect the private field; use the notebook's getter checks for that evidence.

Zero produces the range correction. It can be parsed as an int, but it is not an accepted quantity. Both rejection paths preserve state by avoiding assignment. Now enter five and keep focus in the field. Pressing Enter should use the same submission behavior as the button.

Enter displays Saved five. The form still accepts a valid request after errors. Focus matters: Enter here belongs to the field; Tab can move to the button, where Space requests its action. The two registered routes share the model's rule and feedback operation.

Close this window before restoring the course example. The standalone process finishes. A complete new run creates another model and controls; it does not reuse the earlier saved five.

Restore the TextField's starting text to two and the window title to Quantity Form. Keep the model, accepted range, shared handler, and layout unchanged. Changing starting text still does not submit it.

Predict the initial console report, field text, and status separately. Then trace button submission of two, Enter submission of cat, button submission of zero, and Enter submission of five. Which decisions reject, and when can the saved field change? Pause and record your reasoning before observing.

Run the restored source and compare the actual Quantity Form with those predictions.

The form starts with proposed two and Nothing saved, while the console reports zero. Click Save quantity for the first request, then submit cat through Enter in the field.

The word receives the whole-number correction through Enter. The button and field use the same handler. Now submit zero with the button, followed by five with Enter, to compare range rejection with recovery.

The range correction was followed by Saved five. A status message is the latest feedback, not a live view of every model field. The initial console zero also remains a construction report. Separate model tests in the notebook check stored quantity after each rejected request.

Close the window and run the unchanged source once more. Its new model should return to the nothing-saved marker, even though the earlier window finished with a successful submission.

The fresh Quantity Form again shows proposed two and Nothing saved, with the initial console report zero. That is complete recreation, not a reset of the old form. Close this last window after checking its display.

You separated proposed text, validation feedback, and accepted state, then tested shared mouse and keyboard submission. For another campus form, what must be checked before assignment, and how would you prove that an invalid request preserves the last valid value? Keep the interface observations and model checks distinct.
