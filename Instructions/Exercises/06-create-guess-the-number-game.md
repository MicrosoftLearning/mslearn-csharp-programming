---
lab:
    title: 'Create a Guess the Number game'
    description: 'Write a C# program that uses a while loop, conditional logic, and break to run an interactive Guess the Number game.'
    level: 100
    duration: 25
    islab: true
    status: 'released'
---

# Create a Guess the Number game

In this exercise, you build a classic Guess the Number game. The computer picks a secret number, and the player keeps guessing until they get it right. You practice using a `while` loop to repeat actions, `if`, `else if`, and `else` to compare values, and `break` to exit the loop when the player wins.

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

1. In the VS Code file explorer, navigate to the `Labfiles/06-create-guess-the-number-game` subfolder.

1. Select the `Program.cs` file. You'll see a set of guiding comments that act as an outline for your program — each one marks where a specific piece of code belongs:

    ```csharp
    // Set up the game

    // Ask the player to guess

        // Check the guess and give feedback

    // Announce the result
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code. In the steps that follow, you'll add code beneath each comment.

1. If VS Code shows a prompt about restoring project dependencies, select **Restore**.

## Pick a secret number

Every guessing game needs a target. You'll use the `Random` class to pick a random whole number between 1 and 20.

1. Beneath the `// Set up the game` comment, add the following lines:

    ```csharp
    Random random = new Random();
    int secretNumber = random.Next(1, 21);
    int maxGuesses = 5;
    int guessCount = 0;
    bool hasWon = false;

    Console.WriteLine("I'm thinking of a number between 1 and 20.");
    Console.WriteLine($"You have {maxGuesses} guesses. Good luck!");
    ```

    - `random.Next(1, 21)` returns a random whole number from `1` up to, but not including, `21` — so the secret number will be from `1` to `20`.
    - `maxGuesses` and `guessCount` will control how the loop runs, and `hasWon` will keep track of whether the player guessed correctly.

1. Save the file, then run your program. Open a new terminal (**Terminal > New Terminal**), navigate to the project folder, and run the program:

    ```bash
    cd Labfiles/06-create-guess-the-number-game
    dotnet run
    ```

    You should see something like:

    ```output
    I'm thinking of a number between 1 and 20.
    You have 5 guesses. Good luck!
    ```

    > **Tip**: If you have the C# Dev Kit extension installed, you can also select the **Run** button that appears above your code instead of using the terminal. You only need to `cd` into the project folder once per terminal session — after that, `dotnet run` alone will work for the rest of this exercise.

## Ask the player to guess

Next, you'll add a `while` loop that keeps prompting the player until they either run out of guesses or get the answer right. `Console.ReadLine()` always returns a `string`, so you'll convert it to an `int` before comparing it to the secret number.

1. Beneath the `// Ask the player to guess` comment, add the following lines:

    ```csharp
    while (guessCount < maxGuesses)
    {
        guessCount++;
        Console.Write($"\nGuess #{guessCount}: ");
        int guess = Convert.ToInt32(Console.ReadLine());
    ```

    - `while (guessCount < maxGuesses)` keeps the loop running until the player has used all their guesses.
    - `guessCount++` is shorthand for `guessCount = guessCount + 1`. It increases the count each time through the loop — this is what eventually causes the condition to become `false`.
    - `Convert.ToInt32(Console.ReadLine())` reads the player's input and converts it to a whole number in one step.

    > **Note**: Notice the opening `{` isn't closed yet. You'll add the closing `}` in the next section, once the rest of the loop's code is in place.

## Check the guess and give feedback

Now the loop needs to compare the guess to the secret number and tell the player whether they were too high, too low, or exactly right. When they guess right, you'll set `hasWon` to `true` and use `break` to exit the loop early.

Be sure to maintain the correct indentation levels as you add code inside the `while` loop.

