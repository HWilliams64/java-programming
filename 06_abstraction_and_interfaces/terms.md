**Abstraction** - Describing what an operation promises while leaving its implementation details to another part of the program.
**Interface** - A named Java type that states operations its implementations provide.
**Interface implementation** - A class uses implements and supplies the required public methods with matching names and parameters and compatible result types.
**@Override annotation** - A compiler-checked statement that a method implements or overrides an inherited method.
**Interface-typed reference** - A reference declared with an interface type that exposes its operations while referring to an implementing object.
**Polymorphic method call** - The same instance-method call can run different implementations according to the actual object.
**Default interface method** - An interface method with a body that an implementation may inherit or replace.
**Class inheritance** - Defining a subclass from one superclass so it can reuse accessible state and behavior.
**Superclass** - The base class named in a subclass’s extends clause.
**Subclass** - A class that extends another class.
**Superclass constructor call** - A super(...) call that initializes the base portion of an object; in the course’s Java 21 syntax it comes first in the constructor.
**Overriding inherited class behavior** - Providing a subclass implementation of an inherited instance method.
**Superclass method call** - A super.method(...) call that deliberately invokes an accessible base implementation.
**Abstract class** - A class that cannot be constructed directly and may combine implemented and required behavior.
**Abstract class method** - A method declaration with no body that a concrete subclass must implement unless an inherited implementation supplies it.
**Concrete class** - A class with the required implementations that can be used to create objects.
**Protected access** - Access within the declaring package and, under Java’s access rules, from subclasses.
**Package** - A named group of related Java types; this module uses the term to explain protected access.
**Type parameter** - A type placeholder, such as T, declared by a generic class or interface.
**Generic class** - A class definition that uses type parameters consistently for stored and exchanged values.
**Generic interface** - An operation contract that uses type parameters to relate method inputs and results.
**Compile-time generic type checking** - Checking type arguments and operations so an incompatible operation is rejected before that operation executes.
