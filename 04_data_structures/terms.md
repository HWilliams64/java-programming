**Data structure** - A way to organize values so a program can store, find, and process them. An array can keep a fixed sequence of tour stops, while a map can connect a supply name to its count. Choose the structure from the work the program must do. Preserving order, allowing repetitions, and finding a value by name are different requirements.

**Array** - An ordered sequence of elements whose length is fixed when the array is created. `String[] locations = {"desk", "lab"};` creates two positions for String values. The `[]` in the declared type means that `locations` refers to an array, rather than one String. Replacing a value in a position does not add or remove a position.

**Element** - One value stored at a position in a sequence or as a member of a collection. In the array `{"desk", "lab"}`, the two elements are the strings `"desk"` and `"lab"`. The array is the structure containing those elements. An element's value and its position are different: two positions may contain equal values.

**Array initializer** - A brace-enclosed list of the values that an array starts with. In `int[] quantities = {2, 0, 4};`, the initializer supplies three integer elements in that order. The empty initializer `{}` creates an array with length zero when used in an array declaration. Its braces describe starting data; they are not the body of a loop or method.

**Array element access** - Reading or replacing an array element through its index in square brackets. For a two-element array, `locations[1]` reads the second element, and `locations[1] = "studio";` replaces it. Valid indices start at zero and end one position before the array length. An index equal to the length is already outside the array, even though the index itself is an integer.

**Array length** - The number of positions in an array, read through its `length` field without parentheses. If an array has three elements, `locations.length` is `3`, and its last valid index is `2`. This count remains fixed for that array. By contrast, `locations[0].length()` asks the first String for its character-position count; it does not count array entries.

**Traversal** - Visiting a structure's elements according to a rule. An indexed array traversal starts at zero, reads the current element, and increases the index while it remains less than the length. The strict bound prevents an extra access beyond the last position. For an empty array, the first condition is false, so there is no element to visit.

**Enhanced for loop** - A Java loop that supplies successive element values to a local variable. In `for (int quantity : quantities)`, the keyword `for` introduces the loop, `int quantity` declares the current element variable, and the colon separates that declaration from the source array. This form is useful when the work needs each value without its index. It can also traverse the lists introduced in this module.

**Loop-local variable** - A variable used inside a loop whose declaration limits where its name can be used. In an enhanced loop over an `int[]`, each iteration receives the next integer value in its local variable. Assigning a different integer to that local variable does not replace the source array element. To replace an element at a particular position, use indexed assignment to that position.

**Running total** - A variable that keeps the sum accumulated so far. Starting with `int total = 0;`, the update `total = total + quantity;` adds the current quantity to the previous total. The starting declaration belongs before the loop so earlier additions are retained. Replacing the total with the current quantity would lose the amounts already processed.

**Conditional count** - A count that increases only when an entry meets a condition. A program can increase `nonempty` by one when `quantity > 0`, while adding the actual quantity to a separate total. For quantities `2`, `0`, and `4`, the sum is six units but only two entries are positive. The count measures qualifying entries; the total adds the amount from every entry.

**ArrayList** - A Java library class for an ordered collection whose size can change. An `ArrayList<String>` can hold volunteer names, including repeated equal names, in the sequence they were added. Its methods let a program append, read, replace, and remove entries. Changing the list's size differs from replacing an element in a fixed-length array. `ArrayList` is a class name, not a Java keyword.

**Ordered collection** - A group whose elements form a sequence of positions. An ArrayList preserves that sequence as entries are appended, replaced, or removed. Ordered does not mean alphabetically sorted. After removal, later entries shift to lower indices while keeping their relative order.

**Duplicate** - An entry whose value is equal to another entry in the same collection. A list containing Maya, Luis, and Maya has three entries, including two equal String values. ArrayList keeps both occurrences rather than merging them. In a sign-up report, equal submitted names do not by themselves prove that the entries came from the same person.

**Generic class** - A class whose use can specify the type of values it works with. In this module, `ArrayList<String>` says that a particular list holds String elements. The Java library supplies ArrayList; students are using that class rather than defining a new one. The type information helps Java reject an attempt to add a value of the wrong type.

**Type argument** - A type supplied inside angle brackets when using a generic class. Both occurrences of `<String>` in `ArrayList<String> names = new ArrayList<String>();` specify String elements for this list. Here, the keyword `new` creates the collection, while `ArrayList` names its class. Generic type arguments use reference types; the map lesson introduces `Integer` for storing whole numbers instead of writing `<int>`.

**List size** - The number of entries currently in a list, returned by `size()`. Appending increases this count, replacing an entry keeps it, and removing an entry reduces it. Use the current size when checking whether an index is valid. In `names.size()`, the parentheses belong to a method call; array `length` uses different syntax.

