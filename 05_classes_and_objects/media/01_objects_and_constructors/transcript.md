# Transcript: Objects and Constructors

Welcome to this Java tutorial, where you'll define a class with fields, initialize objects with a constructor, and use an instance method to change each object's own state.

These skills let applications manage separate customer accounts, equipment loans, or order items with one shared set of rules, reducing copied code as the number of records grows.

A campus welcome desk needs a pass record for each visitor. Each pass stores a name and a whole-number visit count that starts at zero. Recording a visit adds one to that visitor's count; it must leave other visitors' counts unchanged.

We'll define the pass, create two separate records, and report each visitor's name with the right count. After a worked example, you'll predict another pair of records before we run the program.

Now that we're in the Workspace, let's open Main.java.

The name and visit count belong together. A class defines the data and operations for one kind of object. Let's define DeskPass and give it two instance fields: an owner name and a visit count.

These fields describe what each pass will store. A field is a variable that belongs to an object, and the values together are its state. The class definition alone creates no visitor's pass. We also need a constructor to initialize each new pass with its owner's name and a zero count.

The constructor's name matches DeskPass, and its header has no return type. It receives an owner parameter for this one call. In the assignment, this dot owner names the new object's field, while owner on the right names that temporary input. The next assignment stores zero in the same object's visits field.

Once a pass exists, we need to record visits without starting over. An instance method performs an operation on the object that receives the call. Let's add a visit method that updates the existing count.

This refers to the current object. The assignment reads that object's visits field, adds one, and stores the new number back in the field. The updated state remains after the call ends. Void means the method returns no value; its useful effect is the changed count.

Our pass definition is complete. Below it, the Main class will hold main, the starting method for this program. That is where we'll create the passes and call their operations.

Let's create one pass for Eden and another for Noah. Each new expression creates a separate DeskPass, invokes its constructor with a name, and yields a reference that lets us reach the resulting object.

First and second now describe the references our program will use. When the program runs, each constructor initializes its own object's name and zero count. The constructor itself returns no value; the new expression provides the reference. Using the same class does not make the two objects share their fields.

We'll record one visit through first and two visits through second. The reference before the dot selects the receiver: the particular object whose method runs. Each call uses the same visit rule on that receiver's fields.

When these calls run, first's count goes from zero to one. The two calls on second move its separate count from zero to one, then to two. During each call, this refers to its receiver. Updating one receiver does not update the other pass.

To check the records, let's print each owner's name beside the count read through the same reference. The dot selects a field, so each label and number come from the same pass.

The complete program creates both passes, records the visits, and prints their current state. Let's click Run and check that the two records stayed separate.

Eden is one because first received one visit call. Noah is two because second received two. Both used the same method definition, but each call changed only its receiver's field. The constructor supplied the starting state once for each new object.

Now let's use the same pass definition for Maya and Luis with a different call sequence. We'll replace the worked program with a fresh copy. The fields, constructor, and visit rule stay the same, so you can focus on which object receives each call.

The class is ready again. We'll add Main and create two fresh objects for Maya and Luis. These new expressions start a new pair of records; they do not reuse the earlier visitors' stored counts.

The two object-creation statements are entered. Let's add the visit calls and the report. Follow the reference before each dot to decide which count changes, then keep your prediction until the complete program is visible.

Before we run it, predict both output lines. Begin with the counts established by the constructors and trace the receiver of each visit call. Pause here if you'd like more time.

Let's click Run and compare the report with your prediction.

Maya is two because first receives two visit calls. Luis is one because second receives one. Both counts began at zero in separate objects. The final print statements read each object's own name and count, so the result agrees with the call sequence.

The desk now has separate visitor records governed by one definition. Fields hold each object's state, the constructor establishes its starting values, and the instance method applies the shared update rule to its receiver. We can change that rule in one place while keeping every visitor's count separate.

Suppose the desk creates a third pass but records no visits on it. What would its count be, and would another call through first change it? Explain which object this would refer to during that call.
