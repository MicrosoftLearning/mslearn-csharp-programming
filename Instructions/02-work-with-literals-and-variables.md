---
lab:
    title: 'Work with literals and variables'
    description: 'Write a C# program that declares variables using explicit types and the var keyword, assigns literal values to them, and displays the values.'
    level: 100
    duration: 15
    islab: true
    status: 'released'
---

# Work with literals and variables

In this exercise, you write a C# program that declares variables to store different kinds of literal values, then displays those values. You practice declaring variables with an explicit type, declaring variables with the `var` keyword, and reassigning a variable to a new value.

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
    // Declare variables using an explicit type

    // Declare a variable using var

    // Display the values of your variables

    // Reassign a variable to a new value
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code.

## Declare variables using an explicit type

A variable is a named storage location that holds a value, called a **literal**, such as a piece of text or a number. When you declare a variable, you specify its type before its name so C# knows what kind of value it can hold.

1. Beneath the `// Declare variables using an explicit type` comment, add the following lines:

    ```csharp
    string favoriteFood = "pizza";
    int slicesEaten = 3;
    bool isHungry = false;
    ```

    Each line declares a variable with an explicit type (`string`, `int`, or `bool`), then uses the `=` operator to assign it a literal value.

1. Select the ▶️ **Run** button to run the code.

1. Nothing appears in the output console yet. That's expected — you've only stored values in variables so far. You'll display them in the next section.

## Declare a variable using var

Instead of writing out a type, you can let C# figure out the type for you by using the `var` keyword. C# looks at the literal value you assign and picks the matching type automatically.

1. Beneath the `// Declare a variable using var` comment, add the following line:

    ```csharp
    var favoriteColor = "blue";
    ```

    Because `"blue"` is a string literal, C# infers that `favoriteColor` is a `string`, just as if you had written `string favoriteColor = "blue";`.

1. Select ▶️ **Run**. The output console still won't show anything new — you'll fix that next.

## Display the values of your variables

Now you'll use `Console.WriteLine()` and string interpolation to display each variable's value in the output console.

1. Beneath the `// Display the values of your variables` comment, add the following lines:

    ```csharp
    Console.WriteLine($"Favorite food: {favoriteFood}");
    Console.WriteLine($"Slices eaten: {slicesEaten}");
    Console.WriteLine($"Is hungry: {isHungry}");
    Console.WriteLine($"Favorite color: {favoriteColor}");
    ```

1. Select ▶️ **Run**. You should see:

    ```output
    Favorite food: pizza
    Slices eaten: 3
    Is hungry: False
    Favorite color: blue
    ```

1. Select the **Clear console** button before you continue.

## Reassign a variable to a new value

A variable's value isn't permanent — you can assign it a new value at any time after it's declared. You only need to specify the type (or `var`) once, when you first declare the variable.

1. Beneath the `// Reassign a variable to a new value` comment, add the following lines:

    ```csharp
    Console.WriteLine($"Slices eaten before dessert: {slicesEaten}");
    slicesEaten = 5;
    Console.WriteLine($"Slices eaten after dessert: {slicesEaten}");
    ```

    Notice that the second line reassigns `slicesEaten` using just its name — no type keyword is repeated.

1. Select ▶️ **Run**. You should see:

    ```output
    Favorite food: pizza
    Slices eaten: 3
    Is hungry: False
    Favorite color: blue
    Slices eaten before dessert: 3
    Slices eaten after dessert: 5
    ```

## Verify your solution

Your complete program should now look like this:

```csharp
// Declare variables using an explicit type
string favoriteFood = "pizza";
int slicesEaten = 3;
bool isHungry = false;

// Declare a variable using var
var favoriteColor = "blue";

// Display the values of your variables
Console.WriteLine($"Favorite food: {favoriteFood}");
Console.WriteLine($"Slices eaten: {slicesEaten}");
Console.WriteLine($"Is hungry: {isHungry}");
Console.WriteLine($"Favorite color: {favoriteColor}");

// Reassign a variable to a new value
Console.WriteLine($"Slices eaten before dessert: {slicesEaten}");
slicesEaten = 5;
Console.WriteLine($"Slices eaten after dessert: {slicesEaten}");
```

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try the prompt below, read the response carefully, and test the code examples it gives you in the online editor.

### Discovery: Naming variables

**AI Prompt:**
```In C#, what are the naming rules and conventions for variables? Can you show me some valid and invalid examples?```

**After the AI responds:** Try renaming a few of your variables to follow the conventions the AI describes, then run your program again to confirm it still works.

<details>
<summary>Show answer</summary>
C# variable names must start with a letter or underscore, can't contain spaces, and can't be a reserved keyword. By convention, variable names use `camelCase` — the first word is lowercase and each following word starts with a capital letter. For example:

```csharp
// Valid, follows convention
string favoriteFood = "pizza";

// Valid, but doesn't follow convention
string FavoriteFood = "pizza";

// Invalid, starts with a number
// string 1favoriteFood = "pizza";
```
</details>

