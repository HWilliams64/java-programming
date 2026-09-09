**Byte** - A small unit of stored data; binary I/O transfers sequences of these units. Example: A successful readInt() consumes four bytes. Bytes need a format to give their contents meaning.
**Byte stream** - An input or output sequence used to transfer bytes. Example: Files.newInputStream(file). This is different from a collection-processing stream.
**Binary file** - A file interpreted using a binary format rather than as an ordinary text document. Example: seat-record-.bin. A .bin extension labels a file for people; it does not enforce the format.
**Files.newOutputStream** - A library method that opens a file for raw byte output. Example: Files.newOutputStream(file). The raw stream does not itself document application field meanings.
**Files.newInputStream** - A library method that opens a file for raw byte input. Example: Files.newInputStream(file). A Path by itself does not open the file.
**DataOutputStream** - A wrapper that adds primitive-value writing operations to byte output. Example: new DataOutputStream(Files.newOutputStream(file)). Closing this wrapper closes its underlying stream.
**Typed binary output** - Writing primitive values using operations that specify how each value is represented as bytes. Example: writer.writeInt(4). Variable names are not automatically saved as field labels.
**writeInt / writeDouble / writeBoolean** - DataOutputStream methods that write int, double, and boolean values at the current output position. Example: writer.writeDouble(2.5). Choose the operation from the field type and agreed order.
**DataInputStream** - A wrapper that reads primitive values from raw byte input. Example: new DataInputStream(Files.newInputStream(file)). It does not search the file for Java variable names.
**Typed binary input** - Reading the next bytes according to an agreed primitive type. Example: reader.readDouble(). The reader must use the same agreement as the writer.
**readInt / readDouble / readBoolean** - DataInputStream methods that read complete primitive representations and advance the input position. Example: reader.readBoolean(). An absent required boolean does not supply false.
**Binary record schema** - The agreed types, meanings and order of one group of values. Example: int seats, double price, boolean open. Record here is a group of fields, not the Java record declaration.
**Field order** - The positions in which a writer stores fields and a reader restores them. Example: room first; available second. Swapping two int meanings can succeed technically and still be wrong.
**Incomplete binary record** - A record that ends before every required field has been read. Example: room and available exist; open is absent. Compare to the complete schema, not merely file length.
**EOFException** - An end-of-file exception raised when a required read cannot obtain all needed data. Example: catch (EOFException exception). Not every IOException means the same failure, and no missing field should be silently invented.

**Object serialization** - The process of writing a representation of supported object state into an object output stream. Example: writer.writeObject(new LabelCard("lab")). This does not save source code, executable methods or a running kernel.

**ObjectOutputStream** - An object stream that writes supported object representations. Example: new ObjectOutputStream(Files.newOutputStream(file)). Its representation is not the primitive record format from Lesson 1.

**writeObject** - An ObjectOutputStream method that writes the supported value supplied as its argument. Example: writer.writeObject("lab"). Constructing a card elsewhere does not force that card to be stored.

**Object deserialization** - The process of reconstructing compatible object state from an object-stream representation. Example: reader.readObject(). Compatible class definitions are still required.

**ObjectInputStream** - An object stream that reads and reconstructs supported saved values. Example: new ObjectInputStream(Files.newInputStream(file)). Only read controlled files in this lesson; a later type check does not make arbitrary input safe.

**ClassNotFoundException** - An exception indicating that a class needed to restore an object could not be found. Example: readObject() may throw ClassNotFoundException. This differs from valid serialized data of an unexpected application type.

**readObject** - An ObjectInputStream method that restores a saved value and returns it through the declared result type Object. Example: Object value = reader.readObject(). The returned value need not be the card type your application expects.

**Marker interface** - An interface whose marker role does not require implementing a method. Example: implements Serializable. Contrast with an interface requiring an operation; do not invent a serialize method.

**Serializable** - The Java interface used to mark a class as supporting serialization. Example: class LabelCard implements Serializable. Saved referenced objects must also support serialization; String does.

**Serialization version identifier** - The class’s explicit identifier used as part of serialization compatibility checks. Example: serialVersionUID = 1L. Matching the identifier does not make every class change compatible.

**serialVersionUID** - The recognized class field naming an explicit serialization version. Example: private static final long serialVersionUID = 1L. This identifier is not a Java keyword or ordinary saved per-object field.

**final** - A Java keyword that prevents a declared variable from being reassigned after initialization. Example: final long serialVersionUID = 1L. A final reference does not by itself make the referenced object immutable.

**long** - A Java primitive type for signed 64-bit whole numbers. Here it holds the explicit serialization version value. Example: 1L. The L suffix makes 1L a long literal; it is not part of the variable name.

**Object** - Java’s common superclass type for class instances; a declared Object reference exposes Object-level operations. Example: Object value = reader.readObject(). It does not expose every method of the more specific object it refers to.

**Runtime type check** - A check of whether an actual value is compatible with a specified reference type. Example: value instanceof LabelCard. Check the value actually read, not a separately created original object.

**instanceof** - A Java keyword used to test whether a value is compatible with a named reference type. Example: value instanceof LabelCard. The condition is false for null; match the type required by the following cast.

**Reference cast** - An expression that gives a reference a specified type for accessing the same object. Example: (LabelCard) value. A cast does not turn a String into a LabelCard.

**ClassCastException** - An exception caused by attempting an incompatible reference cast. Example: (LabelCard) value when value is a String. Place the matching guard before the cast; a wrong guard does not help.

**Transient instance field** - An object field treated as temporary rather than ordinary saved state. Example: views is temporary; owner and points are saved. The original object retains its own value while another object is restored.

**transient** - A Java keyword that excludes an instance field from default serialization. Example: private transient int views. Do not exclude a business value that must survive restoration merely to match an output.

**Default restoration** - The ordinary serialization mechanism restores saved state without replaying these serializable classes’ constructors or field initializers. Example: transient boolean selected begins false. This scope excludes custom serialization and is not a claim that no superclass constructor ever runs.

**Default primitive value** - The initial primitive field value when no restored saved value or custom initialization supplies another. Example: An int field begins at 0; a boolean field begins at false. A constructor’s true or 1 assignment for original is not replayed for the restored serializable class.
