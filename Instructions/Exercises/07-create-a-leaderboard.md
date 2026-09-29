---
lab:
    title: 'Create a Top 5 leaderboard'
    description: 'Write a C# program that logs game scores in a List<int> and builds a fixed-size Top 5 leaderboard array.'
    level: 100
    duration: 25
    islab: true
    status: 'released'
---

# Create a Top 5 leaderboard

In this exercise, you build a simple arcade-style scoring program. As each round is played, the score gets logged to a resizable `List<int>`. Once every round is finished, you copy the five highest scores into a fixed-size `int[]` array that always holds exactly five ranks. You practice using `List<T>` methods like `Add`, `Count`, `Sort`, and `Reverse`, along with array indexing and `Length`, and you see firsthand why a leaderboard's Top 5 is a great fit for an array while the running score log is a great fit for a list.

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

1. In the VS Code file explorer, navigate to the `Labfiles/07-create-a-leaderboard` subfolder.

1. Select the `Program.cs` file. You'll see a set of guiding comments that act as an outline for your program — each one marks where a specific piece of code belongs:

    ```csharp
    // Set up the game

    // Simulate playing rounds and log every score

    // Build the Top 5 leaderboard array

    // Print the leaderboard
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code. In the steps that follow, you'll add code beneath each comment.

1. If VS Code shows a prompt about restoring project dependencies, select **Restore**.

## Log every score in a resizable list

You don't know how many rounds might eventually be played, so you'll store every score in a `List<int>` — a collection that can grow as new scores come in.

1. Beneath the `// Set up the game` comment, add the following lines:

    ```csharp
    Random random = new Random();
    int roundsPlayed = 8;
    List<int> allScores = new List<int>();

    Console.WriteLine($"Playing {roundsPlayed} rounds...\n");
    ```

    - `random.Next(...)` will generate each round's score, so `random` is set up once, up front.
    - `allScores` starts out empty — you'll `Add` a score to it after every round.

1. Beneath the `// Simulate playing rounds and log every score` comment, add the following lines:

    ```csharp
    for (int round = 1; round <= roundsPlayed; round++)
    {
        int score = random.Next(0, 101);
        allScores.Add(score);
        Console.WriteLine($"Round {round}: scored {score} points");
    }

    Console.WriteLine($"\nTotal rounds logged: {allScores.Count}");
    ```

    - `random.Next(0, 101)` returns a random whole number from `0` up to, but not including, `101` — so each score is from `0` to `100`.
    - `allScores.Add(score)` appends the new score to the end of the list, growing it by one each time through the loop.
    - `allScores.Count` reports how many scores have been logged so far.

1. Save the file, then run your program. Open a new terminal (**Terminal > New Terminal**), navigate to the project folder, and run the program:

    ```bash
    cd Labfiles/07-create-a-leaderboard
    dotnet run
    ```

    You should see something like:

    ```output
    Playing 8 rounds...

    Round 1: scored 42 points
    Round 2: scored 88 points
    Round 3: scored 15 points
    Round 4: scored 100 points
    Round 5: scored 67 points
    Round 6: scored 73 points
    Round 7: scored 29 points
    Round 8: scored 91 points

    Total rounds logged: 8
    ```

    > **Tip**: If you have the C# Dev Kit extension installed, you can also select the **Run** button that appears above your code instead of using the terminal. You only need to `cd` into the project folder once per terminal session — after that, `dotnet run` alone will work for the rest of this exercise. Your own scores will be different every run, since they're randomly generated.

## Build the Top 5 leaderboard array

A leaderboard always shows exactly five ranks, no more and no fewer — that's a perfect job for a fixed-size array. You'll sort the logged scores from highest to lowest, then copy the top five into the array by index.

