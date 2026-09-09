**Interface** - A named Java type that describes a shared capability. The keyword `interface` introduces a definition such as `interface Labelled { String label(); }`. This required declaration names an operation but supplies no body. Interfaces can also contain default methods with bodies, so “an interface never contains working code” is not a general rule.

**Abstraction** - Describing what an operation promises while leaving its implementation elsewhere. A label operation promises a useful String without telling the caller which field stores the text. Abstraction lets the caller work with that promise. It does not remove the need for a class to perform the work or for tests to check that the returned label is meaningful.

**Interface implementation** - A class's declared relationship to an interface and the behavior that fulfills its requirements. In `class RoomLabel implements Labelled`, the keyword `implements` establishes the relationship. A public `String label()` method supplies the required result. A similarly named method with different parameters or private access would not fulfill this declaration.

**@Override annotation** - Information asking the Java compiler to check that a method implements or overrides an operation from a supertype—a type that the class extends or implements. Placing `@Override` before RoomLabel's label method can reveal a misspelled method name. It is an annotation, not a language keyword or method call. Removing it does not repair an unimplemented interface requirement.

**Interface-typed reference** - A reference variable whose declared type is an interface. In `TextProvider message = new FixedText("Open");`, the declared type exposes `text()`, while the actual object remains a FixedText. The assignment does not construct another object or change its class. A FixedText-only method is not automatically available through message.

**Polymorphic method call (method dispatch)** - An instance-method call whose implementation is selected using the receiving object's class. A loop can call `greeting.words()` for both a MorningGreeting and an EveningGreeting. The loop statement stays the same while the returned text changes. The declared type still controls which operation the caller may request; runtime method selection does not make every method available through that reference.

**Default interface method** - An interface instance method with a body that an implementing class may inherit or override. The keyword `default` marks this body, as in an announcement method that returns `"Ready: " + label()`. Its inner label call uses the same receiving object. A default method supplies shared behavior, but it does not create shared instance fields in the interface.

**Class inheritance** - A relationship in which a more specific class extends another class and inherits eligible members. The keyword `extends` declares the relationship in `class VisitorCard extends NameCard`. It can keep common behavior in one definition. Java classes have one direct superclass, and constructors are not inherited. Similar-looking code alone does not prove that a subclass relationship is appropriate.

**Superclass** - The base class that a subclass extends. NameCard is VisitorCard's superclass and stores the common name. A superclass can provide working methods that a subclass uses or overrides. Initializing the superclass portion of a VisitorCard does not create a separate NameCard object beside it.

**Subclass** - A class defined by extending a superclass. VisitorCard is a subclass of NameCard; it can reuse the inherited label method or provide a more specific version. Its objects must still honor the base operations. Extending a class does not give subclass code unrestricted direct access to the superclass's private fields.

**Superclass constructor call** - An explicit call that passes initialization arguments to the superclass constructor. In this course's Java 21 runtime, `super(name)` comes first in the subclass constructor body. It initializes the base portion of the same object. In the constructors used here, omitting it implies a no-argument superclass call, which will not satisfy a base constructor that requires a name.

**Method overriding** - Supplying a subclass implementation of an inherited instance method. VisitorCard can override `label()` and return the name followed by ` visitor`. An ordinary label call on that object selects the override even through a NameCard reference. Changing the parameter list can define a different operation rather than override the intended one; `@Override` helps check the relationship.

**Superclass method call** - A call such as `super.label()` that deliberately uses the superclass implementation from subclass code. VisitorCard can obtain the base name, then append its own suffix. This is a method call on the same object, not a constructor invocation. Calling plain `label()` from inside the override would re-enter the override instead of requesting the base result.

**Abstract class** - A class marked with the keyword `abstract` that cannot be constructed directly. NamedJob can store a name, initialize it through a constructor, provide a description, and require a minutes calculation. A concrete subclass supplies the missing behavior. An abstract class can have working methods and need not consist only of abstract declarations.

**Abstract method** - A required operation declared without an implementation body. In `public abstract int minutes();`, the semicolon ends the declaration because no calculation is supplied. A concrete subclass must have an implementation for the remaining required operation. Merely declaring a subclass or adding `@Override` does not provide that body.

**Concrete class** - A class that can be instantiated and has implementations for its required abstract operations. PackingWork supplies the minutes calculation for a nonnegative box count, so `new PackingWork(2)` can create a work object. The class may inherit some implementations rather than declare all of them itself. Being concrete does not prove that its calculations are correct for the task.

**Protected access** - Access within the declaring package and from subclasses under Java's subclass-access rules. The keyword `protected` can mark a getter that a subclass calls on its current object while the backing field remains private. Protected does not mean “subclasses only.” Access across packages through other object references has additional restrictions.

**Package** - A named grouping of related Java types. Packages help explain access boundaries: code in the declaring package can access a protected member even without being a subclass. A package is not an object and does not create shared instance state. This module introduces the term to explain access; it does not require organizing a multi-package application.

**Generics** - Definitions that use type parameters to describe relationships among inputs, stored data, and results. One holder definition can support String values in one use and Integer values in another. The compiler checks that operations fit the selected types. Those checks cannot decide whether a correctly typed value is the value the task intended.

**Type parameter** - A name for a type placeholder declared by a generic class or interface. T in `Holder<T>` connects the field, constructor input, and getter result. It describes a type relationship; it is not a variable containing the message Open. A class and an interface can each declare their own T, with an implements clause connecting the two declarations.

**Generic class** - A class definition that uses one or more type parameters. Holder<T> can store a private T value and return T from get. Using Holder<String> and Holder<Integer> reuses the definition with different type choices. Separately constructed objects still have separate fields; choosing the same type argument for two objects does not make their state shared.

**Type argument** - A specific type selected when using a generic definition. String is the type argument in `Holder<String>`, while `"Open"` is a value passed to its constructor. Generic type arguments use reference types, so Integer is used instead of primitive int. Selecting a type does not supply an initial value or construct an object by itself.

**Generic interface** - An interface that uses type parameters to relate its operations. Sequence<T> accepts T through add and returns T through get, while size returns an int count. Shelf<T> connects its class parameter to that promise with `implements Sequence<T>`. Each implementation must preserve the agreed types; get does not return whichever type a caller happens to request.

**Compile-time generic type checking** - Compiler checks that a generic use fits its selected type relationships. Supplying `"7"` to a Sequence<Integer> is incompatible because quoted digits are a String. Supplying the number 8 may have the right type but still produce the wrong total. Output tests remain necessary, and generic type checks do not make an out-of-range index valid.
