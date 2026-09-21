---
lab:
    title: 'Build a dice game'
    description: 'Write a C# program that simulates rolling dice, uses if, else if, and else to award a prize, and uses logical operators to detect doubles and triples.'
    level: 100
    duration: 20
    islab: true
    status: 'released'
---

# Build a dice game

In this exercise, you write a C# program that simulates rolling three dice and awards a prize based on the result. You practice generating random numbers, comparing values with logical operators, and controlling your program's flow with `if`, `else if`, and `else`.

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
    // Roll the dice

    // Display the roll and total

    // Award a bonus for doubles or triples

    // Display the final result
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code.

1. Leave the code as-is for now. In the steps that follow, you'll add code beneath each comment.

## Roll the dice and calculate a total

You'll use the `Random` class to simulate rolling three six-sided dice, then add the results together.

1. Beneath the `// Roll the dice` comment, add the following lines:

    ```csharp
    Random dice = new Random();

    int roll1 = dice.Next(1, 7);
    int roll2 = dice.Next(1, 7);
    int roll3 = dice.Next(1, 7);
    int total = roll1 + roll2 + roll3;
    ```

    `new Random()` creates a random number generator. Calling `dice.Next(1, 7)` returns a random whole number from `1` up to, but not including, `7` — in other words, a number from `1` to `6`, just like a six-sided die.

1. Beneath the `// Display the roll and total` comment, add the following line:

    ```csharp
    Console.WriteLine($"Dice roll: {roll1} + {roll2} + {roll3} = {total}");
    ```

1. Select the ▶️ **Run** button a few times. You should see output similar to:

    ```output
    Dice roll: 4 + 6 + 2 = 12
    ```

    Notice that the values change each time you run the program, since the dice rolls are random.

1. Select the **Clear console** button before you continue.

## Award a bonus for doubles or triples

Now you'll check whether any of the dice match, and award a bonus to the total. You'll use the logical OR operator (`||`) to check if any two dice match, and the logical AND operator (`&&`) to check if all three match.

1. Beneath the `// Award a bonus for doubles or triples` comment, add the following code:

    ```csharp
    if ((roll1 == roll2) || (roll2 == roll3) || (roll1 == roll3))
    {
        if ((roll1 == roll2) && (roll2 == roll3))
        {
            Console.WriteLine("You rolled triples! +6 bonus to total!");
            total += 6;
        }
        else
        {
            Console.WriteLine("You rolled doubles! +2 bonus to total!");
            total += 2;
        }
    }
    ```

    The outer `if` checks whether **any** two dice match, using `||` so the condition is true if at least one pair is equal. The inner `if` then checks whether **all three** dice match, using `&&` so the condition is only true when every comparison is true. Nesting the `if` statements this way ensures a player only gets one bonus, even when they roll triples.

1. Select ▶️ **Run** a few times until you roll doubles or triples, and confirm the bonus message and updated total appear. For example:

    ```output
    Dice roll: 5 + 5 + 3 = 13
    You rolled doubles! +2 bonus to total!
    ```

1. Select **Clear console** before you continue.

## Display the final result

Finally, you'll use an `if`, `else if`, `else` ladder to award a prize based on the final total.

1. Beneath the `// Display the final result` comment, add the following code:

    ```csharp
    if (total >= 16)
    {
        Console.WriteLine("You win a new car!");
    }
    else if (total >= 10)
    {
        Console.WriteLine("You win a new laptop!");
    }
    else if (total == 7)
    {
        Console.WriteLine("You win a trip for two!");
    }
    else
    {
        Console.WriteLine("You win a kitten!");
    }
    ```

    C# checks each condition from top to bottom and runs the code beneath the first one that's `true`. If none of the `if` or `else if` conditions match, the final `else` block runs.

1. Select ▶️ **Run** several times to see different prizes, including outcomes with doubles and triples.

## Verify your solution

Your complete program should now look like this:

```csharp
// Roll the dice
Random dice = new Random();

int roll1 = dice.Next(1, 7);
int roll2 = dice.Next(1, 7);
int roll3 = dice.Next(1, 7);
int total = roll1 + roll2 + roll3;

// Display the roll and total
Console.WriteLine($"Dice roll: {roll1} + {roll2} + {roll3} = {total}");

// Award a bonus for doubles or triples
if ((roll1 == roll2) || (roll2 == roll3) || (roll1 == roll3))
{
    if ((roll1 == roll2) && (roll2 == roll3))
    {
        Console.WriteLine("You rolled triples! +6 bonus to total!");
        total += 6;
    }
    else
    {
        Console.WriteLine("You rolled doubles! +2 bonus to total!");
        total += 2;
    }
}

// Display the final result
if (total >= 16)
{
    Console.WriteLine("You win a new car!");
}
else if (total >= 10)
{
    Console.WriteLine("You win a new laptop!");
}
else if (total == 7)
{
    Console.WriteLine("You win a trip for two!");
}
else
{
    Console.WriteLine("You win a kitten!");
}
```

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try each prompt below, read the response carefully, and test the code examples it gives you in the online editor.

### Discovery 1: Rolling a different kind of die

**AI Prompt:**
> "In C#, how does the Random.Next() method decide which numbers it can return? Can you show me how to simulate rolling a 20-sided die?"

**After the AI responds:** Take a look at the examples the AI gives you. Try changing your program to simulate a different kind of die, like a 20-sided die, and see how it affects your output.

<details>
<summary>Show answer</summary>
`Random.Next(minValue, maxValue)` returns a random number starting at `minValue` and going up to, but not including, `maxValue`. To simulate a 20-sided die, you'd use `21` as the upper bound so `20` can still be returned:

```csharp
Random dice = new Random();
int roll = dice.Next(1, 21);
Console.WriteLine($"You rolled a {roll} on a 20-sided die!");
```
</details>

### Discovery 2: Letting the player choose how many rounds to play

**AI Prompt:**
> "In C#, how can I ask the player how many rounds they want to play and keep count of how many times a condition is true across those rounds? Can you show me beginner friendly examples?"

**After the AI responds:** Take a look at the examples the AI gives you. Can you find a way to track how many times the player rolled doubles or triples across several rounds? Try it out in your program and see if it works as expected.

<details>
<summary>Show answer</summary>
You can use a variable as a counter, and increase it with the compound assignment operator (`+=`) whenever a condition is true:

```csharp
Console.Write("How many rounds do you want to play? ");
int rounds = Convert.ToInt32(Console.ReadLine());

int bonusCount = 0;
// bonusCount += 1; would go inside your doubles/triples check, once per round
Console.WriteLine($"You rolled a bonus {bonusCount} time(s).");
```
</details>

