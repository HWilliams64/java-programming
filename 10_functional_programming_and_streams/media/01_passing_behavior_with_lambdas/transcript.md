# Passing Behavior with Lambdas — video transcript

## Narration

Welcome to this Java tutorial. You'll use lambdas, small expressions that supply behavior, and method references, which refer to existing operations. You'll pass those rules to one helper and explain when the chosen operation actually runs.

Applications often keep the same processing step while callers choose one detail. Passing behavior lets a shared method serve those different choices, so the program needs fewer copies to maintain. We'll use an interface contract to make the expected input and result types clear.

A campus visitor desk needs cleaned names for some displays and guest labels for others. Each input is text. A cleaning rule removes ordinary spaces around a name. A labeling rule adds Guest, a colon, and a space before the name. The helper must apply exactly the rule its caller supplies.

We'll build one text-rendering helper and use it with both rules. First we'll trace a worked set of names. Then you'll predict a different set before we run it. The report should show the chosen formatting while the helper's body stays the same.

Now that we're in the Workspace, let's open Main.java and define the operation our helper can receive.

Java's Function interface describes one operation with an input and a result. We'll import it, then give LabelPrinter a render method that receives both the text and the rule to apply.

Function is a functional interface: it has one required abstract operation, called apply. Its first String type argument describes the input; the second describes the result. Inside render, apply invokes the supplied rule with the text. Return sends that result back to the caller. The helper doesn't choose the formatting itself.

Let's add the program's entry point around the caller statements. Main is the class containing this part of our code, and its main method is where the program starts. We'll put the rule choices and their calls inside that method.

The first caller needs surrounding spaces removed. We'll store a cleaning lambda, then create a separate labeling lambda that adds the Guest prefix.

The arrow separates each lambda's parameter from its body. The target Function type tells Java that the parameter and result are Strings. In this expression form, the body's value is the returned result. Assigning clean and tag makes the two rules available; it doesn't yet process a name or print anything.

Now let's supply the cleaning rule with padded Ari text and the labeling rule with Bo. Each call passes two arguments to the same helper. The surrounding print statement displays the String that comes back.

For the Ari call, render receives the padded text and the clean rule. Applying that rule removes the surrounding spaces. For Bo, the selected rule constructs a guest label. The helper follows the same steps because both rules satisfy the same input and result contract.

String already has the trim method we need. Let's supply that existing operation through a method reference, then apply it to padded Bea text.

The double colon names behavior to use later. It doesn't call trim at the assignment. When namedClean is applied, the supplied String becomes the object whose trim method runs. This compatible method reference performs the same cleaning operation as our first lambda. Let's click Run and inspect the worked report.

The first line is Ari without surrounding spaces. The second is Guest, a colon and space, then Bo. The last line is Bea without surrounding spaces. The caller supplied a rule and input, render invoked the rule, and printing displayed the returned result. The original Strings weren't edited in place.

Let's keep both rules and the helper exactly as they are. We'll change only the three supplied names to Maya, Luis and Nora. Maya and Nora will still have two spaces on either side in their inputs.

Before running, predict all three lines. For each call, identify its input and the selected rule. Which calls remove surrounding spaces, and which call adds the chosen prefix? Pause here and follow the result through render to its print statement.

Let's click Run and compare your prediction with the actual report.

The report shows Maya, then Guest with Luis, then Nora. Clean processed the first input; tag produced the second label; namedClean used the third input as trim's receiver. Only the caller's text changed. The same helper still applied each chosen operation and returned its result.

You used a functional interface to describe one text operation, supplied behavior with lambdas and a compatible method reference, and separated creating a rule from applying it. For a transfer question, imagine the desk needs staff labels too. What new rule could the caller supply, and why could the existing render method still serve it?

## Visual description

[Four designed opening scenes introduce Java lambdas, method references and invocation; connect different caller choices to one shared method; show a campus visitor desk with cleaning and guest-label rules; and present a blank three-line report with formatting criteria. The guest label includes Guest, a colon and a space before the name. The later prediction output is not shown in the opening.]

[The real Workspace appears and Main.java opens. The camera follows actual typing of the Function import and LabelPrinter helper, the Main class and main entry method, separate clean and tag lambdas, and their caller statements. A method reference supplies the existing trim operation for a third call. The explanation separates creating behavior, passing it, applying it, returning a result and printing.]

[The pointer clicks the native Run Code button. The terminal shows Ari, Guest: Bo, and Bea on separate lines. The two cleaned inputs lose surrounding spaces; the other rule adds the chosen guest label.]

[The caller lines are edited to the retained canonical inputs: padded Maya, Luis, and padded Nora. A prediction prompt and thinking pause precede the second native Run Code click. The terminal shows Maya, Guest: Luis, and Nora on separate lines. The helper and both rules remain unchanged. The closing connects the observed report to the functional interface contract, lambdas and the compatible method reference, then asks how the caller could supply a staff-label rule to the same helper.]
