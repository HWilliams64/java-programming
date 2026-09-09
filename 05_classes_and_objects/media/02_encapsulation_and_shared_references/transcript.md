# Transcript: Encapsulation and Shared State

Welcome to this Java tutorial, where you'll use encapsulation to protect an object's state and distinguish each object's fields from a field shared by its class.

Checked operations help inventory, booking, and account systems keep their records consistent, even when many parts of an application request changes.

Today we'll model a campus supply desk with a separate bin for each kind of item. A request must be positive and no larger than that bin's remaining stock. A rejected request must leave the count unchanged.

We'll put the checks inside the bin, create two bins, and report each request's result alongside the remaining stock and the number of bins constructed. After a worked example, you'll predict a fresh case.

Now that we're in the Workspace, let's open Main.java.

A bin needs its own stock count, while the application needs one construction count for the whole class. Let's define SupplyBin and declare those two fields.

Private keeps callers from assigning these fields directly. Stock belongs separately to every bin. Static gives the class one binsCreated field, initialized to zero when the class is initialized. It counts the constructions we record, not variable names or requests.

We still need starting values for each new bin. The constructor will store its incoming stock and increase the shared count once.

This dot stock selects the new object's field, while stock on the right is this call's parameter. The next assignment increases the class field. Our caller must supply a nonnegative starting count. That is a precondition: this constructor assumes it rather than checking it.

Once a bin exists, callers need a safe way to take items. We'll give them a public take method that returns a Boolean result. First, let's reject requests that must not change the stock.

The condition rejects either a nonpositive amount or an amount greater than the remaining stock. If either comparison is true, return false ends the call immediately. This guard protects our invariant, the rule that stored stock stays nonnegative.

A request that passes both checks can now change the receiving bin. Let's subtract the amount and report success.

The assignment reads the current stock, subtracts the accepted amount, and stores the remainder. Returning true reports that the request succeeded. The order matters: returning false after an earlier subtraction would not undo that subtraction. An exact request for the remaining stock is allowed and leaves zero.

Callers also need to inspect the counts without assigning the private fields. Let's add a reader for one bin and a static reader for the construction count.

GetStock returns the receiving bin's current count. GetBinsCreated returns the shared class count, so callers use the class name for that operation. Public readers make values available without allowing an outside assignment to either private field.

The bin definition is ready. We'll put the caller in Main, whose main method starts the program. For this worked case, create a three-pen bin and a separate one-map bin.

These two new expressions run the constructor twice. The bins have separate stock values, while the class count becomes two. Requesting pens must not change the map bin.

Let's request two pens twice and print the result of each request. The first request should leave one pen. The second asks for two when only one remains, so it must fail without another subtraction.

Each print statement calls take before printing its Boolean result. We also need to inspect the stored counts, because a false result alone would not prove that rejection left the state unchanged. Let's add that report and finish the program.

The complete report checks success, rejection, both bins, and the shared construction count. Let's click Run and see whether all those observations agree.

The first request is true because two pens were available. The repeated request is false because only one remained. Pens is still one, confirming that rejection preserved the state. Maps is one because we never requested maps. Bins is two because we constructed two objects; taking items creates no additional bin.

Now we'll use the same class with five pens and two maps, requesting three pens and then four. We'll enter a fresh program so you can trace both requests from those starting values. The guard and construction rule stay the same.

The guarded operation is entered again. Let's finish its readers and create the two bins for the prediction case. Each run starts a new Java process, so this program begins with a fresh construction count.

The caller now supplies five and two to separate constructors. Let's add the two requests and the report. Trace each request using the stock left by the previous one, rather than reusing the original quantity.

Before we run it, predict all five output lines. For each request, decide whether the guard ends the call or permits subtraction. Then account for the untouched bin and the construction count. Pause here if you'd like more time.

Let's click Run and compare the report with your prediction.

Taking three is true and leaves two pens. Taking four is false because four exceeds those two, so Pens remains two. Maps also reports two, but for a different reason: no request changed that separate bin. Bins is two because the two new expressions ran the constructor twice.

The supply desk now has one place to check requests before changing a bin. Private fields keep callers on that path, the guard preserves the stock rule, and the readers let us check the result. Instance fields keep each bin's stock separate, while the static field records constructions for the class.

Suppose the next request is for zero pens, followed by a request for exactly the remaining stock. What should each call return, what stock should remain after each one, and should either call change Bins? Explain which part of the method supports your answer.
