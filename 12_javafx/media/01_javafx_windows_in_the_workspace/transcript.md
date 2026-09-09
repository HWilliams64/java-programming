# Transcript: JavaFX Windows in the Workspace

Welcome to this Java tutorial, where you'll learn how JavaFX windows, scenes, labels, and layouts work together to build and test a graphical interface. Scenes connect a window to its content; labels present text, and layouts place it.

These connections help graphical applications keep window titles, content, and arrangement separate. That makes changes easier to reason about and gives you better checks when a program prints the right values but does not show the interface a user needs.

A campus course desk needs a small welcome display. We will first build a desk status window with one centered message. Then we'll adapt the same structure for the course welcome display.

We'll inspect each actual window on the Workspace Desktop and compare its title and message with the console. We'll also close the course window and run the complete program again. A printed report and a visible, working window answer different testing questions.

Now that we're in the Workspace, let's open Main.java. We'll use a supplied JavaFX runner and place our window-building instructions inside its start method.

A standalone graphical program needs JavaFX to start its toolkit and call the interface code on the JavaFX Application Thread, the sequence that handles interface work. The Application class provides that runner. Our Main class extends it, and its start method receives the primary Stage from JavaFX.

The imports make the JavaFX class names available. Override marks start as the operation our class supplies in place of the inherited one. JavaFX calls it when the toolkit is ready. In the notebook, the supplied Fx support handles this setup differently; we'll connect those two execution paths after observing the window.

A window object alone has no message to display. We'll refer to the supplied primary window as stage, create a Label containing Open, and give that label to a StackPane. A Label presents text for reading. StackPane is a layout container that centers this single child.

The label and layout are nodes, objects in the scene's content tree. The layout is the parent and the label is its child. We'll use that layout as the root, the starting node for this scene. The Stage itself is the surrounding native window, not a node in that content tree.

The content now has a root, but it still needs a connection to the window. We'll create a Scene using that root and request a three hundred by one hundred eighty content area. Then we'll set the Stage title to Desk Status and attach the Scene.

The scene holds the root, while the stage holds the scene. Its title is a separate value from the label's text. These steps configure the display, but construction and attachment do not make the window visible. We still need to show it.

We'll call show on the stage, then print its title and the label's text. Both getters run here inside start, on the interface thread. Those lines report configured values; the Desktop will provide our separate view of the actual window.

We'll finish the supplied runner now. Main is the class containing this program, and main is the method where its standalone execution begins. The launch call starts JavaFX so it can call the start method we've just completed. You do not need to build this runner in the notebook.

Let's click Run. The stage title is Desk Status and the label stores Open, so the print calls will report those two properties. StackPane will place its one label in the center of the scene. After the report appears, we'll switch to the Desktop to inspect that display.

Desk Status appears in the native title bar, and Open is centered in the content area. The window's border and title bar sit outside the requested scene dimensions. We have now seen the result of connecting the layout to the scene, attaching the scene to the stage, and showing it.

Let's close this desk status window. In this standalone program, closing its last window lets the Java process finish. We'll return to the code to adapt the same structure for the course display.

We'll keep the runner and the object connections. Only the Label text, scene dimensions, and Stage title will change. The new label input is Welcome to C S C two thirty-nine, the scene requests four hundred twenty by two hundred twenty, and the title input is Course Welcome.

Before we run this version, predict the two console lines. Which value comes from the Stage, and which comes from the Label? Also predict where the label will appear in the larger scene. Pause here and trace the object connections and the two getter calls.

Let's click Run and compare your prediction with the actual course welcome display. We'll read the report and then inspect the native title and content.

The window title is Course Welcome. Its centered label says Welcome to C S C two thirty-nine. The console reports Window with the stage's title, then Message with the label's text. Those values belong to separate objects. The larger Scene gives the layout more room without changing its single child's default alignment.

We'll close this course window and confirm that it disappears. Once this standalone process finishes, running the complete program again will start a new process and construct another window. That checks more than merely repeating the same printed values.

The source is unchanged. Let's click Run again, then inspect the newly created Course Welcome window on the Desktop.

The new window has the same title and centered message. This run constructed a new set of objects with the same inputs. It did not revive the earlier Stage object. We'll close this final window after the check.

Notebook cells already run inside a Java process. Their supplied Fx support starts the toolkit once and keeps it available after a window closes. Fx.run gives a short interface action to the JavaFX Application Thread, and Fx.closeWindows clears earlier windows in that kernel. Rerunning a complete notebook example builds fresh objects while using that same toolkit. Keep launch in this standalone runner, not in a notebook cell.

You connected a native Stage to a Scene, used a StackPane root to center a Label, and checked both the configured values and the visible window. Separating these jobs makes the interface easier to change and test. For a campus tutoring desk, what would you change to give the window a new title and a different message? Which checks would you make in the console, and which would require seeing the Desktop?
