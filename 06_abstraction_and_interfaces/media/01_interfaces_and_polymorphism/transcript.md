# Interfaces and Polymorphism — video transcript

## Narration

Welcome! In this Java tutorial, you'll use interfaces, which describe shared operations, and polymorphism, which lets different objects answer the same request in their own way.

These ideas help applications work with different kinds of records or services through one shared operation, so adding a new implementation doesn't require a separate version of every caller.

Today we'll help campus staff announce a room location and a course identifier. Each sign will supply its own label. Both announcements must start with Ready, and the room must appear before the course.

We'll describe the shared request, implement two kinds of signs, and use one loop to announce them. A default method will provide the common formatting. First we'll trace a worked example; then you'll predict a fresh pair of signs.

Now that we're in the Workspace, let's open Main.java.

The file is open. Our caller needs a text label from either kind of sign, without knowing how that sign stores its information. Let's give that shared request a name: Labelled.

The interface keyword introduces our shared type. Label is a required method that returns a String and takes no arguments. Its declaration ends with a semicolon because the implementing classes will supply the body. This required interface method is public even though we haven't written public here.

Every announcement also needs the same prefix. Rather than repeat that formatting in both classes, let's put a default announcement method in the interface.

A default method has a body that implementing classes can inherit. Announcement asks the receiving object for its label and adds Ready before it. The formatting is shared, but the label still comes from the particular object. We now need a class that can answer that label request.

Our first sign will remember a room location. Let's define RoomLabel as an implementation of Labelled, keep its location private, and initialize that field in the constructor.

Implements establishes the interface relationship. The constructor copies its room argument into this object's private field, using the pattern from our earlier classes. That gives the object a location to remember; we still need the public method that turns the location into a useful label.

Let's supply the required label method and mark it with the Override annotation so the compiler can check the intended relationship.

This method returns Room followed by the stored location. Public preserves the access promised by the interface. Override is an annotation, not a method call: it helps catch a mismatched method name, but it doesn't create the implementation for us. A room named West will therefore supply the label Room West.

A course sign needs the same operation but different data. Let's give CourseLabel its own private course identifier and initialize it in a constructor.

The course object now remembers its own identifier. Its field has a different name from the room field, and the caller won't need either name. What connects the two classes is their promised label operation. Let's complete the course version of that method.

CourseLabel returns Course followed by its stored identifier. Both classes now answer the same request with different method bodies. Neither class replaces announcement, so both can use the default formatting. The interface checks the operation's shape; we still need to test that each returned label has the right meaning.

Let's bring the signs together in Main. Main is the class containing our caller, and its main method is where this program starts. We'll construct a West room sign and a JAVA-1 course sign, in that order.

The array's element type is Labelled, so each element can hold a reference to an implementing object. The objects remain a RoomLabel and a CourseLabel; using an interface reference doesn't change their classes or copy their fields. This array fixes the room-first order. We can now request one announcement from each object.

On each iteration, sign holds the next reference and has the declared type Labelled. Its announcement call enters the default body, which calls label on that same object. The actual object's class selects the label implementation. Let's click Run and follow those calls through the output.

The first line is Ready: Room West. The loop visits the room object, whose label method supplies Room West; the default method adds Ready. The second line is Ready: Course JAVA-1. Now the same default body reaches CourseLabel's label method. The loop and declared reference type stayed the same, while the receiving object changed.

The worked announcements follow the requested order and share their formatting. Let's test a fresh pair: room Lab A and course CSC-239. We'll keep the same definitions so you can trace the mechanism with new data.

The interface and room implementation are back in place. Notice that the default method still requests a label from its receiving object; it contains no fixed room name. Let's add the course implementation again.

Both implementations are ready. Let's construct the new signs in room-first order and use the same announcement loop. The new constructor arguments should provide the data; the method bodies should not need to change.

Before running, predict the two complete output lines. For each iteration, name the actual receiving class and the label method called inside the default announcement method. Explain which part determines the output order and which part supplies the label. Pause here if you need more time.

Let's click Run and compare the two announcements with your prediction.

The first announcement is Ready: Room Lab A, and the second is Ready: Course CSC-239. The array puts RoomLabel first and CourseLabel second. Each object supplies its own label, and the inherited default method adds the common prefix. Changing the input text required no change to either implementation or the loop.

We built one caller that announces two different kinds of signs. The interface describes the shared operations, polymorphic calls reach the receiving object's implementation, and the default method keeps the common formatting together. The output confirms both the requested order and the object-specific labels.

Suppose staff add an event sign to the same array. What operation must its class provide, what should that operation mean, and why could the existing loop announce it without a new branch? Describe one test that would check the event label's meaning, not just its String result type.

## Visual description

[The video opens without code. A red BHCC title band and Java logo identify the lesson. A central interface diagram connects one shared request to two objects with different implementations.]

[Three application panels connect records, pricing services, and new implementations to one shared caller. The next scene places campus staff beside a room sign and a course sign. An announcement board then shows placeholder room and course labels, the common Ready prefix, room-first order, and a default method's shared formatting.]

[The overview gives way to the real Workspace. Main.java is opened and its code is entered in purposeful blocks. The interface declares label and supplies announcement. RoomLabel stores a private room location and supplies a public label implementation. CourseLabel stores a private course identifier and supplies its own label implementation. The code view follows the insertion point as these definitions are typed.]

[Main's main method constructs the two sign objects and places their references in a Labelled array. One enhanced-for loop requests announcement from each object. The mouse moves to the toolbar play button and clicks it. The worked program prints Ready: Room West followed by Ready: Course JAVA-1. The explanation follows the default method's inner label call to each object's implementation.]

[The complete definitions are entered again with the new inputs Lab A and CSC-239. A prediction pause comes before the second Run click. The resulting output is Ready: Room Lab A followed by Ready: Course CSC-239. The closing connects the output to interfaces, polymorphic dispatch, and shared default behavior, then asks how an event sign could join the same caller.]
