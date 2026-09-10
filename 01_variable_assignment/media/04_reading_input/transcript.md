# Transcript: Reading Keyboard Input with Scanner

Welcome to this Java tutorial, where you'll learn to read keyboard input with Scanner and choose methods for text, whole numbers, and decimal values.

Interactive programs can respond to new information while they run. Reading text and parsing numbers, which means converting numeric text into a numeric value, lets software collect requests and calculate useful results without editing its source code.

A campus workshop assistant needs a small receipt program. The person at the keyboard will enter a full attendee name, a one-word kit code, a whole-number quantity, a dollar price per kit, and a pickup location. We'll ask for one response on each line and use a decimal point in the price.

The program should display the attendee, kit quantity and code, calculated cost, and pickup location. Names and locations must keep their spaces. We'll run the completed program twice with different keyboard responses to check that the same instructions handle both requests.

Let's open Main.java in the Workspace and build the receipt program. Main is the class that contains our code. Its main method is the named operation where this program starts. We'll put our input and receipt statements inside that method.

Before we can ask for responses, we need a reader connected to the keyboard. The import makes the Scanner type available. The word new creates a Scanner object, and System.in is standard input, the stream that receives what we type into this running terminal.

Our keyboard variable now refers to that reader. A prompt is a message that tells the person what to enter. We'll print the name prompt before reading. The nextLine method returns a String containing the rest of a line, including spaces, and consumes its ending line break. The trim method removes spaces only from the ends of that returned name.

This read waits when no complete line is available. Pressing Enter completes our name response. A kit code has a different shape: it must be one word. A token is one piece of input separated by whitespace, such as spaces or line breaks. The next method returns a String token. It skips leading whitespace and stops before the whitespace after that token, so it does not return a whole multiword line.

Quantity must support arithmetic, so a String token is not enough. The nextInt method skips leading whitespace and parses the next token into an int, a whole-number value. The parsing happens before the value is assigned to quantity. A word such as three would fail this numeric read; we'll study input validation later.

The price can include a fraction of a dollar. The nextDouble method parses the next token into a double value. For this Workspace, enter a decimal point, as in four point five. Both numeric methods leave the delimiter after their token unread. A delimiter is a separator; Scanner uses whitespace by default.

Here is the boundary we must handle. After the price token, pressing Enter has also supplied a line break. The next line read would return the rest of that price line, which is empty when we typed only the price. We consume that remainder first, then ask for the pickup location on its own new line.

The extra nextLine call does not read the future pickup response. It finishes the current price line. If meaningful text followed a number on the same line, this call would consume that text too, so don't discard a line remainder blindly. Our prompts deliberately request one response per line. The following nextLine keeps spaces in the pickup location.

With both numeric values available, we can multiply quantity by price and display the receipt. We'll combine the stored text and numbers using the printing and String skills from the earlier lessons.

The calculation uses numeric values; the print statements then turn the results into readable messages. Let's run the completed program with the toolbar play button. For each visible prompt, I'll focus the terminal, type a response, and press Enter. Watch how each read waits for its own response.

Maya's full name and Student Center both kept their spaces. Three art kits at four dollars and fifty cents each produced thirteen dollars and fifty cents. Java displays that double as thirteen point five here; currency formatting comes later. The pickup prompt waited for our new line, so the leftover price line did not skip the location.

Now apply the same reasoning to another request. Without changing the source, we'll enter Nora Patel, art, four kits, a price of one point five dollars, and Library Desk. Predict the total and whether the full pickup location will appear. Pause the video to make your prediction before the second run.

The second receipt shows Nora Patel, four art kits, a total of six dollars, and Library Desk. Four times one point five is six. The source stayed unchanged; only the keyboard responses changed. We have tested two real requests, including spaces in both names and locations.

Scanner connected our program to standard input. We chose nextLine for whole-line text, next for a single token, nextInt for quantity, and nextDouble for price. Handling the price line remainder let the pickup read wait correctly. For another workshop, which fields would need a whole-line read, and where would you need to account for a token read's remaining line break?


## Visual description and demonstrated program

The video opens with four animated scenes: Scanner learning outcomes, the value of runtime input, a campus workshop request, and the expected receipt. In the live Workspace, the instructor types Main.java in small groups. The camera follows the active code. The visible toolbar play button starts each run. After each prompt appears, the terminal receives visible keyboard typing followed by Enter. The second run uses the same source.

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner keyboard = new Scanner(System.in);
        System.out.println("Full name:");
        String customer = keyboard.nextLine().trim();
        System.out.println("Kit code (one word):");
        String kitCode = keyboard.next();
        System.out.println("Number of kits:");
        int quantity = keyboard.nextInt();
        System.out.println("Price per kit in dollars (use a decimal point):");
        double price = keyboard.nextDouble();
        keyboard.nextLine();
        System.out.println("Pickup location:");
        String pickup = keyboard.nextLine();
        double total = quantity * price;
        System.out.println(customer + ": " + quantity + " " + kitCode + " kits");
        System.out.println("Total: $" + total);
        System.out.println("Pickup: " + pickup);
    }
}
```

## First run: typed responses and verified result

Responses, one line each: Maya Chen; art; 3; 4.5; Student Center.

```text
Maya Chen: 3 art kits
Total: $13.5
Pickup: Student Center
```

## Second run: typed responses and verified result

Responses, one line each: Nora Patel; art; 4; 1.5; Library Desk.

```text
Nora Patel: 4 art kits
Total: $6.0
Pickup: Library Desk
```

Each run first displays the prompts Full name, Kit code (one word), Number of kits, Price per kit in dollars (use a decimal point), and Pickup location. The closing connects these results to Scanner, whole-line versus token input, numeric parsing, and the price line remainder.
