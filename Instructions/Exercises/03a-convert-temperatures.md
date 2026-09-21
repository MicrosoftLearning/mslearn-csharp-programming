---
lab:
    title: 'Challenge: Convert Fahrenheit to Celsius'
    description: 'Write a C# program that stores a Fahrenheit temperature, converts it to Celsius using decimal arithmetic, and displays a formatted result.'
    level: 100
    duration: 15
    islab: true
    status: 'released'
---

# Challenge: Convert Fahrenheit to Celsius

You've learned how to store values in variables, perform arithmetic, and convert user input into numbers. In this exercise, you put it all together by writing a program that converts a Fahrenheit temperature to Celsius.

This exercise takes approximately **15** minutes.

## Open the online C# IDE

You'll write and run your code using an online C# editor — no installation required.

1. Open a browser and navigate to the C# editor at [https://microsoftlearning.github.io/c-sharp-minor](https://microsoftlearning.github.io/c-sharp-minor).

2. You'll see two panels:
    - **Code Editor pane** (top): where you write your C# code.
    - **Output Console** (bottom): where output is displayed and where you can type input when the program asks for it.

3. The editor may contain some default code. Select all of it and delete it so you're starting with a clean, empty file.

## Set up your program

Before writing any logic, you'll paste a set of guiding comments into the editor. These comments act as an outline for your program — each one marks where a specific piece of code belongs.

1. Copy the following comments and paste them into the editor pane:

    ```csharp
    // Store a Fahrenheit temperature

    // Convert it to Celsius

    // Display the result
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code.

## Store a Fahrenheit temperature

1. Beneath the `// Store a Fahrenheit temperature` comment, declare a variable that stores a Fahrenheit temperature, such as `94`.

    > **Tip**: Think about which data type to use. The conversion formula in the next section involves division, and you'll want to keep the decimal part of the result. Look back at how you declared money values in the [Build a tip calculator](5-exercise-calculator.md) exercise for a type that works well here.

## Convert it to Celsius

1. Beneath the `// Convert it to Celsius` comment, add code that converts the Fahrenheit value to Celsius using the formula:

    $$C = (F - 32) \times \frac{5}{9}$$

    Store the result in a new variable.

    > **Tip**: If you use `int` for the formula, C# performs **integer division**, which drops any decimal places and gives you the wrong answer. Using `decimal` for every value in the formula keeps the fractional part.

## Display the result

1. Beneath the `// Display the result` comment, add a `Console.WriteLine()` statement that uses string interpolation to display both the original Fahrenheit value and the converted Celsius value.

1. Select the ▶️ **Run** button to run your program. For a Fahrenheit value of `94`, your output should look similar to:

    ```output
    94°F is 34.44444444444444444444444444°C
    ```

    > **Note**: That's a lot of decimal places! You'll clean this up in the Code with AI section below.

1. Select the **Clear console** button before you continue.

## Verify your solution

Compare your program to the example below. Your code doesn't need to match exactly — there are many ways to write a program that works correctly — but the behavior should be the same.

```csharp
// Store a Fahrenheit temperature
decimal fahrenheit = 94;

// Convert it to Celsius
decimal celsius = (fahrenheit - 32) * 5 / 9;

// Display the result
Console.WriteLine($"{fahrenheit}°F is {celsius}°C");
```

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try each prompt below, read the response carefully, and test the code examples it gives you in the online editor.

### Discovery 1: Rounding the result

**AI Prompt:**
> "In C#, how can I display a decimal value rounded to one decimal place, like 34.4 instead of 34.44444444444444444444444444? Can you show me beginner friendly examples?"

**After the AI responds:** Try using the technique it suggests to clean up your Celsius output so it only shows one decimal place.

<details>
<summary>Show answer</summary>
You can use the `F1` format specifier inside an interpolated string to round a number to one decimal place:

```csharp
decimal celsius = 34.44444444444444444444444444m;
Console.WriteLine($"{celsius:F1}°C"); // Output: 34.4°C
```
</details>

### Discovery 2: Accepting the temperature as user input

**AI Prompt:**
> "In C#, how can I ask the user to type a temperature and convert their answer into a decimal I can use in a calculation? Can you show me beginner friendly examples?"

**After the AI responds:** Try updating your program so the user enters the Fahrenheit temperature instead of it being hardcoded.

<details>
<summary>Show answer</summary>
You can use `Console.ReadLine()` to read the user's input, then convert it with `Convert.ToDecimal()`:

```csharp
Console.Write("Enter a Fahrenheit temperature: ");
decimal fahrenheit = Convert.ToDecimal(Console.ReadLine());
```
</details>

### Bonus challenge

Once your basic version works, try supporting the other direction: convert a Celsius temperature to Fahrenheit using the formula **F = (C × 9 / 5) + 32**.

