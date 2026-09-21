---
lab:
    title: 'Challenge: Interact with the user'
    description: 'Write a C# program that combines Console.Write(), Console.ReadLine(), and string interpolation to collect multiple pieces of information from the user and display a personalized message.'
    level: 100
    duration: 15
    islab: true
    status: 'released'
---

# Challenge: Interact with the user

You've learned the basics of C# console output, user input, and string manipulation. In this exercise, you put it all together by writing a program that asks the user two questions and combines their answers into a single personalized message.

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
    // Ask for the user's name

    // Ask for the user's age

    // Display a personalized message that includes both pieces of information
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code.

## Ask for the user's name

1. Beneath the `// Ask for the user's name` comment, add code that:
    - Uses `Console.Write()` to display the prompt `What is your name? ` (remember the space before the closing quote, so the user's answer doesn't run into the prompt)
    - Uses `Console.ReadLine()` to read the user's response into a variable named `name`

    > **Tip**: If you get stuck, look back at how you asked for the user's name in the [Create a personalized greeting](01-exercise-greeting.md) exercise.

1. Select the ▶️ **Run** button to run the code so far, and type your name when prompted.

1. Select the **Clear console** button to clear the output before you continue.

## Ask for the user's age

1. Beneath the `// Ask for the user's age` comment, add code that:
    - Uses `Console.Write()` to display the prompt `How old are you? `
    - Uses `Console.ReadLine()` to read the user's response into a variable named `age`

    > **Note**: `Console.ReadLine()` always returns a `string`, even if the user types a number. That's fine for this exercise — you can use the `age` variable directly inside a string interpolation without converting it to a number first.

1. Run the program again, and answer both prompts when asked.

1. Select **Clear console** before you continue.

## Display a personalized message

1. Beneath the `// Display a personalized message that includes both pieces of information` comment, add a `Console.WriteLine()` statement that uses string interpolation (`$"..."`) to combine the `name` and `age` variables into a single message.

1. Run your program and check that the output looks similar to this, using the name and age you entered:

    ```output
    What is your name? Sam
    How old are you? 25
    Hello, Sam! You are 25 years old.
    ```

    > **Note**: If you get an error, check that you have double quotes around each piece of text, a semicolon at the end of each statement, and that `Console`, `Write`, `WriteLine`, and `ReadLine` are capitalized correctly.

1. Select **Clear console** before you continue.

## Verify your solution

Compare your program to the example below. Your code doesn't need to match exactly — there are many ways to write a program that works correctly — but the behavior should be the same.

```csharp
// Ask for the user's name
Console.Write("What is your name? ");
string name = Console.ReadLine();

// Ask for the user's age
Console.Write("How old are you? ");
string age = Console.ReadLine();

// Display a personalized message that includes both pieces of information
Console.WriteLine($"Hello, {name}! You are {age} years old.");
```

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try each prompt below, read the response carefully, and test the code examples it gives you in the online editor.

### Discovery 1: Printing a decorative banner

**AI Prompt:**
```In C#, how can I print a line of 20 dashes in a row without typing them all out? Can you show me an example?```

**After the AI responds:** Try using the technique it suggests to print a banner line above and below your program's final greeting.

<details>
<summary>Show answer</summary>
You can use the `new string(char, count)` constructor to repeat a character multiple times. For example, to print 20 dashes in a row:

```csharp
Console.WriteLine(new string('-', 20));
Console.WriteLine($"Hello, {name}! You are {age} years old.");
Console.WriteLine(new string('-', 20));
```
</details>

### Discovery 2: Formatting a multi-line message

**AI Prompt:**
```In C#, how can I display a message that spans multiple lines using a single Console.WriteLine() statement? Can you show me examples?```

**After the AI responds:** Try modifying your program's final message so the name and age each appear on their own line.

<details>
<summary>Show answer</summary>
You can use the newline escape character `\n` inside a regular string, or a verbatim/raw string that spans multiple lines. For example:

```csharp
Console.WriteLine($"Name: {name}\nAge: {age}");
```
</details>