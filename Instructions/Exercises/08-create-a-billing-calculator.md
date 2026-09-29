---
lab:
    title: 'Create a billing calculator'
    description: 'Write a C# program that organizes tax and total calculations into a Billing namespace, using methods with default parameters, named arguments, and return values.'
    level: 100
    duration: 25
    islab: true
    status: 'released'
---

# Create a billing calculator

In this exercise, you build a small billing calculator for a store. You organize your tax and total calculations into their own file under a `Billing` namespace, then bring that namespace into your main program with a `using` directive. You practice defining methods with parameters and return values, giving a parameter a default value, overriding that default with a named argument, and calling methods through the class name they belong to.

This exercise takes approximately **25** minutes.

## Set up your workspace

You'll write and run your code in Visual Studio Code. The starter code for this exercise lives in a GitHub repository — you'll clone that repo now if you haven't already.

> **Tip**: If you've already cloned the repo during another exercise, skip to the next section.

1. Open a new **Visual Studio Code** window (**File > New Window**).

1. On the Welcome page, select **Clone Git Repository...** (or open the Command Palette with **Ctrl+Shift+P** and run **Git: Clone**).

1. Paste the following URL and press **Enter**:

    ```
    https://github.com/MicrosoftLearning/mslearn-csharp-programming.git
    ```

1. When the file selection dialog appears, create a new folder in a convenient location to hold the repo (for example, `mslearn-csharp`), select it, and click **Select as Repository Destination**.

1. After the clone completes, select **Open** to open the folder in VS Code.

## Review the starter code

1. In the VS Code file explorer, navigate to the `Labfiles/08-create-a-billing-calculator` subfolder.

1. Select the `Billing.cs` file. It contains an empty shell for a `Calculator` class inside a `Billing` namespace — you'll add methods to it in the next section:

    ```csharp
    namespace Billing
    {
        public static class Calculator
        {
            // Add the CalculateTax and CalculateTotal methods here
        }
    }
    ```

1. Now select the `Program.cs` file. You'll see a set of guiding comments that act as an outline for your program — each one marks where a specific piece of code belongs:

    ```csharp
    // Bring in the Billing namespace

    // Set up the order

    // Calculate tax and total

    // Print the receipt
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code. In the steps that follow, you'll add code beneath each comment.

1. If VS Code shows a prompt about restoring project dependencies, select **Restore**.

## Add tax and total methods to the Billing namespace

Grouping related methods under a namespace keeps a growing project organized, and makes it clear at a glance where a method comes from.

1. In `Billing.cs`, replace the `// Add the CalculateTax and CalculateTotal methods here` comment with the following methods:

    ```csharp
    public static double CalculateTax(double subtotal, double taxRate = 0.08)
    {
        return subtotal * taxRate;
    }

    public static double CalculateTotal(double subtotal, double tax)
    {
        return subtotal + tax;
    }
    ```

    - `taxRate = 0.08` gives the parameter a **default value**. If a caller doesn't supply a tax rate, `8%` is used automatically.
    - Both methods declare `double` as their return type and use `return` to hand a usable value back to whatever code calls them.

1. Save `Billing.cs`.

## Bring the Billing namespace into Program.cs

`Billing.cs` and `Program.cs` are two separate files in the same project, so you use a `using` directive to bring the `Billing` namespace into scope before you can call `Calculator`'s methods by name.

1. In `Program.cs`, beneath the `// Bring in the Billing namespace` comment, add the following line:

    ```csharp
    using Billing;
    ```

1. Beneath the `// Set up the order` comment, add the following line:

    ```csharp
    double subtotal = 49.99;
    ```

1. Beneath the `// Calculate tax and total` comment, add the following lines:

    ```csharp
    double tax = Calculator.CalculateTax(subtotal);
    double total = Calculator.CalculateTotal(subtotal, tax);
    ```

    - `Calculator.CalculateTax(subtotal)` calls the method through its class name, `Calculator`. Since no tax rate is supplied, the default value of `0.08` is used.
    - The returned `tax` value is then passed straight into `CalculateTotal`, which returns the final amount due.

