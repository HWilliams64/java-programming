# Sets and Unique Values

## Narration

Welcome to this Java tutorial, where you'll use a HashSet to remember unique String values, check membership, and interpret boolean results that say whether an addition changed the set.

These operations help applications recognize repeated categories and build distinct-value reports, so another request for an existing kind isn't mistaken for a new kind of data.

A campus supply desk receives requests for pins and tags. Each name represents a kind of supply, not the number of physical items requested. The desk needs to recognize a repeated name and check which kinds it has recorded.

We'll report whether each addition changes membership, compare a query before and after adding an item, and display the distinct count. After that worked case, you'll predict a different request sequence before we run it.

Let's open Main.java and build the membership check.

Main is the class that contains our program, and its main method is where execution starts. We'll place the statements inside that method. The import makes the HashSet class name available for the collection we're about to create.

The program structure is ready. Now we'll create an empty set named items. String is the element type on both sides of the declaration, just as it was for an ArrayList of text. The new keyword creates this collection; the import alone doesn't create it.

The declaration gives the program an empty starting collection. A set keeps one representative of each equal value, and String equality compares the contents. Let's add a pin request and print the method's result so we can see whether that addition changed membership.

The first print will report true because pin starts absent. The add call stores the new member before its returned boolean is joined to the label. Next we'll try the same text again, then ask whether tag is present without adding it.

The repeated pin call will return false because an equal value is already present; it won't create a second pin member. Contains is a different question: it reads whether a value is present and doesn't remember a new value. Since tag hasn't been added, that query will return false too.

Those two false results describe different operations. One says the duplicate addition made no change; the other says tag is absent. We'll now add tag, query it again, and print the number of distinct members after the requests.

This standalone add changes membership without displaying its returned result. The following query will find tag, and size will count the distinct members. We are asking about values, not list indices or a promised traversal order. Let's click Run and check the complete worked case.

The first pin line is true and the repeated pin line is false. Tag before add is false, then Tag after add is true. The last line reports Unique: 2. Three addition attempts produced two distinct members, and the contains queries did not change that count.

A false add result is normal duplicate handling, not a Java error. The final count describes the different String values present, rather than the number of requests or the number of method calls. With that distinction established, we can apply the same rules to a new report.

Let's replace the worked program with the supply desk's map and kit report. We'll start a fresh empty set, then print the results of a first map request and another equal map request. Keep your predicted results to yourself while we enter the complete program.

The new setup and two labeled map attempts are in place. We'll add kit without printing that call's result, then ask whether kit is present and report the unique count. The final queries read the state left by the earlier additions.

The new program is complete. Before clicking Run, predict all four labeled output lines. Track whether each addition changes membership, and distinguish the query from the count. Pause here if you'd like more time to work through it.

Let's run this version and compare its output with your prediction.

First map is true because no equal map was present. Duplicate map is false because the first call already stored it. Adding kit supplies another distinct member, so Contains kit is true and Unique is two. The query reads membership without adding a third value.

The desk's report now distinguishes new and repeated names, checks the resulting membership, and counts distinct kinds. HashSet provides that membership rule, while each returned boolean tells us what its particular operation did. We didn't need to assume any order for visiting set members.

Suppose the desk asks whether pass is present but never adds it. What would that membership query report, and would it change the unique count? Explain which operation would be needed to remember pass for a later request.

## Visual description

Four distinct opening scenes show an unnumbered group of supply symbols beside membership goals; application rows about repetition and distinct-category reports; a supply desk and request sheet with pin and tag labels; and a report panel requiring change results, membership queries and a distinct count. The opening does not reveal the canonical output.

The real Workspace shows Main.java. Seven small groups of source are typed while the camera follows the editor. The worked program creates an empty HashSet of String values, tries pin twice, queries tag before and after adding it, and prints the distinct count. The actual Run Code toolbar button is clicked for each of two complete programs.

### Worked pin and tag

```java
import java.util.HashSet;
public class Main {
    public static void main(String[] args) {
        HashSet<String> items = new HashSet<String>();
        System.out.println("First pin: " + items.add("pin"));
        System.out.println("Repeated pin: " + items.add("pin"));
        System.out.println("Tag before add: " + items.contains("tag"));
        items.add("tag");
        System.out.println("Tag after add: " + items.contains("tag"));
        System.out.println("Unique: " + items.size());
    }
}
```

Actual output:

```text
First pin: true
Repeated pin: false
Tag before add: false
Tag after add: true
Unique: 2
```

### Canonical prediction

```java
import java.util.HashSet;
public class Main {
    public static void main(String[] args) {
        HashSet<String> items = new HashSet<String>();
        System.out.println("First map: " + items.add("map"));
        System.out.println("Duplicate map: " + items.add("map"));
        items.add("kit");
        System.out.println("Contains kit: " + items.contains("kit"));
        System.out.println("Unique: " + items.size());
    }
}
```

Actual output:

```text
First map: true
Duplicate map: false
Contains kit: true
Unique: 2
```

The editor is cleared before a fresh map-and-kit program is entered. Before that canonical run, an eight-second prediction pause leaves the source visible without the answer. The closing distinguishes change results, membership reads and a unique count, then asks about querying pass without adding it. That transfer answer stays hidden.

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0). Full license and source evidence are retained with the composition.
