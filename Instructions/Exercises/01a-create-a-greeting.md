---
lab:
    title: 'Create a personalized greeting'
    description: 'Write a C# program that uses Console.WriteLine(), Console.ReadLine(), and string interpolation to display a personalized greeting message.'
    level: 100
    duration: 15
    islab: true
    status: 'released'
---

# Create a personalized greeting

In this exercise, you write a C# program that asks for the user's name and displays a personalized greeting. You practice using the `Console.WriteLine()` method to display output, the `Console.ReadLine()` method to collect user input, and string interpolation to format a custom message.

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
    // Display a welcome message

    // Ask for the user's name

    // Display a personalized greeting
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code.

## Display a welcome message

The first thing your program should do is greet the user when it starts. You'll use the `Console.WriteLine()` method to display a message on the screen.

1. In the editor pane, add the following line beneath the `// Display a welcome message` comment:

    ```csharp
    Console.WriteLine("Welcome to the greeting program!");
    ```

1. Select the ▶️ **Run** button to run the code.

1. Check the output console. You should see:

    ```output
    Welcome to the greeting program!
    ```

    > **Note**: If nothing appears, make sure the code is typed exactly as shown, including the quotes, parentheses, and semicolon.

1. Select the **Clear console** button to clear the output before you continue.

## Ask for the user's name

Now you'll add code that pauses the program and asks for the user's name. You'll use `Console.Write()` to display a prompt without moving to a new line, and `Console.ReadLine()` to wait for the user to type a response.

1. Beneath the `// Ask for the user's name` comment, add the following lines:

    ```csharp
    Console.Write("What is your name? ");
    string name = Console.ReadLine();
    ```

    The first line displays the prompt `What is your name? ` in the console. The second line waits for the user to type a response and stores whatever they type into a variable called `name`.

1. Run the program again by selecting ▶️ **Run**.

1. When `What is your name? ` appears in the output console, click on the console and type your name, then press **Enter**.

1. The program finishes after you enter your name — but it doesn't say anything yet. You'll fix that in the next step.

1. Select **Clear console** before you continue.

## Display a personalized greeting

Now you'll use the `name` variable to build a personalized message. You'll do this with **string interpolation** — a technique that lets you embed variable values directly inside a string by prefixing the string with `$` and wrapping variable names in curly braces `{}`.

1. Beneath the `// Display a personalized greeting` comment, add the following line:

    ```csharp
    Console.WriteLine($"Hello, {name}! It's great to meet you.");
    ```

1. Run the program, enter your name when prompted, and press **Enter**.

1. You should see output similar to:

    ```output
    Welcome to the greeting program!
    What is your name? Alex
    Hello, Alex! It's great to meet you.
    ```

1. Your complete program should now look like this:

    ```csharp
    // Display a welcome message
    Console.WriteLine("Welcome to the greeting program!");

    // Ask for the user's name
    Console.Write("What is your name? ");
    string name = Console.ReadLine();

    // Display a personalized greeting
    Console.WriteLine($"Hello, {name}! It's great to meet you.");
    ```

1. Run the program one more time and confirm the output matches what you entered. For example:

    ```output
    Welcome to the greeting program!
    What is your name? Alex
    Hello, Alex! It's great to meet you.
    ```

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try the prompt below, read the response carefully, and test the code examples it gives you in the online editor.

### Discovery: Transforming text

**AI Prompt:**
```In C#, how can I change a string input to all uppercase or all lowercase? Can you show me examples?```

**After the AI responds:** Look closely at the code examples it provides. Try modifying your greeting program to display the user's name in uppercase or lowercase.

<details>
<summary>Show answer</summary>
You can use the following string methods to transform text:

```csharp
string name = Console.ReadLine();

// Converts to all uppercase
string uppercaseName = name.ToUpper();

// Converts to all lowercase
string lowercaseName = name.ToLower();
```
</details>
