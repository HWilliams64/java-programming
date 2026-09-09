# Transcript: Building a Growable Collection

Welcome to this Java tutorial, where you'll build a growable collection using a backing array, logical size, and ordered copying.

Applications often collect more records than they start with. Understanding how storage grows helps you build reusable collections that accept new entries without losing earlier data or changing its order.

Today we'll help a campus signup coordinator record names in arrival order. We'll start with room for two names, then accept more. Each added name counts as one entry, and earlier signups must stay in their original positions.

We'll track used entries separately from available slots, make more room when needed, and print the names in signup order. A worked report will show size and capacity before and after growth. Then you'll predict a fresh case.

Now that we're in the Workspace, let's open Main.java.

Our collection needs storage for names and a count of entries actually added. Let's define GrowingNames, keep those fields private, and initialize them in its constructor.

Storage refers to the backing array, the array our class uses internally. Its length is capacity: the number of available slots. Size is the number of entries added so far. We begin with two slots but zero entries. New String array slots contain null, meaning no object reference; those empty slots are not signups.

An array cannot change its length. Our add method therefore needs to detect a full array and allocate a larger one before inserting another name. Let's write that decision.

When size equals storage length, every current slot is used. Larger refers to a new array with twice the capacity. That allocation creates room, but it has not moved any names. The original storage still holds the earlier signups.

We must preserve those signups before replacing the storage reference. Let's copy each used entry to the same index in the larger array, then make that array our backing storage.

The loop visits indexes from zero up to, but not including, size. Each assignment reads from the old array and writes to the matching position in the new one. After the loop, storage is reassigned to larger. Copying changes capacity, not the number of signups, so size stays unchanged.

Now there is space for the incoming name, whether growth was needed or not. Let's store it at the next unused position and then increase the entry count.

Before insertion, size is also the index of the next unused slot. We write there first and increase size afterward. Reversing those steps would skip a position and could write beyond the array. The growth check stays inside add, so every caller gets the same ordered insertion behavior.

The coordinator also needs to read a name and inspect both counts. Let's expose those values through public methods while keeping the fields private.

Get returns the entry at its supplied index. This small implementation assumes callers choose an index from zero up to, but not including, size; it does not check that precondition. Size returns the number of added entries. Capacity returns array length. Keeping those counts separate lets a report avoid unused slots.

The collection definition is ready. In Main, the main method will start our worked example. Let's create an empty collection and print its starting size and capacity.

Constructing GrowingNames runs the constructor once. The report should show zero entries and two slots. We'll now add Maya and Luis in that order and inspect the full state.

Maya occupies index zero and Luis occupies index one. After those calls, size reaches two, matching capacity. Neither call needed a larger array: each had a free slot when it began.

Nora arrives next. Let's add her name, report the grown state, and print only the names that have actually been added.

Nora's call begins with a full array. Add makes room, copies Maya and Luis, and inserts Nora after them. The reporting loop stops at size, so an unused slot cannot appear as another signup. Let's click Run to inspect both the counts and the order.

Start shows zero entries in two slots. Full shows two entries in two slots. Grown shows three entries in four slots: the third addition doubled capacity but added only one name. Maya, Luis, and Nora still print in arrival order. The spare fourth slot is omitted because the loop follows logical size.

Let's try a fresh collection with Iris, Owen, Bea, and Kai. We'll enter the same class again, then change the caller. Trace when each addition finds a free slot and when it must grow the backing array.

The constructor and copy logic are in place. Let's complete insertion and the readers. Remember that growing storage alone must not increase size; adding the new entry does that.

Now let's create the fresh collection in Main and add the four names. Each call sees the size and capacity left by the previous call.

The four additions are entered. Let's finish with separate size and capacity lines, followed by the entries in order. This report checks both storage behavior and preservation of earlier data.

Before running, predict all six output lines. Identify which addition needs a larger array, then decide whether the final addition fits. Also predict the order of the names and explain why no unused slot appears. Pause here if you need more time.

Let's click Run and compare the actual report with your prediction.

Size is four and capacity is four. Bea's third addition found the two-slot array full and grew it to four slots. Kai's fourth addition used the remaining slot, so it did not grow again. Iris, Owen, Bea, and Kai print in order because copying preserved their indexes and each new name was appended after the used entries.

The signup collection can now accept more entries than its starting array could hold. Logical size identifies the entries, capacity measures available space, and ordered copying preserves earlier records. The public add method keeps the grow, copy, and append sequence together for every caller.

If Zoe signs up next, what size and capacity should the report show, and which index should hold her name? Explain which entries would be copied and why the reporting loop should still use size rather than capacity.
