---
lab:
    title: 'Challenge: Display a subscription renewal message'
    description: 'Write a C# program that uses if, else if, and else to display a subscription renewal message and discount based on a randomly generated number of days until expiration.'
    level: 100
    duration: 20
    islab: true
    status: 'released'
---

# Challenge: Display a subscription renewal message

You've learned how to generate random numbers and control your program's flow with `if`, `else if`, and `else`. In this exercise, you put it all together by writing a program that displays a subscription renewal message based on a randomly generated number of days until expiration.

This exercise takes approximately **20** minutes.

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
    // Generate a random number of days until expiration

    // Display an expiration message based on the days remaining

    // Display a discount message if a discount applies
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code.

## Generate a random number of days until expiration

1. Beneath the `// Generate a random number of days until expiration` comment, add the following lines:

    ```csharp
    Random random = new Random();
    int daysUntilExpiration = random.Next(12);
    int discountPercentage = 0;
    ```

    `random.Next(12)` returns a random whole number from `0` up to, but not including, `12` — so `daysUntilExpiration` will be a number from `0` to `11`. `discountPercentage` starts at `0` and you'll update it later, depending on how urgent the renewal is.

## Display an expiration message based on the days remaining

Now you'll add an `if`, `else if`, `else` chain that checks `daysUntilExpiration` and displays a message. C# checks each condition from top to bottom and only runs the first one that matches, so you need to order your conditions from the **most urgent** to the **least urgent**.

1. Beneath the `// Display an expiration message based on the days remaining` comment, add code that checks the following rules, in this order:

    1. If `daysUntilExpiration` is `0`, display: `Your subscription has expired.`
    2. If `daysUntilExpiration` is `1`, display: `Your subscription expires within a day!` and set `discountPercentage` to `20`
    3. If `daysUntilExpiration` is `5` or less, display: `Your subscription expires in {daysUntilExpiration} days.` and set `discountPercentage` to `10`
    4. If `daysUntilExpiration` is `10` or less, display: `Your subscription will expire soon. Renew now!`
    5. Otherwise, don't display anything

    > **Tip**: Use one `if` for the first rule, `else if` for the next three rules, and a final `else` for the last rule. Since `daysUntilExpiration` is random, a value like `3` should match rule 3 (`5` or less) — but only because rules 1 and 2 didn't match first.

1. Select ▶️ **Run** several times. Since `daysUntilExpiration` is random, you'll need multiple runs to see each message. Confirm that:
    - A value of `0` shows the expired message
    - A value of `1` shows the "within a day" message
    - Values from `2` to `5` show the "expires in X days" message
    - Values from `6` to `10` show the "will expire soon" message
    - A value of `11` shows nothing

1. Select the **Clear console** button before you continue.

## Display a discount message if a discount applies

Finally, you'll display a discount message — but only when a discount was actually set in the previous section.

1. Beneath the `// Display a discount message if a discount applies` comment, add a **separate** `if` statement (not `else if`) that checks whether `discountPercentage` is greater than `0`, and if so, displays: `Renew now and save {discountPercentage}%.`

    > **Tip**: This needs to be its own `if` statement, outside the chain you wrote above. That's because the discount message depends on the value of `discountPercentage`, not directly on `daysUntilExpiration`.

1. Select ▶️ **Run** several times until you see a run where `daysUntilExpiration` is `1` or between `2` and `5`, and confirm the discount message appears beneath the expiration message.

## Verify your solution

Compare your program to the example below. Your code doesn't need to match exactly — there are many ways to write a program that works correctly — but the behavior should be the same.

```csharp
// Generate a random number of days until expiration
Random random = new Random();
int daysUntilExpiration = random.Next(12);
int discountPercentage = 0;

// Display an expiration message based on the days remaining
if (daysUntilExpiration == 0)
{
    Console.WriteLine("Your subscription has expired.");
}
else if (daysUntilExpiration == 1)
{
    Console.WriteLine("Your subscription expires within a day!");
    discountPercentage = 20;
}
else if (daysUntilExpiration <= 5)
{
    Console.WriteLine($"Your subscription expires in {daysUntilExpiration} days.");
    discountPercentage = 10;
}
else if (daysUntilExpiration <= 10)
{
    Console.WriteLine("Your subscription will expire soon. Renew now!");
}

// Display a discount message if a discount applies
if (discountPercentage > 0)
{
    Console.WriteLine($"Renew now and save {discountPercentage}%.");
}
```

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try each prompt below, read the response carefully, and test the code examples it gives you in the online editor.

### Discovery 1: Using a switch statement instead

**AI Prompt:**
> "In C#, is there another way to write a long chain of if/else if statements? Can you show me a beginner friendly example using a switch statement?"

**After the AI responds:** Take a look at the examples the AI gives you. Do you see how a `switch` statement might replace part of your `if`/`else if` chain? You don't need to change your program — just compare the two approaches.

<details>
<summary>Show answer</summary>
A `switch` statement can check one value against several possible matches, which can be easier to read than a long `if`/`else if` chain when you're checking exact values:

```csharp
switch (daysUntilExpiration)
{
    case 0:
        Console.WriteLine("Your subscription has expired.");
        break;
    case 1:
        Console.WriteLine("Your subscription expires within a day!");
        discountPercentage = 20;
        break;
    default:
        Console.WriteLine("Check back later.");
        break;
}
```
</details>

### Discovery 2: Combining conditions with logical operators

**AI Prompt:**
> "In C#, how can I combine multiple comparisons into a single if condition using logical operators? Can you show me beginner friendly examples?"

**After the AI responds:** Take a look at the examples the AI gives you. Can you rewrite the "5 days or less" rule so it explicitly checks both the lower and upper bounds (for example, more than 1 day, but 5 or fewer)? Try it out in your program and see if it still behaves the same way.

<details>
<summary>Show answer</summary>
You can use the logical AND operator (`&&`) to require that two conditions are both true:

```csharp
if (daysUntilExpiration > 1 && daysUntilExpiration <= 5)
{
    Console.WriteLine($"Your subscription expires in {daysUntilExpiration} days.");
    discountPercentage = 10;
}
```
</details>

### Bonus challenge

Once your basic version works, try adding a new rule that offers an extra discount (like `30`%) when a subscription has already expired, to encourage the user to renew anyway.

