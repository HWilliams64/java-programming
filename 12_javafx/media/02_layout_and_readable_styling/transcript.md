# Transcript: Layout and Readable Styling

Welcome to this Java tutorial, where you'll learn to arrange interface content in rows and columns, separate sections with spacing and padding, and keep text readable when a window changes size.

These skills help people find related information quickly and keep important instructions visible as an application’s window changes size.

A campus service desk needs a notice with a heading, a room location, and a short instruction. We'll first build a reading desk notice. Then we'll adapt the same structure for a study room, keeping the location and instruction easy to find.

We'll inspect the actual notice, narrow its native window, and check that the complete instruction remains visible. The console will report the room value and wrapping setting. That report supports our check, but only the visible interface can show whether its layout fits.

In the Workspace, we'll open Main.java and use the supplied standalone JavaFX runner from the previous lesson. Its start method receives a Stage after the toolkit is ready. Our layout instructions belong inside that interface method.

The imports make the class names available. Main extends Application, and start runs on the JavaFX Application Thread. The stage variable refers to the primary window. We can now create the nodes that will become its content.

Start with a Label for Reading Desk. A heading should stand out from ordinary instructions, so we'll give this label an inline style: presentation settings stored in a Java String on this node.

Inside that String, each CSS declaration has a property name, a colon, a value, and a semicolon. The font size is twenty-two pixels, and the font weight is bold. The quotes belong to the Java String. These settings change the heading's appearance; they do not change its text or move it into a different container.

Next, create a label for Room and a separate label for Library. Those two pieces form one location, so we'll place them in an HBox. An HBox arranges its children horizontally, in the order they are supplied.

The first constructor argument, eight, is the gap between adjacent children. The remaining arguments name the two labels. Space inside a label is not what creates this gap; the HBox owns the arrangement. Soon this whole row will become one child of a larger column.

The instruction is longer than the room value. We'll give it a separate Label and enable text wrapping. Wrapping allows a label to use another line when its assigned width cannot hold all the words on one line.

The true setting permits wrapping. It does not promise that every possible window size will display the whole message. The container must allocate enough width and height, so we will inspect the actual label after resizing.

Now build a VBox containing the heading, the HBox row, and the instruction label. A VBox arranges its children vertically. We'll separate adjacent children by twelve pixels, then add twenty pixels of padding inside the container's edges.

The VBox has three direct children. The two location labels are children of the HBox inside it. Spacing controls the gaps between neighboring children. Padding controls the space between the container boundary and its content. Insets describes that edge space; its one-number constructor applies the same amount to all four sides.

Attach this root to a Scene and give the Stage its separate title, Desk Notice. The scene requests a four hundred twenty by two hundred forty content area. After showing the Stage, we'll print the room label's text and whether wrapping is enabled.

We'll finish the supplied start method and main entry point. The launch call belongs to this standalone runner. In the notebook, the supplied Fx support uses the existing kernel process instead, so you will keep the notebook's complete example format.

Let's click Run. We have configured Library as the room value and enabled wrapping. The console will report those properties, while the Desktop will show the heading, row, and instruction arranged by the two containers.

The Reading Desk heading appears above the room row and instruction. Its larger, bold text gives it a clear role. The row reads from left to right. The VBox places the three sections from top to bottom, with edge space around the group.

Let's make the native window narrower using its resize control. The source and label text will stay the same. Watch how less available width changes the instruction's line breaks, and check that its final words remain visible.

The window is narrower, and the full instruction remains available in the label. The containers have laid out their children again using the new space. Wrapping can change where a line ends; it does not require the number of lines to increase every time the width changes. Resizing also does not print a new construction report.

We'll close this notice before changing its inputs. Closing the last window lets this standalone Java process finish. A complete run will start a new process and construct a new notice at its requested initial size.

For the study room version, use Study Room as the heading, Lab A as the room, and the instruction about bringing course notes and leaving the table ready. Set the window title to Room Notice and request a four hundred forty by two hundred twenty scene. Keep the same row, column, gaps, padding, and style.

Before we run, predict the two console lines by tracing the getter calls. Then predict which values stay unchanged when the native window becomes narrower. Will the source text change, or will the container assign a different width to the same label? Pause and write your prediction.

Let's click Run and compare the report with your prediction. Then we'll inspect the study room notice before and after the same native narrowing action.

The report gives Lab A and wrapping true. Room Notice is the native window title, while Study Room is the heading inside the scene. The full instruction is visible, and the HBox remains one child between the heading and note in the VBox.

Now narrow this window without changing the program. Watch the final words of the instruction as the available width decreases.

The instruction still ends with for the next group. Its line break has moved earlier. Both of these tested views use two lines, so the visible change is the break point, not the line count. The padding still belongs to the root's edges, and the row and column still arrange the same children.

Let's close the window and run the unchanged program once more. That should create a fresh notice at the scene's original requested size, rather than preserve the width we chose by dragging its edge.

The source is unchanged. Click Run again to check that complete recreation restores the initial Room Notice layout.

The notice is back at its initial size with the same title, heading, location, and instruction. That separates the program's initial configuration from a user's later resize. We'll close this final window after checking the full text.

You built a row inside a column, distinguished gaps from edge padding, styled a heading, and tested wrapped text in a real window. For a campus equipment notice with a longer instruction, which parts of this layout would you preserve? What would you inspect at a smaller width before calling the interface readable?