1. Beneath the `// Build the Top 5 leaderboard array` comment, add the following lines:

    ```csharp
    allScores.Sort();
    allScores.Reverse();

    int[] topScores = new int[5];

    for (int i = 0; i < topScores.Length; i++)
    {
        topScores[i] = allScores[i];
    }
    ```

    - `allScores.Sort()` puts the list in order from lowest to highest.
    - `allScores.Reverse()` flips that order, so the highest score ends up first.
    - `topScores` is declared with `new int[5]` — its length is locked at five slots for the rest of the program.
    - The loop copies the five highest values from `allScores` into `topScores`, using `topScores.Length` so the loop always fills exactly five slots, however many rounds were played.

## Print the leaderboard

Now that `topScores` holds the five highest scores in order, you can read it by index to display the final rankings.

1. Beneath the `// Print the leaderboard` comment, add the following lines:

    ```csharp
    Console.WriteLine("\n🏆 Top 5 Leaderboard 🏆");

    for (int i = 0; i < topScores.Length; i++)
    {
        Console.WriteLine($"{i + 1}. {topScores[i]} points");
    }
    ```

    - `i + 1` turns the zero-based index into a familiar 1st-through-5th ranking.
    - `topScores[i]` reads the score stored at that rank's position in the array.

1. Your complete program should now look like this:

    ```csharp
    // Set up the game
    Random random = new Random();
    int roundsPlayed = 8;
    List<int> allScores = new List<int>();

    Console.WriteLine($"Playing {roundsPlayed} rounds...\n");

    // Simulate playing rounds and log every score
    for (int round = 1; round <= roundsPlayed; round++)
    {
        int score = random.Next(0, 101);
        allScores.Add(score);
        Console.WriteLine($"Round {round}: scored {score} points");
    }

    Console.WriteLine($"\nTotal rounds logged: {allScores.Count}");

    // Build the Top 5 leaderboard array
    allScores.Sort();
    allScores.Reverse();

    int[] topScores = new int[5];

    for (int i = 0; i < topScores.Length; i++)
    {
        topScores[i] = allScores[i];
    }

    // Print the leaderboard
    Console.WriteLine("\n🏆 Top 5 Leaderboard 🏆");

    for (int i = 0; i < topScores.Length; i++)
    {
        Console.WriteLine($"{i + 1}. {topScores[i]} points");
    }
    ```

1. Run the program a few times with `dotnet run`. Since the scores are random, you'll see a different leaderboard each time.

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try each prompt below, read the response carefully, and test the code examples it gives you in VS Code.

### Discovery 1: Handle fewer than 5 scores safely

**AI Prompt:**
> "In C#, what happens if I try to read an index from a List<int> that has fewer items than the index I'm asking for? How can I safely fill a fixed-size array from a list that might not have enough items yet, as a beginner?"

**After the AI responds:** Right now, the program assumes at least five rounds were played — try changing `roundsPlayed` to `3` and rerunning to see what happens. Take a look at the examples the AI gives you, then try updating your leaderboard loop so it only fills as many slots as there are scores available.

<details>
<summary>Show answer</summary>
You can use `Math.Min()` to limit the loop to whichever is smaller: the array's length or the list's count. Any slots left over simply stay at their default value of `0`:

```csharp
int slotsToFill = Math.Min(topScores.Length, allScores.Count);

for (int i = 0; i < slotsToFill; i++)
{
    topScores[i] = allScores[i];
}
```
</details>

### Discovery 2: Align your leaderboard neatly

**AI Prompt:**
> "In C#, how can I use string interpolation to add fixed-width spacing so numbers line up in columns, like a scoreboard?"

**After the AI responds:** Currently the leaderboard's rank and score numbers don't line up neatly when the digit counts differ. Take a look at the examples the AI gives you, then try adding alignment to your leaderboard's `Console.WriteLine` so the score column lines up no matter how many digits each score has.

<details>
<summary>Show answer</summary>
Adding a comma and a number inside the interpolation braces, like `{value,width}`, pads that value to a fixed column width. A positive width right-aligns the text, and a negative width left-aligns it:

```csharp
for (int i = 0; i < topScores.Length; i++)
{
    Console.WriteLine($"{i + 1,2}. {topScores[i],3} points");
}
```
</details>
