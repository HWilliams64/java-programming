# Throwing Exceptions and Preserving Causes — video transcript

## Narration

Welcome! In this Java tutorial, you'll throw custom exceptions to report application failures, declare checked exceptions that callers must handle or pass onward, and preserve an earlier failure as the cause.

These skills give other parts of an application a clear failure contract, so they can respond to invalid requests while keeping the diagnostic details developers need to investigate problems.

Today we'll build a quantity reader for campus supply staff. Each entry is text representing a requested number of items. Our rule accepts zero or a positive integer, and rejects words and negative quantities.

The reader should return an accepted quantity or explain why an entry failed. When number conversion fails first, we'll keep that original exception alongside our application message. Each request will receive its own response.

Now that we're in the Workspace, let's open Main.java.

The file is open. Our caller needs one application-specific kind of failure to handle, whether the text cannot become a number or the number breaks our quantity rule. Let's define InvalidQuantityException with a message and an optional earlier cause.

Extending Exception makes this a checked exception type. In ordinary Java method code, a checked failure that can escape must be caught or declared. The constructor forwards the message and cause to the parent constructor. Throwable is the common base type for throwable objects, so it can hold the earlier exception. A null cause means there is no earlier failure attached.

Now we need the reader that either produces a quantity or reports that checked failure. Let's add QuantityParser and its read method, then declare the integer that will hold a successful conversion.

The throws declaration belongs to the method header. It tells callers that InvalidQuantityException may escape; it does not raise an exception on every call. A successful call still returns an integer. That is our contract: a quantity on success, a named failure otherwise.

First we have to discover whether the text represents an integer. Parsing means converting that text into a value. Let's try Integer.parseInt and catch the conversion failure it can produce.

For text such as three, conversion supplies the integer three. A word such as two, written as letters, raises NumberFormatException instead. That is an unchecked exception, so Java does not require callers to catch or declare it. We catch it here because our application should report all invalid quantities through its own exception type.

The conversion has already failed when this handler runs. Let's give that failure a useful quantity message while keeping the original exception object as its cause.

Executing throw raises the new object and leaves this method without a returned quantity. The earlier NumberFormatException is still reachable through the new object's cause. We have added application context without discarding the original diagnostic. Since the method has left, the range check below will not run for that word.

If conversion succeeds, we still need to check the application's rule. A negative integer is a number, but it is not an acceptable request. Let's reject negative quantities and return values that pass.

This condition is validation: checking a value against an application rule. Negative one parses successfully, then fails this separate check. We pass null because there was no earlier conversion failure to preserve. Zero and positive integers reach return. The executed throw changes the path; the throws declaration describes that possibility to the caller.

Our reader is ready. Let's add Main, the class containing this standalone program, and main, the method where it starts. We'll prepare three independent text entries and handle each one inside its own loop iteration.

These inputs represent a request for three items, a word, and a negative quantity. They let us observe acceptance, conversion failure, and rule failure in one report. The try block belongs to a single request, so handling that request's failure can leave the next request available to process.

Let's print a returned quantity when reading succeeds. If the reader throws our checked exception instead, we'll print its application message and whether it retains an earlier cause.

Java must finish the read call before it can print Quantity. If read throws, that success line is skipped and the handler prints the problem. GetMessage retrieves our explanation. GetCause retrieves the earlier exception, or null; comparing it with null produces the true or false status. Let's click Run and examine all three responses.

The first entry prints Quantity: three because conversion succeeds and three is nonnegative. The word prints our whole-number message and Has cause: true, because the original conversion exception was retained. Negative one prints the negative-quantity message and Has cause: false. It was already a valid integer, so its rejection has no earlier parsing failure attached.

We now have evidence for both kinds of failure, and neither is confused with a returned quantity. Let's change only the input array to a boundary value, a different word, and another negative value. The reader and its rule will stay the same.

Before running, predict the complete report for zero, the word many, and negative four. Which entries return a quantity, and which failures retain an earlier cause? Use the two checks we just traced: conversion first, then the nonnegative rule. Pause here to make your prediction.

Let's click Run and compare the actual responses with your prediction.

Zero prints Quantity: zero. The rule rejects values below zero, so the boundary value is accepted. Many cannot convert to an integer; its application exception keeps the earlier cause. Negative four converts, then fails validation, so its cause is absent. The different messages and cause statuses explain different paths through the same method.

We built a quantity reader that returns acceptable values and gives callers a consistent way to handle failures. You used throw to raise a particular object, throws to declare a possible checked failure, and a cause to preserve an earlier exception. Those distinctions help callers respond appropriately while keeping useful diagnostic information.

For a transfer question, imagine the supply desk changes its rule to require at least one item. Which validation condition should change, and what should the caller observe for zero? Keep conversion and validation separate as you explain your answer.

## Visual description

[The video opens with four distinct code-free scenes in the BHCC red, blue, and white style. A custom-exception concept connects to raising a failure, declaring a checked failure, and preserving its cause. A horizontal application journey connects failed requests to caller responses and developer investigation. A supply-desk scene introduces campus staff, text quantity requests, and the nonnegative-integer rule. A report card previews an accepted quantity or an application failure with an earlier cause when one exists.]

[The real Workspace appears and Main.java opens. The camera follows the insertion point while code is typed. InvalidQuantityException extends Exception and forwards a message and cause to its parent constructor. QuantityParser.read declares that this checked exception may escape. It tries integer conversion, wraps a NumberFormatException with an application message and the original cause, rejects a negative parsed value with a null cause, and returns an accepted quantity.]

[The Main class and its main entry method process the text entries 3, two, and -1 independently. Each loop iteration prints a returned quantity or catches InvalidQuantityException and reports its message and whether a cause exists. The pointer moves to the native Run button and clicks. The report shows Quantity: 3, then the whole-number failure with Has cause: true, then the negative-quantity failure with Has cause: false. The explanation distinguishes conversion failure from validation failure.]

[The input array changes to 0, many, and -4. The video asks for a prediction and pauses before another visible Run-button click. Zero is accepted. The word many receives the whole-number message with a retained cause. Negative four receives the negative-quantity message without an earlier cause. The closing connects those observations to throw, throws, and exception causes, then asks how a minimum-one-item rule would change validation and the response for zero.]
