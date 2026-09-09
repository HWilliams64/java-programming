# Reading and Writing Binary Records — video transcript

## Narration

Welcome to this Java tutorial, where you'll write and restore a binary record, a group of stored values whose types, order, and meanings follow a shared agreement.

Typed binary input and output help applications exchange saved values reliably, while a shared field agreement lets the reading code recover what those values mean for a booking, a setting, or a game record.

A campus event desk has four seats available at two dollars and fifty cents per seat, and booking is open. We will save that offer in a private temporary file, then restore its count, price, and booking status.

The recovered report should show four seats, a price of two point five, and true for open status. The writer and reader must agree on an integer, a double, and a boolean, in that order. After reading, we will remove only this example's file.

Now that we're in the Workspace, let's open Main.java and build the record program.

We need the two data-stream types for primitive values, plus Files and Path for the file location. Main is the class containing this program. Its main method is where execution begins; we will place the record operations inside it.

The imports let us use those short library names. The throws declaration allows a checked I/O failure to leave this main method. It does not catch the failure or create a default record. Next, we need one owned file for the two phases.

CreateTempFile makes a new empty temporary file and returns its Path. The prefix helps identify the name, generated characters distinguish it, and the suffix is dot bin. The suffix does not choose a format. We keep the returned path so the writer, reader, and final cleanup use the same file.

First, open byte output and wrap it with typed writing operations. Then write the seat count, price, and booking flag in their agreed order.

The Files call opens the byte stream. DataOutputStream adds operations that represent primitive Java values. Each write adds its value after the previous one. We stored the values, not their variable names or the labels that will appear in the report.

The writer closes as its resource block ends, including its underlying byte stream. We can now open a separate reader at the beginning and recover the same three types in the same order.

The first read receives the integer seat count. The next receives the double price, and the last receives the boolean status. Each call advances through the required input. The reader does not search for a name; its sequence and assignments give each recovered value its meaning.

All required values are now available for the report. We will print each label beside its restored variable, then end the reader block and remove our temporary file.

These labels are added to console output; they were not field labels in the file. The reader closes before finally performs deletion. Closing and deleting are separate actions. Finally also runs when the attempted record operations fail, although deletion can itself report an I/O failure.

The complete program follows one field agreement from writing through reading. Let's click Run and inspect the actual restored offer.

The report restores four seats, the price two point five, and true for booking open. Each typed read matches its write and its intended field meaning. The price is printed as a double value; this example does not add currency formatting. The following cleanup removes the file.

Now try a separate offer with seven seats, a price of three dollars and twenty-five cents, and booking closed. We will change only the three written values. The reader and all labels stay the same.

Before running, predict every named output line. Match each read with the value written at that position, and explain how its assigned variable is used by the report. Pause here to make your prediction.

Let's click Run and compare your prediction with the new record.

The restored report shows seven seats, price three point two five, and false for open status. False is an actual value written into this complete record. It is different from omitting the required flag, which would leave the boolean read without enough input. Replaying the complete program creates another private file.

You used typed output and input to recover the event desk's offer with the same field types, order, and meanings. The notebook also shows why successful same-type reads can assign wrong meanings, and why an incomplete required field is a separate failure. Those checks go beyond confirming that a program reached its last line.

For your next step, imagine two integer fields for a room number and an available-seat count. What must the reader know beyond their shared type to label them correctly? Explain why a complete read alone would not prove that those meanings were preserved.

## Visual description

[Four code-free opening scenes introduce binary records and typed input/output, connect a shared field agreement to saved-data uses, establish the campus event desk offer, and show the baseline report with type/order/meaning and cleanup requirements.]

[The real Workspace appears. Main.java opens and the camera follows actual typing of four imports, the Main class, and a main method declaring IOException. The program creates a new empty temporary file, opens typed output, writes an int of 4, a double of 2.5, and a boolean of true, closes the writer, then opens typed input and restores the same three fields. Console labels are added during printing. The reader closes and finally removes the owned file.]

[The pointer clicks the actual Run Code button. The terminal reports Seats: 4, Price: 2.5, and Open: true. Narration explains the restored values and their meanings.]

[Three visible line edits change the written values to 7, 3.25, and false. A prediction and pause precede the second actual Run Code click. Its report shows Seats: 7, Price: 3.25, and Open: false. The closing connects the matching schema to the event desk's recovered offer and asks why two integer fields still require distinct meanings. The same-type error and incomplete-record demonstrations are identified as notebook work, not shown executions in this video.]