1. Beneath the `// Check the guess and give feedback` comment, add the following lines, then close the `while` loop with a final `}`:

    ```csharp
        if (guess == secretNumber)
        {
            Console.WriteLine($"Correct! You got it in {guessCount} guesses.");
            hasWon = true;
            break;
        }
        else if (guess < secretNumber)
        {
            Console.WriteLine("Too low.");
        }
        else
        {
            Console.WriteLine("Too high.");
        }
    }
    ```

1. Run the program with `dotnet run`. Type a guess after each prompt and press **Enter**. You should see something like:

    ```output
    I'm thinking of a number between 1 and 20.
    You have 5 guesses. Good luck!

    Guess #1: 10
    Too low.

    Guess #2: 15
    Too high.

    Guess #3: 12
    Correct! You got it in 3 guesses.
    ```

## Announce the result

Right now, if the player runs out of guesses, the program just ends silently. You'll add a final message after the loop to reveal the secret number when the player loses.

1. Beneath the `// Announce the result` comment, add the following code:

    ```csharp
    if (!hasWon)
    {
        Console.WriteLine($"\nOut of guesses! The number was {secretNumber}.");
    }
    ```

    The `!` in `!hasWon` means "not" — so this block only runs if `hasWon` is still `false`, which happens when the player never guessed correctly and the loop ended naturally instead of hitting `break`.

1. Your complete program should now look like this:

    ```csharp
    // Set up the game
    Random random = new Random();
    int secretNumber = random.Next(1, 21);
    int maxGuesses = 5;
    int guessCount = 0;
    bool hasWon = false;

    Console.WriteLine("I'm thinking of a number between 1 and 20.");
    Console.WriteLine($"You have {maxGuesses} guesses. Good luck!");

    // Ask the player to guess
    while (guessCount < maxGuesses)
    {
        guessCount++;
        Console.Write($"\nGuess #{guessCount}: ");
        int guess = Convert.ToInt32(Console.ReadLine());

        // Check the guess and give feedback
        if (guess == secretNumber)
        {
            Console.WriteLine($"Correct! You got it in {guessCount} guesses.");
            hasWon = true;
            break;
        }
        else if (guess < secretNumber)
        {
            Console.WriteLine("Too low.");
        }
        else
        {
            Console.WriteLine("Too high.");
        }
    }

    // Announce the result
    if (!hasWon)
    {
        Console.WriteLine($"\nOut of guesses! The number was {secretNumber}.");
    }
    ```

1. Run the program a few times with `dotnet run`. Try guessing correctly on your first try, and also try running out of guesses on purpose to see the losing message.

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try each prompt below, read the response carefully, and test the code examples it gives you in VS Code.

### Discovery 1: Handle invalid input safely

**AI Prompt:**
> "In C#, what happens if I use Convert.ToInt32(Console.ReadLine()) and the user types letters instead of a number? How can I handle that safely as a beginner?"

**After the AI responds:** Right now, if the player types anything that isn't a whole number, the program crashes. Take a look at the examples the AI gives you, then try updating your `guess = Convert.ToInt32(Console.ReadLine())` line so it keeps prompting until the player enters a valid number.

<details>
<summary>Show answer</summary>
You can use `int.TryParse()` in a loop to keep asking until the player enters a valid whole number. `TryParse()` returns `true` if the conversion succeeded, and stores the result in an `out` variable:

```csharp
int guess;
while (!int.TryParse(Console.ReadLine(), out guess))
{
    Console.Write("That's not a valid number. Try again: ");
}
```
</details>

### Discovery 2: Give warmer hints

**AI Prompt:**
> "In C#, how can I check whether one number is close to another number? Can you show me an example using Math.Abs()?"

**After the AI responds:** Currently the game only says "Too high" or "Too low." Take a look at the examples the AI gives you, then try using `Math.Abs()` to detect when a guess is within 2 of the secret number, and add a "very close" hint to your feedback logic.

<details>
<summary>Show answer</summary>
`Math.Abs()` returns the positive difference between two numbers, no matter which one is larger. You can use it to check how close a guess is to the secret number:

```csharp
int difference = Math.Abs(guess - secretNumber);

if (difference <= 2 && guess != secretNumber)
{
    Console.WriteLine("You're very close!");
}
```
</details>
