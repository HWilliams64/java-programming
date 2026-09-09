# Testing Behavior with JUnit — video transcript

## Narration

Welcome to this Java tutorial. You'll use JUnit to check a method's normal result, a boundary case, and an expected exception. You'll also interpret a test summary and deliberately challenge an assertion to check that the tests can detect a mismatch.

A program can still compile after a change that breaks its behavior. Automated tests make important expectations repeatable, so a team can check those expectations again as its code changes. Each test gives evidence about a particular case; passing tests do not prove that every possible input works.

Our campus workshop needs one label for each kit in every group. Two groups with three kits each need six labels. Zero groups need zero labels. Negative counts are invalid, so the method must reject them with a clear exception message.

We'll build three tests for those rules, then run them together. A successful baseline should report three succeeded and zero failed. After reading that result, we'll change one expectation and use the next summary to see whether the test detects the disagreement.

Now that we're in the Workspace, let's open Main.java. This lesson's prepared project includes JUnit and the Run configuration, so we can focus on testing behavior.

First, let's import the test and assertion tools, followed by the launcher tools that will run our test class and collect its results.

These imports make library types available by their short names. Importing JUnit does not run a test. We still need a method to check, test methods that state expectations, and a runner that executes them.

Let's define labelCount. Its two inputs represent groups and kits per group. The guard rejects either negative count before multiplication.

For valid counts, the product is the number of labels. For an invalid count, IllegalArgumentException reports that the caller broke the input rule. The message is part of the behavior we will check.

Now let's start the test class and add our ordinary positive case. The Test annotation marks a method for JUnit to discover. The assertion compares an expected value with the method's actual result.

Six is the expected value; the call with two and three produces the actual value. If they differ, this assertion makes the test fail. The test's name describes the behavior being checked, while the public constructor lets JUnit create the test object.

Zero sits at the edge of the valid counts. Let's add a separate boundary test so this case remains visible even if the implementation changes.

The expected result is zero because there are no groups to label. Keeping this in a separate test helps distinguish an ordinary calculation from behavior at the edge of the allowed input range.

Our third test checks rejection of a negative count. Let's include both a failure when the call returns normally and a message check when the expected exception is caught.

The negative call should jump into the catch block. If it returns instead, the fail assertion prevents a false success. In the catch block, assertEquals checks the message. A different exception type is not accepted by this handler. Together, these paths check more than merely calling the method and hoping an error occurs.

The tests are defined, but they have not run. Let's add the application entry point and build a discovery request selecting this test class.

The request identifies the tests we want JUnit to find. Next, a summary listener will collect the results. We'll open a launcher session, register that listener, and execute the request.

Execute is the step that runs the selected tests. Try-with-resources closes the launcher session afterward. The individual test order is not prescribed here; our summary counts outcomes across the selected tests.

Finally, let's print the succeeded and failed counts from the collected summary, then click Run to establish our baseline.

Three tests succeeded and none failed. That result covers the positive product, the zero boundary, and rejection of a negative group count with the expected message. It is our baseline for these three cases, not a guarantee about every input.

Let's challenge the positive test by changing only its expected value from six to seven. The method and its two inputs will stay the same.

Before running, predict the two summary counts. The calculation still uses two groups and three kits per group, but one assertion now expects seven. Which tests should agree with their expectations? Pause here and reason through all three cases.

Let's click Run and compare your prediction with JUnit's actual summary.

Two tests succeeded and one failed. The positive test expected seven while the method returned six. The other expectations still matched. This deliberate mismatch checks that an assertion can detect disagreement; it is not a regression, because we did not break previously correct application behavior.

Now let's restore the correct expectation of six and run the same tests again.

The summary returns to three succeeded and zero failed. We repaired the test expectation without changing the method. A future unintended behavior change would be a regression if it broke behavior that had worked before; keeping useful tests helps detect that kind of problem.

You used assertions to make three behavior rules executable, included both paths needed for a reliable exception test, and separated defining tests from running them. For a transfer question, what extra test would check a negative kit count? In the notebook, you will also add a boundary test for zero kits.

## Visual description

[Four code-free opening scenes use the BHCC red, blue, and white visual system with a Java logo. Behavior rows introduce normal results, boundary cases, and expected exceptions. A change-and-recheck flow explains repeatable evidence. Two group panels each contain three kits, connecting two groups times three kits to six labels, while zero and negative count rules appear below. A three-case list and a baseline scoreboard show three succeeded and zero failed.]

[The actual Workspace opens Main.java in the prepared JUnit project. The camera follows typed imports, the labelCount method with its negative-input guard, and three test methods. The positive test expects six from two and three. The zero test expects zero. The negative test contains a fail assertion after the call, plus a catch block checking the expected exception message. A Main entry point selects the test class, registers a summary listener, executes the request inside a launcher session, and prints summary counts.]

[The real pointer clicks Run Code. The terminal shows Succeeded: 3 and Failed: 0. The positive assertion is changed from six to seven while the method and inputs remain the same. Learners predict the two counts during a pause. A second native Run click produces Succeeded: 2 and Failed: 1. The expected value is restored to six, and a third native Run click returns the summary to three succeeded and zero failed. The closing distinguishes this deliberate mismatch from a regression and asks learners to transfer the exception-testing pattern to a negative kit count. It then points to the notebook boundary test for zero kits.]
