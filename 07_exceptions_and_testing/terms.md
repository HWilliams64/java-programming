**Exception object** - An object that describes an execution failure through its type, message, and related information.
**Abrupt completion** - Leaving an operation before its remaining statements finish.
**Try block** - A block surrounding work whose exceptions may be handled by associated catch blocks.
**Catch block** - A block that receives a matching exception and responds to it.
**Stack trace** - A record of the chain of method calls associated with an exception.
**Stack unwinding** - Leaving unfinished method calls while searching outward for a matching exception handler.
**Checked exception** - An exception type outside the RuntimeException and Error families whose possible propagation generally must be caught or declared.
**Unchecked exception** - An exception type in the RuntimeException or Error family whose possible propagation does not require a throws declaration.
**Throw statement** - A statement that raises a particular exception object now.
**Throws declaration** - A method declaration that names exception types that may leave the method and reach its caller.
**Custom exception class** - An application-defined exception type that gives a particular failure a meaningful name.
**Exception cause** - An earlier failure retained inside a later exception.
**Resource lifetime** - The interval between acquiring a resource and releasing it.
**Finally block** - A block that normally runs as control leaves its associated try/catch, including during a pending return or exception.
**AutoCloseable contract** - An interface whose close operation makes a resource eligible for automatic cleanup.
**Try-with-resources statement** - A statement that closes successfully initialized AutoCloseable resources when its scope ends.
**Reverse resource closure** - Closing registered resources in the opposite order from their successful initialization.
**Suppressed exception** - A secondary cleanup failure attached to an earlier primary exception.
**External dependency** - A library added beyond the Java standard library.
**JAR** - A Java archive file containing compiled classes and related resources.
**Classpath** - The locations Java searches for classes needed by a program or kernel.
**Dependency coordinate** - The group, artifact, and version that identify a library for the supplied dependency setup.
**Unit test** - An automated check of a small behavior using controlled inputs and expected results.
**@Test method** - A method marked for JUnit Jupiter to discover and execute as a test.
**Test assertion** - A check that compares actual behavior with an expected result and reports a failure when they differ.
**Test runner** - Software that discovers tests, executes them, and collects results.
**Class literal** - An expression such as LabelToolsTest.class that refers to the class itself.
**Summary listener** - A supplied object the test runner notifies as tests progress so it can collect their result counts.
**Regression test cycle** - Keeping a behavior check, confirming that it detects a relevant mistake, and rerunning it after the repair.
**SHA-256 checksum** - A fingerprint calculated from a file’s contents; comparing it with an expected value helps check that the file has the expected bytes.