1. Beneath the `// Print the receipt` comment, add the following lines:

    ```csharp
    Console.WriteLine($"Subtotal: {subtotal:C}");
    Console.WriteLine($"Tax:      {tax:C}");
    Console.WriteLine($"Total:    {total:C}");
    ```

    The `:C` format specifier displays each number as currency.

1. Save the file, then run your program. Open a new terminal (**Terminal > New Terminal**), navigate to the project folder, and run the program:

    ```bash
    cd Labfiles/08-create-a-billing-calculator
    dotnet run
    ```

    You should see something like:

    ```output
    Subtotal: $49.99
    Tax:      $4.00
    Total:    $53.99
    ```

    > **Tip**: If you have the C# Dev Kit extension installed, you can also select the **Run** button that appears above your code instead of using the terminal. You only need to `cd` into the project folder once per terminal session — after that, `dotnet run` alone will work for the rest of this exercise.

## Override the default with a named argument

Not every order uses the standard tax rate. You'll add a second order that passes a different rate using a **named argument**, which makes the call easy to read even though it skips over the default.

1. Beneath your existing code (but still above the `// Print the receipt` output, or after it — either works), add a second order:

    ```csharp
    double outOfStateSubtotal = 80.00;
    double outOfStateTax = Calculator.CalculateTax(outOfStateSubtotal, taxRate: 0.05);
    double outOfStateTotal = Calculator.CalculateTotal(outOfStateSubtotal, outOfStateTax);

    Console.WriteLine($"\nOut-of-state subtotal: {outOfStateSubtotal:C}");
    Console.WriteLine($"Out-of-state tax:      {outOfStateTax:C}");
    Console.WriteLine($"Out-of-state total:    {outOfStateTotal:C}");
    ```

    - `taxRate: 0.05` names the parameter explicitly, overriding its `0.08` default with `5%` for this order.
    - Named arguments make the call self-documenting — anyone reading `taxRate: 0.05` immediately knows what that `0.05` represents, without needing to check the method's parameter order.

1. Run the program again with `dotnet run`. You should now see both receipts printed, each using a different tax rate.

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try each prompt below, read the response carefully, and test the code examples it gives you in VS Code.

### Discovery 1: Read a missing-namespace error

**AI Prompt:**
> "In C#, what compiler error do I get if I try to use a class from a namespace without a using directive for it? How do I read that error message to figure out the fix?"

**After the AI responds:** Try commenting out your `using Billing;` line at the top of `Program.cs` and running `dotnet run` again. Read the compiler error that appears in your terminal, then use what the AI told you to explain, in your own words, what the error is telling you. When you're done, uncomment the `using Billing;` line so your program runs again.

<details>
<summary>Show answer</summary>
Without the `using Billing;` directive, the compiler doesn't know where to find `Calculator`, so it reports something like `CS0103: The name 'Calculator' does not exist in the current context`. The fix is to either add back the `using` directive, or refer to the class by its full name, `Billing.Calculator`, every time you call it.
</details>

### Discovery 2: Give the Calculator class a shorter alias

**AI Prompt:**
> "In C#, how can I create a shorter alias for a class from another namespace using a using directive?"

**After the AI responds:** Take a look at the examples the AI gives you, then try adding a `using` alias for `Calculator` at the top of `Program.cs`, and update your method calls to use the shorter name instead.

<details>
<summary>Show answer</summary>
A `using` directive with `=` creates an alias for a type's full name:

```csharp
using Calc = Billing.Calculator;
```

You can then call its methods through the shorter alias instead of the original class name:

```csharp
double tax = Calc.CalculateTax(subtotal);
double total = Calc.CalculateTotal(subtotal, tax);
```
</details>
