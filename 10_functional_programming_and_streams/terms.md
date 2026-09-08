**Functional interface** - An interface whose single abstract method describes one operation that a lambda can provide.
**Function** - A functional interface whose apply operation accepts one input and returns a result; its two type arguments describe those types.
**Lambda expression** - An expression that supplies parameter-and-body behavior for a compatible functional interface.
**Behavior as an argument** - Passing a functional-interface value so a method can invoke the supplied rule.
**Captured local value** - A lambda can use an enclosing local value that is final or effectively final.
**final** - A Java modifier that prevents reassignment after a variable receives its initial value.
**Effectively final** - A local variable or parameter whose assigned value is not reassigned, allowing its value to be used by a lambda.
**Method reference** - A compact way to supply compatible behavior by referring to an existing method.
**Stream pipeline** - A source and sequence of operations that describe a computation over elements.
**Intermediate operation** - An operation that produces another stream stage.
**Terminal operation** - An operation that triggers a pipeline and produces its final result or effect.
**List** - An interface for an ordered collection of entries; a particular implementation decides which editing operations it supports.
**Unmodifiable result list** - A result list that rejects adding, removing, or replacing its entries; make a separate collection copy when edits are needed.
**Mapping elements** - Applying a function to each processed element to obtain a result element.
**Encounter order** - The order defined by a source, such as list order, which an ordered result preserves.
**Lazy evaluation** - The pipeline describes work before a terminal operation starts processing elements.
**Late-bound collection source** - An ArrayList stream observes source contents when terminal processing begins, not when the pipeline is first created.
**Single-use stream** - A stream must not be reused after a terminal operation; create a new stream for another computation.
**IllegalStateException** - An exception reporting that an operation is invalid for the current object state, such as reusing the consumed stream shown here.
**UnsupportedOperationException** - An exception reporting that an object does not support the requested operation, such as adding to a toList result.
**Collection copy** - Creating a new collection containing the current elements of another collection.
**Shallow copy** - A new collection containing references to the same element objects; editing membership is separate from changing an element object.
**Reduction** - Combining processed elements into one result.
**BinaryOperator** - A functional interface for an operation with two inputs and a result of the same type.
**Identity value** - A neutral starting value that does not change the combined result.
**Associative combination** - Regrouping a combination without changing its result.
**Parallel stream processing** - Allowing different parts of pipeline work to run at the same time, then combining their partial results.
**Stateless behavior** - A processing rule that does not depend on changing shared state.
**Noninterference** - Leaving the stream source unchanged while its pipeline executes.
