---
lab:
    title: 'Build a tip calculator'
    description: 'Write a C# program that stores bill values as variables, performs arithmetic to calculate a tip and total, and accepts amounts as user input using type conversion.'
    level: 100
    duration: 20
    islab: true
    status: 'released'
---

# Build a tip calculator

In this exercise, you write a C# program that calculates a tip and total for a restaurant bill. You practice storing values in variables, performing arithmetic operations, and converting user input from text to numbers so you can use it in calculations.

This exercise takes approximately **20** minutes.

## Open the online C# IDE

1. Open a browser and navigate to the C# editor at [https://microsoftlearning.github.io/c-sharp-minor](https://microsoftlearning.github.io/c-sharp-minor).

1. You'll see two panels:
    - **Code Editor pane** (top): where you write your C# code.
    - **Output Console** (bottom): where output is displayed and where you can type responses when the program prompts you.

1. Clear any default code from the editor so you're starting with a clean file.

## Set up your starter code

Before writing any logic, you'll paste a set of guiding comments into the editor. These comments act as an outline for your program — each one marks where a specific piece of code belongs.

1. Copy the following comments and paste them into the editor pane:

    ```csharp
    // Collect the bill amount and tip percentage

    // Display the entered values

    // Calculate the tip and total

    // Display the results
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code.

1. Leave the code as-is for now. In the steps that follow, you'll add code beneath each comment.

## Store bill details as variables

You'll start by storing the bill amount and tip percentage as hardcoded variables.

1. Beneath the `// Collect the bill amount and tip percentage` comment, add the following lines:

    ```csharp
    decimal billAmount = 45.50m;
    decimal tipPercentage = 18.0m;
    ```

    Each variable is a `decimal` — a data type suited for precise values like money. The `m` after each number is a suffix that tells C# to treat the literal as a `decimal` instead of a `double`.

1. Beneath the `// Display the entered values` comment, add the following lines:

    ```csharp
    Console.WriteLine("Bill details:");
    Console.WriteLine($"  Bill amount:    ${billAmount}");
    Console.WriteLine($"  Tip percentage: {tipPercentage}%");
    ```

1. Select the ▶️ **Run** button to run the program. You should see:

    ```output
    Bill details:
      Bill amount:    $45.50
      Tip percentage: 18.0%
    ```

1. Select the **Clear console** button before you continue.

## Calculate the tip and total

Now you'll use arithmetic to calculate the tip amount and the total bill, using the formula:

$$tip = billAmount \times \frac{tipPercentage}{100}$$

1. Beneath the `// Calculate the tip and total` comment, add the following lines of code:

    ```csharp
    decimal tipAmount = billAmount * (tipPercentage / 100);
    decimal totalAmount = billAmount + tipAmount;
    ```

1. Beneath the `// Display the results` comment, add the following lines of code:

    ```csharp
    Console.WriteLine($"\nTip amount:   ${tipAmount}");
    Console.WriteLine($"Total amount: ${totalAmount}");
    ```

    > **Note**: `\n` inside an interpolated string adds a blank line before the text, which helps separate sections of output.

1. Select ▶️ **Run**. Your complete output should now look like this:

    ```output
    Bill details:
      Bill amount:    $45.50
      Tip percentage: 18.0%

    Tip amount:   $8.190
    Total amount: $53.690
    ```

1. Select **Clear console** before you continue.

## Accept bill details from user input

Hardcoded values are useful for testing, but a real program should accept input from the user. `Console.ReadLine()` always returns a `string`, so you need to convert it to a `decimal` before you can use it in calculations.

1. Replace the two hardcoded variables beneath the `// Collect the bill amount and tip percentage` comment with the following code:

    ```csharp
    Console.WriteLine("Enter your bill details:\n");
    Console.Write("Bill amount:    ");
    decimal billAmount = Convert.ToDecimal(Console.ReadLine());
    Console.Write("Tip percentage: ");
    decimal tipPercentage = Convert.ToDecimal(Console.ReadLine());
    ```

    Wrapping `Console.ReadLine()` inside `Convert.ToDecimal()` converts the text the user types into a decimal number in a single step.

1. Keep the rest of your code exactly as it is. Your complete program should now look like this:

    ```csharp
    // Collect the bill amount and tip percentage
    Console.WriteLine("Enter your bill details:\n");
    Console.Write("Bill amount:    ");
    decimal billAmount = Convert.ToDecimal(Console.ReadLine());
    Console.Write("Tip percentage: ");
    decimal tipPercentage = Convert.ToDecimal(Console.ReadLine());

    // Display the entered values
    Console.WriteLine("\nBill details:");
    Console.WriteLine($"  Bill amount:    ${billAmount}");
    Console.WriteLine($"  Tip percentage: {tipPercentage}%");

    // Calculate the tip and total
    decimal tipAmount = billAmount * (tipPercentage / 100);
    decimal totalAmount = billAmount + tipAmount;

    // Display the results
    Console.WriteLine($"\nTip amount:   ${tipAmount}");
    Console.WriteLine($"Total amount: ${totalAmount}");
    ```

1. Select ▶️ **Run**. When each prompt appears in the output console, click on it, type a value, and press **Enter**.

1. Try entering the same values as before to verify your output matches the following:

    ```output
    Enter your bill details:

    Bill amount:    45.50
    Tip percentage: 18

    Bill details:
      Bill amount:    $45.50
      Tip percentage: 18%

    Tip amount:   $8.190
    Total amount: $53.690
    ```

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try each prompt below, read the response carefully, and test the code examples it gives you in the online editor.

### Discovery 1: Formatting currency automatically

**AI Prompt:**
> "In C#, how can I display a decimal value as currency, with a dollar sign and exactly two decimal places? Can you show me beginner friendly examples?"

**After the AI responds:** Take a look at the examples the AI gives you. Do you see a way to clean up the `$53.690` in your output so it displays as `$53.69`? Try it out in your program and see if it works as expected.

<details>
<summary>Show answer</summary>
You can use the `C` format specifier inside an interpolated string to format a number as currency. For example:

```csharp
decimal totalAmount = 53.690m;
Console.WriteLine($"Total amount: {totalAmount:C}"); // Output: Total amount: $53.69
```
</details>

### Discovery 2: Rounding decimal values

**AI Prompt:**
> "In C#, how can I round a decimal value to two decimal places without using currency formatting? Can you show me beginner friendly examples?"

**After the AI responds:** Take a look at the examples the AI gives you. Can you find a way to round your tip amount before displaying it? Try it out in your program and see if it works as expected.

<details>
<summary>Show answer</summary>
You can use the `Math.Round()` method to round a number to a specific number of decimal places. For example:

```csharp
decimal tipAmount = 8.190m;
decimal roundedTip = Math.Round(tipAmount, 2);
Console.WriteLine($"Tip amount: ${roundedTip}"); // Output: Tip amount: $8.19
```
</details>

### Discovery 3: Comparing two numbers

**AI Prompt:**
> "In C#, what are some common methods I can use to compare numbers and find the larger or smaller of two values? Can you show me beginner friendly examples?"

**After the AI responds:** Take a look at the examples the AI gives you. Can you find a way to compare this bill's total to a previous total and display the larger one? Try it out in your program and see if it works as expected.

<details>
<summary>Show answer</summary>
You can use the `Math.Max()` method to find the larger of two numbers and `Math.Min()` to find the smaller:

```csharp
decimal totalAmount = 53.69m;
decimal previousTotal = 40.00m;

decimal higherTotal = Math.Max(totalAmount, previousTotal);
decimal lowerTotal = Math.Min(totalAmount, previousTotal);
```
</details>

