# Reading and Writing Binary Records — video transcript

## Narration

Welcome to this Java tutorial, where you'll use serialization and deserialization to save and restore object state, then check a restored value's type before using it.

These skills let applications preserve settings and records between runs while checking that recovered values are the types their code expects.

A campus equipment desk keeps the location label lab in a small card object. We will save that card to a private temporary file and restore its label. The reader must check that it received the expected card before calling the method that returns the label.

Our report should show Label, followed by lab, confirming that the desk recovered its saved location. Then we'll change the stored value and predict how the same reader responds.

Now that we're in the Workspace, let's open Main.java and build the card's round trip.

We need object input and output streams, the serialization marker, and the familiar Files and Path types. Add these imports so their short names are available in the program.

Next, define the card with its String label, a constructor to set that field, and a getter to read it. Mark the class as supporting serialization and give it an explicit version identifier.

Serializable is a marker interface: it declares support without requiring a serialize method. Our String field supports serialization too. The static version identifier belongs to the class, final prevents reassignment, and long is its whole-number type. The L suffix makes the value a long literal. Matching that identifier does not make every class change compatible.

Main holds the conventional entry method for this Workspace program. We will declare the checked exceptions that may leave it, create one private temporary file, and start the outer cleanup structure.

The throws declaration allows I/O and class-lookup failures to leave main; it does not handle them. CreateTempFile creates an empty file and returns its Path. We retain that location for both stream phases and deletion. A dot bin suffix labels the name but does not select the stored format.

Open byte output and wrap it in an object output stream. Pass a new LabelCard holding lab to the writer, then finish the resource block before reading.

WriteObject receives the card and writes its supported state representation. It does not save Java source, a running method, or the notebook kernel. The version identifier is class compatibility information, separate from the ordinary instance label. Closing this wrapper also closes the underlying byte output.

Now open byte input, wrap it in an object input stream, and restore the saved value. Keep the initial result in an Object variable so we can check what actually came back.

ReadObject reconstructs the saved state using the compatible class available to this program. Its declared result type is Object, Java's common superclass for class instances. That reference can hold the restored card, but its declared type does not expose the card's particular getter.

Check whether the returned value is a LabelCard. In that matching branch, cast the reference to LabelCard and call its getter. Otherwise, report an unexpected type.

Instanceof checks the actual value and is false for null. The cast then gives us a LabelCard reference to the same restored object; it does not create another card or convert a String into one. A cast on an incompatible non-null value can throw ClassCastException. The matching guard keeps that attempt out of this reader's mismatch path.

Finish the reader block, then put deletion in the outer finally block. Closing releases the stream; deletion removes the file that this complete run owns.

The reader closes before finally attempts deletion, including when the protected work fails. Deletion can itself report an I/O error. With the complete supported-card path in place, let's click Run and inspect the actual report.

The report shows Label, followed by lab. The restored value passed the card check, and its getter returned the saved text. This verifies the restored label; it does not mean the restored card is the original in-memory instance.

For a second run, write the String lab directly instead of constructing a card. Keep the same class definition, LabelCard check, cast, and report branches. This changes the actual stored value, not what the reader expects.

Before running, predict which report branch will execute. What type will the restored non-null value have, and will the cast or getter run? Pause here and explain your prediction from the value actually passed to the writer.

Let's click Run to test that prediction against the reader's actual behavior.

The program reports an unexpected object type. The String was valid saved data, but it did not satisfy this reader's LabelCard requirement. The false guard skipped both the cast and getter. Declaring LabelCard elsewhere did not turn the written String into a card.

You saved supported state, restored it with a compatible class, and separated the Object result, runtime type check, and reference cast. Those steps let the desk recover a useful label while reporting a controlled mismatch. The notebook practice asks you to complete this agreement, repair a wrong guard, and build your own tag-card reader.

For your next step, choose a small object whose state you would save. What class-specific operation should the reader use, and what must it check first? Plan both an accepted value and an unexpected type so your tests show that the reader can do more than always reject.

## Visual description

[Four code-free opening scenes introduce saving and restoring supported object state and checking recovered types, connect earlier and later application runs, establish the equipment desk location card, and show the expected Label: lab report plus a later change-and-predict task.]

[The real Workspace appears. Main.java opens and the camera follows five imports, the supported LabelCard class with its fixed version identifier and String field, and the conventional Main entry method declaring checked I/O and class-lookup exceptions. A fresh temporary file receives the card. The writer closes, the reader restores Object, and the matching LabelCard check precedes a cast and getter. The reader closes before finally removes the owned file.]

[The pointer clicks the actual Run Code button. The report shows Label: lab. Narration separates the restored field value from original object identity.]

[One visible edit writes the String lab directly, keeping the LabelCard check and cast unchanged. A prediction and pause precede the second actual Run Code click. The report shows Unexpected object type. The false guard skips the cast and getter. The closing connects the checked-reader sequence to the desk task and asks for both accepted and unexpected test values.]