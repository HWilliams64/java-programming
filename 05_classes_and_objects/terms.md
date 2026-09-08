**Class as a state and behavior definition** - A reusable definition of the fields and operations its objects have. The Java keyword `class` begins a definition, as in `class WelcomePass { ... }`. The definition supplies a common design; writing it does not create a pass for a particular visitor.

**Instance field** - A variable stored separately in each object. In a pass class, `int visits;` declares a field that can retain that pass's count after a method call finishes. Fields appear inside the class body and outside constructor and method bodies. A same-named method parameter is a separate, temporary input.

**Object instance** - One object created from a class. Two separate `new WelcomePass(...)` expressions create two passes, each with its own instance fields. Both use the same class definition, but recording a visit for one does not change the other's count.

**State** - The values an object currently stores. A pass's owner and visit count describe its state at a particular point in execution. State can change as operations run; it is different from the class definition that supplies the common structure and rules.

**Behavior** - The operations an object can perform. For a pass, `visit()` changes the stored count according to the class's rule. Behavior describes what an operation does; the current count is state. Several objects can follow the same behavior while holding different values.

**Constructor** - The initialization operation invoked when a new object is created. Its name matches the class name, and its header has no return type, including no `void`. In `new WelcomePass("Zara")`, the constructor stores the supplied name and establishes the starting count. After it finishes, the new expression yields the object's reference; the constructor itself does not return a value.

**This reference** - The Java keyword `this` refers to the current object inside its constructor or instance method. In `this.owner = owner`, the left side names the object's field and the right side names the constructor parameter. The distinction prevents a temporary input from being confused with lasting state. An instance method's receiver determines which object `this` identifies.

**Instance method** - An operation called for a particular object that can use or change that object's state. A call such as `east.visit()` applies the method body to the pass reached through `east`. The method may return a value or use `void` when it has no returned result. Calling it does not itself create a new receiver or rerun that receiver's constructor.

**Receiver** - The object selected for an instance-method call. In `east.visit()`, the value of `east` identifies the receiver, and `this` refers to that object during the method body. A different reference in another call can select a different object while using the same method definition.

**Do not repeat yourself (DRY)** - Keep a shared rule in one definition instead of copying its implementation for every use. A pass class defines its visit increment once, and every pass can use that rule. Changing that definition changes the shared behavior; it does not combine the separate fields of different objects.

**Encapsulation** - Keeping an object's state behind operations that control how it changes. A stock record can hide its count and provide a method that checks a requested withdrawal before subtracting it. Encapsulation gives the class a place to enforce its rules. Merely moving a variable inside a class does not prevent outside code from changing an accessible field.

**Access control** - The Java rules that determine where a member can be accessed. The keyword `private` restricts access to the defining class and its permitted nested context; `public` allows access wherever the enclosing type is accessible. This module uses private fields and public operations so callers use the class's checks. These are source-code access rules, not passwords or runtime user permissions.

**State invariant** - A rule that must hold after an object's initialization and after each completed operation. A stock class might require its stored quantity to stay nonnegative. A withdrawal method preserves that rule by rejecting an invalid request before subtraction. Tests should check both the returned result and the state left behind.

**Precondition** - A rule the caller must satisfy before an operation begins. A constructor can require a nonnegative starting quantity even when its body does not test that condition. A stated precondition is not evidence that invalid input is automatically rejected. Use inputs that satisfy the lesson's constructor contract unless a task explicitly asks you to implement a check.

**Aliasing** - Two variables referring to the same object. After `second = first`, both references can reach the existing object; the assignment does not create a duplicate object. A field change through one reference is visible through the other. Creating objects with two separate new expressions gives a different arrangement.

**Mutation** - A change to an existing object's state. Calling an operation that decreases a stock object's quantity mutates that object. Reassigning a local reference variable instead changes which object that variable reaches. A method can mutate the caller's referenced object even though Java passes the reference value by value.

**Static field** - A field belonging to the class rather than a separate field in every instance. A construction counter declared with the keyword `static` can increase whenever that class's constructor runs. Its value counts whatever the program explicitly records; it does not automatically count live objects or references. Reusing a notebook kernel can preserve class state, so follow the lesson's fresh-state instructions when repeating such experiments.

**Logical size** - The number of elements a collection currently uses. A collection with three added scores has logical size three, even if its backing array has more positions. Logical indices run from zero through size minus one. An explicitly added zero is still an element and contributes to size.

**Capacity** - The number of positions available in the current backing array. An array of length four provides capacity four, even when only two positions belong to the logical collection. Capacity limits how many entries fit before growth is needed. It is different from the number already added and from the sum of their values.

**Array allocation** - Creating an array with a specified length. `new int[2]` creates an array with two positions whose valid indices are zero and one. The length of that particular array remains fixed. Growing a collection requires a different array and a change to the storage reference.

**Default element values** - The starting values assigned automatically to new array elements. An `int[]` starts with numeric zeros; a `String[]` starts with null references. A zero in an unused position does not prove that a student added a zero-valued score. Logical size identifies which positions belong to the collection.

**Backing storage** - The internal array that holds a collection's elements. A collection class can keep that array in a private field and expose operations such as `add`, `get`, and `size`. Callers then work with the collection's logical entries instead of relying on spare array positions. Protecting the reference helps the class maintain its size and capacity rules.

**Growth by copying** - Creating a larger array, copying the used elements in order, and replacing the backing-storage reference. When a collection with positive capacity becomes full, doubling its capacity makes room for another addition. The existing elements must be copied before the new element is appended at the old logical size. Increasing the size afterward keeps the stored entries and count consistent.
