# Generic Classes and Interfaces — video transcript

## Narration

Welcome! In this Java tutorial, you'll write generic classes and interfaces: reusable definitions that keep input, stored-value, and result types consistent when callers choose different types.

Applications often need the same storage operations for different kinds of data. Generics let you reuse those operations while the compiler checks whether each caller supplies and receives compatible types.

Today we'll help campus workshop staff keep two separate collections: participant names and whole-number quiz scores. We'll store Maya and Luis in the names collection, and four and seven points in the scores collection.

One Shelf class will support both collections through a shared Sequence interface. We'll report the first name, the number of names, and the combined score. Then you'll predict the reports for a different set of inputs.

Now that we're in the Workspace, let's open Main.java.

The file is open. Both collections need to add a value, read a value by index, and report their size. Let's import the familiar ArrayList class and describe those operations in a generic Sequence interface.

T is a type parameter: a name for a type used consistently within this definition. Add accepts a T, and get returns a T. Size returns an int because an item count does not depend on the element type. T is not a stored value and is not a Java keyword.

The interface states the operations, but it does not store our entries. Let's define a generic Shelf class that implements Sequence and keeps its values in a private ArrayList.

Shelf declares its own type parameter. In implements Sequence, that parameter supplies the interface's type argument. The private list uses the same parameter, connecting the promised operations to compatible storage. Choosing String for a Shelf use connects those source-level types to String; it does not put the word String into the list as an entry.

Each shelf needs an initially empty list. Let's create that list in the constructor so a new shelf starts with its own storage.

This constructor creates an ArrayList and stores its reference in this shelf's private field. Calling the constructor again creates a separate shelf with a separate list. The two collections will share the class definition without sharing their entries.

Now we can supply the first interface operation. Let's implement add by passing its value to this shelf's private list.

The parameter and stored elements both use T, so the operation and the list agree about their type. Add changes the list by appending an entry; it returns no result value. The Override annotation asks the compiler to check that this method implements the intended interface operation.

Our caller also needs an indexed value and a count. Let's implement get and size by requesting those operations from the same private list.

Get returns the element at the requested index, using the familiar zero-based list positions. Size returns the number of entries. Neither call removes an entry. We'll use indexes that exist in our example; the generic type relationship does not make an invalid index valid.

The class is ready. Main contains the main method where this standalone example starts. Let's create a Shelf for String values, refer to it through Sequence of String, and add Maya followed by Luis.

String is the type argument here, while Maya and Luis are the values we store. The declared interface type makes the three promised operations available to the caller. Names now has Maya at index zero and Luis at index one. Let's print the first name and the number of entries.

The names reports are in place. We need the same operations for whole-number scores, so let's create a separate Shelf using Integer and add four and seven points.

Generic type arguments use reference types, which is why this declaration uses Integer rather than int. Java boxes each supplied whole-number value into the wrapper form used by the collection. These entries belong to the scores shelf; adding them does not change the names shelf.

To report the combined score, let's read both entries, add their values, and print the total.

The two get calls return Integer values. Java unboxes them for addition, and the result goes into the separate int variable total. Reading the values does not replace either list entry with the sum. Let's click Run and check all three reports.

First: Maya comes from index zero of names. Names: two confirms that its two entries are stored. Total: eleven comes from four points plus seven points in the separate scores collection. We used one class definition, two distinct objects, and the same interface operations with different element types.

These type relationships help reject an incompatible operation, such as supplying text to the Integer sequence. They do not tell us whether a numeric score is the score we intended. To check that part of the task, we still compare the program's results with known inputs and expected behavior.

We have explained the original reports. Let's keep the class and interface unchanged, then use Nora and Eli as the names and three and six as the scores.

Before running, predict the first name, the name count, and the total score. Trace which object each call reaches and which indexes it reads. Also consider whether calculating total changes either stored score. Pause here to work through your prediction.

Let's click Run and compare the reports with your prediction.

First: Nora is the entry at index zero. Names: two reflects the two names we added. Total: nine comes from three plus six. The score entries remain three and six because get reads them and the addition stores its result in total.

We wrote a generic interface and class that keep their operation and storage types consistent. Each caller chose a type argument, and each shelf kept its own values. The compiler checks compatible types; our result checks confirm the intended behavior. For another application, think of two kinds of data that could use these same operations and one wrong value that type checking alone would not catch.

## Visual description

[The code-free opening uses the BHCC red title band and Java icon. One reusable definition branches into text and number collections. A different horizontal layout connects incoming data, shared storage operations, and returned values, with a type-consistency band.]

[The task scene shows workshop staff beside separate cards for participant names Maya and Luis and quiz scores of four and seven points. The report scene reveals three fields: first name, number of names, and combined score. The two collections are separate; the diagram does not assign individual scores to named people.]

[The video enters the real Workspace and opens Main.java. The view follows the insertion point as code is typed. Sequence declares add, get, and size. Shelf implements that generic interface using a private ArrayList with the same type parameter. Its constructor creates a separate list for each shelf. The public methods delegate storage, retrieval, and counting to that list.]

[The Main class and main entry method create a String shelf for Maya and Luis, then a separate Integer shelf for four and seven. The caller prints the first name and number of names, retrieves both scores, adds their values, and prints the total. The view widens for caller explanations. The pointer moves to the editor Run button and clicks. The actual reports are First: Maya, Names: 2, and Total: 11.]

[Two small edits change only the names to Nora and Eli and the scores to three and six. The class and interface remain unchanged. The video pauses for a prediction before the second visible Run click. The new reports are First: Nora, Names: 2, and Total: 9. The closing keeps the completed code and output visible while connecting consistent types, separate state, and behavior tests to another application.]
