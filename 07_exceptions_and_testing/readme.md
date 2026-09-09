A reservation or equipment system must respond clearly when a request cannot be completed. This module traces how Java exceptions interrupt work and how a caller can handle a failure. You will state failure contracts, preserve useful causes, and release resources when work ends. You will finish by writing automated JUnit checks for ordinary inputs, boundaries, and required exceptions, then confirm that those checks detect a deliberate mismatch.

1. [Catching and Tracing Exceptions](01_catching_and_tracing_exceptions.ipynb) — Trace which statements run after an arithmetic failure inside a loop.
2. [Throwing and Exception Contracts](02_throwing_and_exception_contracts.ipynb) — Create a checked exception and either handle it or declare its propagation.
3. [Cleanup and Resources](03_cleanup_and_resources.ipynb) — Trace cleanup during normal work, return and an exception.
4. [JUnit Behavior Tests](04_junit_behavior_tests.ipynb) — Write JUnit Jupiter tests for normal, boundary and exceptional behavior.
