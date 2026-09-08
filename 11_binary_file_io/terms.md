**Byte stream** - A sequence of bytes read or written without treating every byte as text.
**DataOutputStream** - A wrapper that writes primitive Java values to an underlying byte stream.
**DataInputStream** - A wrapper that reads primitive Java values from an underlying byte stream.
**Typed binary output** - Writing primitive values through matching data-stream operations.
**Typed binary input** - Reading encoded primitive values through matching data-stream operations.
**Binary record schema** - The agreed field types and order used by the writer and reader.
**Incomplete binary record** - An input ends before the required fields or bytes of a record have been read.
**EOFException** - An IOException subtype reporting that input ended before a required value could be read.
**Object serialization** - Writing an object state representation into an object output stream.
**Object deserialization** - Reconstructing an object from a compatible saved representation.
**ObjectOutputStream** - A stream that writes a supported Java object and its saved state.
**ObjectInputStream** - A stream that reconstructs objects from a compatible serialized representation.
**Serializable marker interface** - An interface with no required methods that marks support for Java object serialization.
**Serialization version identifier** - An explicit serialVersionUID used as part of class-version compatibility checks.
**Object** - The common superclass used to refer to an object before checking a more specific type.
**Runtime type check** - Using instanceof to test whether a non-null value is compatible with a reference type.
**Reference cast** - Requesting a more specific reference type when the actual object supports it.
**ClassCastException** - An exception reporting that an object cannot be used through the requested reference type.
**ClassNotFoundException** - A checked exception reporting that a required class definition could not be found.
**Transient instance field** - An instance field excluded from default serialization and restored with its default value unless custom handling supplies one.