**List insertion** - Adding a new element to a list and increasing its size. The call `names.add("Maya")` appends Maya after the entries already present. Appending a second equal name keeps another entry; ArrayList does not remove repetitions automatically. Adding an entry is a different operation from replacing the value at an existing index.

**Indexed list access** - Reading a list element through its current index with `get`. If the first two names are Maya and Luis, `names.get(1)` returns Luis. List indices start at zero, just like array indices, but a list uses a method call rather than array brackets for this operation. The index must be less than the current size, so an empty list has no index zero to read.

**List replacement** - Changing the value at an existing list position without changing the list's size. In a list containing Maya and Luis, `names.set(1, "Nora")` replaces Luis with Nora and leaves two entries. The supplied index must already exist. Calling `set(0, ...)` cannot create the first entry of an empty list; append an entry or guard the replacement first.

**List removal** - Removing a list element so later elements move to lower indices. In the list Maya, Luis, Maya, the call `names.remove(0)` removes the first Maya and leaves Luis at index zero. The size falls from three to two. This lesson uses the method form whose argument is an integer index; it removes the element at that current position, not every equal value.

**Filtering a sequence** - Building a result sequence from the entries that meet a condition. A loop can read every source location and append it to a separate list only when it is not `"desk"`. Appending retained entries as they are encountered keeps their relative order and repetitions. This process leaves the source array available; it does not delete the rejected entries from that array.

**Set** - A collection that holds at most one member equal to a given value. For a set of strings, adding `"map"` twice still leaves only one member equal to `"map"`. This supports questions about uniqueness instead of questions about an entry's position. A set does not keep the number of times an equal value was requested; that information needs a separate count.

**Membership** - Whether a value equal to a requested value is present in a collection. After `items.add("kit")`, the call `items.contains("kit")` returns `true`. A membership check reads the current state without adding a new member. A `false` result means that no equal member is present; it does not report a count of earlier requests.

**Unique value** - A distinct value counted once under the collection's equality rule. In map, kit, map, the unique String values are map and kit, so there are two kinds despite three requests. For the sets in this lesson, equal text contents represent the same kind. Unique membership does not record how often each value occurred.

**HashSet** - A Java library class that uses hashing and equality to organize set membership. A `HashSet<String>` can record which supply names have already appeared. Its `add`, `remove`, `contains`, and `size` methods answer different questions about that membership. HashSet makes no promise that traversal will follow the order in which values were added.

**Change result** - A returned value that tells whether an operation changed the collection. HashSet `add` returns `true` for a newly added member and `false` when an equal member was already present. HashSet `remove` returns `true` when it removes a present member and `false` when no equal member was there. A false result is normal behavior, so it can guide an `if` statement without indicating an execution error.

**contains()** - A membership-query method that returns whether an equal value is present in a HashSet. After adding kit, `items.contains("kit")` returns true; asking about an absent pen returns false. The query does not add the requested value or change the set size. Its result reports current membership, rather than whether an operation changed it.

**Set removal** - Removing an equal member by value, using HashSet's `remove` method. If borrowed contains lamp, `borrowed.remove("lamp")` removes it and returns true; repeating the call returns false because no equal member remains. The argument is the value to find, not an index as in the ArrayList removal taught earlier. Removing an absent member is normal and leaves the size unchanged.

**Hashing** - Using a hash code to help narrow where a collection looks for a value. HashSet combines this lookup aid with equality checks to distinguish members. This supports membership operations without assigning students an array index for each member. The hash number does not describe the order in which the set will be traversed.

**Hash code** - An integer computed from a value and used to help locate it in a hash-based collection. For a String, `hashCode()` computes that number from its text. Equal strings have equal hash codes, but unequal strings can also share a code. A hash code therefore cannot replace an equality check or serve as a guaranteed unique identifier.

**Hash collision** - A case in which unequal values have the same hash code. The strings `"Aa"` and `"BB"` both have hash code `2112`, but their `equals` comparison is false. A HashSet can therefore keep both strings as distinct members. Sharing a hash code does not force two unequal values to become one member.

**Unspecified iteration order** - A collection provides no contract promising the order in which traversal visits its members or entries. HashSet and HashMap have this limit. An observed run may look sorted or match insertion order, but that appearance is not a guarantee for other data or runs. When report order matters, record and traverse an ordered structure such as a separate ArrayList.

**First-seen order** - The order in which distinct values first appear in an input sequence. In map, kit, map, pass, the first-seen order is map, kit, pass. A program can record each new value once in an ArrayList while a set checks uniqueness. Repeated occurrences do not append another entry, and the list supplies the final report order.

