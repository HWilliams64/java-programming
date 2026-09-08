# Designing Static Methods

## Narration

Welcome to this Java tutorial, where you'll define static methods—named operations in a class—supply typed inputs, return results, and distinguish those results from printed output.

Keeping a calculation in one reusable method lets different parts of an application use the same rule, choose how to display its result, and test changes in one place.

A campus workshop needs totals for supply orders. Each order gives a whole-number item quantity and a price in dollars per item. We'll build one method that multiplies those inputs and returns the total in dollars. The caller, the code requesting the calculation, will decide what to print.

Success means different orders use the same calculation and receive their own results. We'll first work through example calls, then look at a copied numeric input and an output action. Finally, you'll predict two new totals before we run the completed order program.

Let's open Main.java in the Workspace and give the shared calculation a name.

PriceTools is a class, a container for this helper. Its static method can be called through the class name, without creating a separate PriceTools object. We'll name the operation orderTotal and declare the inputs it needs.

Quantity and unitPrice are parameters, the method's local input variables. Their types describe a whole-number count and a decimal price. The return type tells a caller what kind of result to expect. Here, double before the method name declares a decimal numeric result. Let's put the common multiplication in the body and return its value.

Return evaluates the product, ends this method call, and sends the number to its caller. It doesn't print. Declaring this helper hasn't performed an order calculation yet; we still need calls that supply values. We'll place those calls in Main. Main is the program's starting class, and its main method is where this application begins.

Our first example order has two items at three dollars each. Arguments are the values supplied at a call. Their positions match the declared parameters: two goes to quantity, and three point zero goes to unitPrice. The product is six dollars. We'll store that returned number in a caller variable before displaying it.

Total belongs to the caller. The assignment receives the completed method result, and println then reads total. A second order will use four items at two dollars each. It should return eight dollars. This time we'll pass the returned value directly to println.

Each call gets fresh parameter values. Java completes the inner calculation before the outer println can print it. Let's click Run to check both caller choices.

The first line is six point zero, and the second is eight point zero. One result was stored before printing; the other went directly to println. Both came from the same multiplication rule. Inspect the helper body: it reads only its parameters and returns a product. It doesn't print or change state outside itself. That makes this calculation pure; two matching observations alone wouldn't establish purity.

A method's input variable is separate from the caller's variable. Let's replace this example with a small helper that adds one to a copied quantity. This makes the separation visible before we return to the orders.

Java uses pass by value: a parameter receives a copy of the supplied value. For an integer, that copy is a number. The assignment inside addOne changes its own quantity parameter. It doesn't assign to a caller variable. We'll start the caller's requested quantity at three and store the returned result separately in revised.

The parameter receives three, changes its local copy to four, and returns four. Revised stores that returned value. Requested has never been reassigned, so it should still be three. We'll print the two caller variables in that order.

Let's run this complete program and inspect the two values left in the caller.

Requested prints three, while revised prints four. Returning didn't automatically replace the original argument variable. To change requested, the caller would have to store the returned result there. This example traces numeric values; it does not mean that Java copies an entire object whenever an object is passed.

A calculation can supply a result, but another method may be useful for an action. We'll replace the numeric helper with a display method. The keyword void means the call sends no value back. The print in this body is a side effect, an observable action beyond providing a return value.

ShowTotal receives a number and displays it with a label. We will put a caller message before and after the call so we can see when control enters the method and when it returns. The void call stands alone, because there is no returned value to assign or give to another println.

The caller should print its first message, the method should print the labeled total, and then the caller should continue with its last message. Let's run it to follow that order.

We see the caller's Before display, the method's Total line, and the caller's After display. The body finished and control returned without a result value. Void doesn't require a method to print; this particular body does. Likewise, static doesn't guarantee purity. Inspect what an operation actually does.

Now we'll return to the workshop calculation and keep output in the caller. We'll restore the same PriceTools method, then supply two new orders for your prediction. The rule has not changed.

The first order has three items at four dollars and fifty cents each. The second has five items at two dollars and fifty cents each. We'll call the helper once for each order, leaving both print statements in the main method.

Before we run this final program, write the two output lines you expect, in order. Match each argument to its parameter, calculate the product, and decide where printing occurs. Use the earlier worked calls as your model. Pause here if you want more time.

Let's click Run and compare both returned totals with your prediction.

The program prints thirteen point five, then twelve point five. Three items at four dollars and fifty cents cost thirteen dollars and fifty cents. Five items at two dollars and fifty cents cost twelve dollars and fifty cents. Each call received its own parameters and returned its own product. The caller printed each result after the calculation finished.

We've built one reusable rule and checked it with changing inputs. Typed parameters state what the calculation needs, and return supplies the result. The caller can store or display that value. The numeric-copy example showed that a parameter assignment is local, while the void example showed an action that returns control without returning a value.

Now use the notebook to build a discounted total method. Keep the calculation separate from printing, subtract the flat discount once, and test both stated orders and the zero-quantity case. Explain why the chosen inputs are allowed and why the body supports calling the calculation pure.

## Visual description

[Four code-free BHCC opening scenes show a vertical learning agenda, a horizontal inputs-to-shared-rule-to-caller diagram, a workshop order with quantity and price units, and a central returned-result card.]

[Main.java is opened and built in small groups while the camera follows the active typing. PriceTools defines a static calculation with typed parameters and a double return type. The caller stores the result for two items at 3.0 dollars each, then directly prints the result for four items at 2.0 dollars each. An actual mouse Run click produces 6.0 then 8.0.]

[The example is replaced with QuantityTools. Its addOne method changes a numeric parameter from 3 to 4. The caller stores the returned value separately. An actual Run click prints requested as 3 and revised as 4.]

[ReceiptDisplay demonstrates an action method with void return type. The caller prints Before display, invokes the method to print Total: 9.0, then resumes and prints After display. An actual Run click verifies the three lines.]

[The canonical PriceTools program below is restored. Students predict both results before the fourth actual Run click. The terminal prints 13.5 then 12.5. The closing distinguishes return values, numeric parameter copies, void actions, and the caller’s display choices, then directs students to construct and test the notebook’s discountedTotal method.]

## Canonical program

```java
class PriceTools {
    static double orderTotal(int quantity, double unitPrice) {
        return quantity * unitPrice;
    }
}

public class Main {
    public static void main(String[] args) {
        System.out.println(PriceTools.orderTotal(3, 4.5));
        System.out.println(PriceTools.orderTotal(5, 2.5));
    }
}
```

## Exact canonical output

```text
13.5
12.5
```

## Asset credits

Java logo: Material Icon Theme contributors (MIT), pinned commit db37396672f801195be1bf082cca76942deb8c24. Concept icons: Font Awesome Free 6.7.2 by Fonticons, Inc. (CC BY 4.0), recolored for the BHCC palette. Sources, licenses and original hashes are retained in production evidence.
