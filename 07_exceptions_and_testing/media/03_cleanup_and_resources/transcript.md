# Cleanup and Resource Lifetimes — video transcript

## Narration

Welcome! In this Java tutorial, you'll use AutoCloseable and try-with-resources to connect an object's cleanup to its lifetime, then trace the order in which Java closes multiple resources.

Reliable cleanup keeps files and other limited resources available for later work. When an application handles many requests, tying cleanup to scope helps prevent one request from leaving resources unavailable to the next.

Today we'll build a small classroom model for campus workshop staff. Two named objects will report when their use begins and ends. These printed messages model resource lifetimes; they do not borrow real equipment or open actual files.

We expect the program to acquire the first resource, acquire the second, and perform its work. Then Java should close the second resource before the first, and only afterward print that the operation is done.

Now that we're in the Workspace, let's open Main.java.

The file is open. We need each object to identify itself when it starts and finishes. Let's define NamedResource, connect it to the AutoCloseable interface, and give it a field for that name.

The name field belongs to each object. Implementing AutoCloseable promises that our class supplies a close method. The interface gives Java a standard cleanup operation to call, but this declaration alone does not create an object or schedule its cleanup.

Next, the constructor will store the name supplied by the caller and report that this object's modeled use has begun.

The parameter brings the caller's name into the constructor. This dot name selects the field on the new object, so that name remains available after construction. The Opened message makes the beginning of this modeled lifetime visible.

Now let's provide the promised close operation. It will report the end of use with the same stored name.

Override asks Java to check that this method fulfills the inherited method relationship. It does not execute close. Our close method prints a lifecycle message; a real resource would perform its actual release work here. The constructor and close method use the same field, so their messages identify the same object.

With our model ready, let's add the Main class and its main method. This is the program's entry point when we run the Java application.

The main method will own this operation. We want both resources to finish their use when the operation ends, so we'll declare them in a try-with-resources header instead of relying on manual close calls at the bottom of the work.

Java initializes resources from left to right. It constructs first, then second, and both must initialize successfully before the body begins. The declarations inside these parentheses register automatic cleanup. The semicolon separates the two resource declarations.

Let's give the body a Work message, then put Done after the entire try statement so we can see where cleanup fits.

Work runs while both resources are available. When the body finishes, Java calls close in reverse initialization order: second, then first. Done is outside that scope, so it follows both close operations. Let's click Run and check the complete sequence.

The two Opened lines show first being constructed before second. Work appears only after both are ready. The Closed lines reverse that order, with second finishing before first. Done appears last because continuation waits for cleanup to finish. We did not put any manual close calls in the body.

The order comes from the positions in the resource header, not from the names we chose. Let's keep the variables and declaration order, but swap the names passed to the two constructors.

Before running, predict all six output lines. The first variable now refers to the object named second, and the second variable refers to the object named first. Which name will appear in each Opened and Closed message? Pause here and follow the header positions.

Let's click Run and compare that prediction with the actual lifecycle messages.

Opened now shows second before first, because those are the names supplied in initialization order. Closed shows first before second, because Java still closes the later resource before the earlier one. Work and Done keep their positions. Changing a name changed the report, not the cleanup rule.

You connected an object's close operation to scope with AutoCloseable and try-with-resources. The output showed when each lifetime began and ended, and confirmed reverse closing order. This pattern lets the code describe the operation while Java arranges cleanup around it.

For a transfer question, imagine the work raises an exception after both resources are ready. Which close operations should Java attempt before a handler responds, and in what order? Use the resource lifetimes we just traced as you prepare for the notebook's failed-path examples.

## Visual description

[The video opens with four distinct code-free scenes in the BHCC red, blue, and white style. A horizontal path shows acquisition, use, and closure, connected to AutoCloseable and try-with-resources. An application panel and current/later request cards explain the broader importance of cleanup. Campus workshop staff appear beside two named model objects. An ordered event trace previews the initial acquisition, work, reverse closing, and continuation sequence. These objects print lifecycle messages; they do not open files or borrow real equipment.]

[The real Workspace appears and Main.java opens. The camera follows the insertion point as the NamedResource class is typed. It implements AutoCloseable and stores a name field. Its constructor stores the supplied name and prints an Opened message. Its close method prints a Closed message with the same name. The Main class and main entry method contain a try-with-resources header that initializes the resources named first and second, then a body that prints Work. A Done message follows the try statement.]

[The pointer moves to the native Run Code button and clicks. The output shows Opened: first, Opened: second, Work, Closed: second, Closed: first, and Done. The explanation connects left-to-right initialization, reverse closing order, and continuation after cleanup.]

[The two constructor names are swapped while variable names and header positions remain unchanged. The video asks learners to predict the six output lines and pauses before the pointer clicks Run Code again. The output shows Opened: second, Opened: first, Work, Closed: first, Closed: second, and Done. This confirms that header positions determine the order; the names identify the objects in the report. The closing connects the result to resource lifetime and automatic cleanup, then asks which cleanup operations Java should attempt if the work throws an exception after both resources are ready.]