**Deduplication** - Keeping one representative of each group of equal values. A set can recognize whether a request has already appeared, but the program must still choose how to report the unique values. Appending to a separate list only when set `add` returns true creates a unique first-seen report. Appending every request to that list would retain duplicates even though the set itself is unique.

**Map** - A data structure that associates each distinct key with a value. A supply name can be the key, while its available quantity is the associated value. Looking up the name retrieves its recorded quantity. Distinct keys may have equal values, so the map's key count is different from both the sum of quantities and the number of distinct quantities.

**Key** - The value used to identify a map entry. In `stock.put("map", 2)`, the String `"map"` is the key and identifies the recorded supply quantity. Using an equal key again refers to that same association. The key is not an integer position like an array index, and changing its associated value does not add another equal key.

**Value in a map** - The information associated with a map entry's key. If `stock.put("map", 2)` has run, the recorded value for `"map"` is the number two in Integer form. A later `put` can replace that associated value. Two different supply names can each have a value of two; map values do not have to be unique.

**Map entry** - One key and its associated value considered together. An entry such as map → 2 connects a supply name to its recorded quantity. Adding a new distinct key creates another entry, while replacing a value under an existing key keeps the entry count unchanged. The arrow is a diagram of the relationship, not Java source syntax.

**HashMap** - A Java library class that uses hashing and equality to organize key/value entries. This module uses `HashMap<String, Integer>` for named whole-number quantities and counts. The class supplies methods such as `put`, `get`, `containsKey`, and `size`. Like HashSet, it does not promise first-seen traversal order; an ordered report needs a separate ordering rule.

**Integer** - Java's object form for a whole-number value of primitive type `int`. This library class lets a map use the type argument `Integer` when its values represent whole numbers. In `Integer saved = stock.get("map");`, the variable can refer to the returned Integer object. The capitalized class name `Integer` differs from the lowercase keyword `int` used for primitive integer variables.

**Wrapper type** - A Java library class whose objects represent values of a corresponding primitive type. Integer supplies the object form of int, so a `HashMap<String, Integer>` can associate names with whole-number values. Generic type arguments require reference types; writing `int` in place of Integer is not the same declaration. You use the library class rather than defining it yourself.

**Reference value** - A value that refers to an object rather than directly being a primitive number or boolean. When a successful map lookup returns an Integer, a variable such as `saved` holds a reference to that object. Printing it may display `7`, but that text does not make `saved` a primitive `int` variable. A reference alone also does not imply that a separate copy of the object has been created.

**Map replacement** - Storing a new value under a key that the map already contains. After `stock.put("map", 2)`, the call `stock.put("map", 3)` changes the associated quantity to three. The map still has one key equal to `"map"`. Its `size()` counts distinct keys, rather than counting how many `put` calls have been made.

**Lookup** - Retrieving recorded information by an identifying key. After `stock.put("map", 3)`, `stock.get("map")` supplies the associated Integer value. Reading the value does not change the key count. A missing key supplies null rather than numeric zero, so arithmetic requires the presence rule explained in the lesson.

**Boxing** - Converting a primitive value to the corresponding object form. Passing an `int` amount to a map with Integer values boxes the number for storage, as in `stock.put("badge", amount)`. Java can perform this conversion automatically in the appropriate context. The conversion does not change the original primitive variable into an Integer variable; its declared type stays `int`.

**Unboxing** - Obtaining the primitive value represented by an object such as an Integer. If `saved` refers to an Integer containing seven, the expression `saved + 1` unboxes seven for arithmetic and produces the primitive result eight. A later map `put` can box that new result for storage. Unboxing requires an actual object; a null reference cannot supply a primitive number.

**Key-presence check** - A test of whether a map contains an entry for a key, using `containsKey`. In the counting examples, a true result selects the branch that reads and increments an existing number. A false result selects the branch that starts a new count at one. An entry storing zero is present, so its presence result differs from the result for a missing entry.

**Null reference** - A reference value that does not refer to an object, written with the Java literal `null`. A HashMap lookup for a missing key returns null, which is different from a stored Integer representing zero. This module's counting examples store numeric values and never deliberately store null values. HashMap can store null values in general, so `containsKey` is the direct way to check whether an entry exists.

**Frequency table** - A mapping from each observed value to the number of times it occurs. A request-counting program stores one on a key's first appearance and increments the stored count on later appearances. The frequencies describe repeated occurrences, while map `size()` counts distinct keys. To print the frequencies in first-seen order, the program traverses a separate ordered list and looks up each final count.
