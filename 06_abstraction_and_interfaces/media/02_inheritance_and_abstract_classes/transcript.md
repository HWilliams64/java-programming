# Inheritance and Abstract Classes — video transcript

## Narration

Welcome! In this Java tutorial, you'll use inheritance to share class behavior, override a method to specialize it, and use an abstract class to require behavior that each concrete subclass must provide.

Related features in an application often need common information but different calculations. These tools help you keep the shared work in one place while giving each kind of object the behavior it needs.

Today we'll help a campus team plan a reading task. Each job has a name. A reading job also has a nonnegative page count, and our planning rule allows two minutes per page. We'll start with a three-page task named Guide.

Our program will report a job heading, a reading description, and an estimated duration. We'll put the shared name in a base class, build a reading subclass, and trace how the caller reaches the right methods.

Now that we're in the Workspace, let's open Main.java.

The file is open. Every job needs a name, but different jobs may calculate time differently. Let's define an abstract NamedJob class that stores the common name without pretending it can calculate every job's duration.

Abstract means we cannot directly construct a NamedJob. The class can still store information and provide working methods. Its constructor receives a name and copies it into the private field of the object being initialized.

A reading subclass will need to use that name, but it does not need direct control over the field. Let's add a protected getter and a public description method that returns the name.

GetName returns the stored name without changing it. Protected makes this operation available in the subclass code we'll write; Java also permits access from the same package. The name field remains private. Description provides ordinary public behavior that a caller can request.

We can describe a named job now, but we still need an estimate. Let's require an integer minutes method without choosing a calculation in the base class.

This declaration has no method body. A concrete subclass must supply the missing implementation before we can create its objects. That lets a caller ask for minutes through the shared base type while each kind of job supplies its own rule.

A reading job adds a page count to the shared name. Let's extend NamedJob, keep pages in a private field, and pass the name to the superclass constructor before storing the page count.

Extends establishes the superclass relationship. In our Java 21 runtime, this explicit super call comes first in the constructor body. It initializes the base part of the same ReadingJob object; it does not create a second job. The next statement stores that object's page count. Constructors are not inherited, which is why ReadingJob supplies this constructor.

The shared description gives us a name. For a reading job, we also want the word reading after it. Let's override description, call the base version explicitly, and add that suffix to the returned text.

The Override annotation asks the compiler to check the method relationship. Inside this body, super.description deliberately calls NamedJob's implementation on the same object. It returns the name, and our override adds a space followed by reading. The stored name itself stays unchanged.

We have specialized the description, but the abstract minutes operation is still unfinished. Let's implement it using our two-minutes-per-page rule.

Minutes reads this object's page count and multiplies it by two. The result represents minutes, because each page contributes two minutes. For the three-page Guide task, that calculation returns six. Our accepted inputs are nonnegative page counts; this small example relies on that stated limit rather than adding validation here.

We also need a heading for the display. Let's add a public heading method that gets the inherited name and puts Job before it.

Heading uses getName from the base class. It does not reach into the private name field directly. The subclass gets the information it needs through a defined operation, while the base remains responsible for that stored field.

Now we can connect these methods to a real task. Main contains the main method where this standalone example starts. Let's create the Guide reading job with three pages, then keep a second reference to that same object using the NamedJob type.

Reading and job refer to one ReadingJob object. Their declared types differ, so they do not offer the same set of calls to the compiler. We'll use reading for its heading method, and job for the shared description and minutes operations. Let's print those three reports.

The program now connects shared state, an override, and a required calculation. Let's click Run and compare its reports with the task we planned.

Job: Guide comes from heading, which obtains the stored name through the protected getter. Guide reading comes from the override: it reuses the base description and appends the suffix. Minutes: six comes from ReadingJob's calculation for three pages. The calls through job reach the concrete object's implementations, even though that reference is declared as NamedJob.

We have traced the complete Guide task. Let's keep the class behavior unchanged and create a task named Checklist with four pages, so you can apply the same reasoning to different inputs.

Before we run it, predict all three lines. Which method supplies the heading? How does the override build the description? Which page count and rate determine the duration? Pause here if you need time to trace the calls.

Let's click Run and check your prediction against the new task.

The reports are Job: Checklist, Checklist reading, and Minutes: eight. The new object stores Checklist and four pages. The heading and description use that name, and the required minutes implementation calculates four times two. Changing the input did not require a new version of the shared base behavior.

We used inheritance to share the name and working methods, an override to extend the description, and an abstract method to require a concrete estimate. Both constructor bodies and the later method calls worked with one object. For a different kind of job, consider which information could stay in NamedJob and which duration rule the new subclass would need to supply.

## Visual description

[The code-free opening uses the BHCC red title band and Java logo. A shared foundation introduces inheritance, followed by two distinct outlines for overriding and abstract requirements. Three application panels then connect common information to different calculations.]

[The next scene shows a campus team and three pages for the Guide task, with a rule of two minutes per page. A single report sheet reveals fields for the job heading, reading description, and estimated minutes.]

[The video enters the real Workspace and opens Main.java. Code is typed in purposeful blocks while the view follows the insertion point. NamedJob stores a private name, provides a protected getter and a public description, and declares the required minutes operation. ReadingJob initializes the shared name and its page count, overrides description using the explicit superclass method, implements the duration rule, and adds a heading.]

[The Main class and its main entry method create one ReadingJob with two reference variables. The caller prints a heading, description, and labeled duration. The pointer moves to the editor Run button and clicks it. The first output is Job: Guide, Guide reading, and Minutes: 6.]

[Only the construction line changes to Checklist with four pages. The video asks for a prediction before the second Run click. The new output is Job: Checklist, Checklist reading, and Minutes: 8. The closing connects shared state, overriding, abstract requirements, and one object's initialization to the original task, then asks about a different kind of job.]
