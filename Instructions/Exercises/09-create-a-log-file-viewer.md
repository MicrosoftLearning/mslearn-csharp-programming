---
lab:
    title: 'Create a log file viewer'
    description: 'Write a C# program that appends event entries to a log file, then reads them back line by line with a StreamReader.'
    level: 100
    duration: 25
    islab: true
    status: 'released'
---

# Create a log file viewer

In this exercise, you build a small event logger. Your program appends a new entry to a log file every time it "runs," without erasing what's already there, then reads every entry back one line at a time to display the full history and count how many events have been logged. You practice using `File.AppendAllText()` to add to a file, and a `StreamReader` with `.ReadLine()` in a loop that keeps going until it reaches the end of the file.

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

1. In the VS Code file explorer, navigate to the `Labfiles/09-create-a-log-file-viewer` subfolder.

1. Select the `Program.cs` file. You'll see a set of guiding comments that act as an outline for your program — each one marks where a specific piece of code belongs:

    ```csharp
    // Log a new event

    // Read back every logged event

    // Count the logged events
    ```

    Remember, comments are ignored by C# when the program runs. They're just there to help you organize your code. In the steps that follow, you'll add code beneath each comment.

1. If VS Code shows a prompt about restoring project dependencies, select **Restore**.

## Log a new event by appending to a file

Every time the program runs, it should add one new entry to `log.txt` without erasing the entries from earlier runs.

1. Beneath the `// Log a new event` comment, add the following lines:

    ```csharp
    string logFile = "log.txt";
    string timestamp = DateTime.Now.ToString("HH:mm:ss");

    File.AppendAllText(logFile, $"[{timestamp}] Application started\n");

    Console.WriteLine("Event logged.\n");
    ```

    - `File.AppendAllText()` adds to the **end** of `log.txt`, keeping every entry from previous runs intact. If the file doesn't exist yet, C# creates it.
    - `DateTime.Now.ToString("HH:mm:ss")` gives each entry its own timestamp, so you can tell runs apart.

1. Save the file, then run your program. Open a new terminal (**Terminal > New Terminal**), navigate to the project folder, and run the program:

    ```bash
    cd Labfiles/09-create-a-log-file-viewer
    dotnet run
    ```

    You should see:

    ```output
    Event logged.
    ```

1. Run the program two or three more times with `dotnet run`. Each run adds a new line to `log.txt` — open `log.txt` in the VS Code file explorer to see the entries building up, each with its own timestamp.

    > **Tip**: If you have the C# Dev Kit extension installed, you can also select the **Run** button that appears above your code instead of using the terminal. You only need to `cd` into the project folder once per terminal session — after that, `dotnet run` alone will work for the rest of this exercise.

## Read back every logged event

Now you'll read `log.txt` one line at a time using a `StreamReader`. Its `.ReadLine()` method returns the next line each time you call it, and returns `null` once there are no more lines left — that's your signal to stop.

1. Beneath the `// Read back every logged event` comment, add the following lines:

    ```csharp
    Console.WriteLine("Event history:");

    using StreamReader reader = new StreamReader(logFile);
    string line;

    while ((line = reader.ReadLine()) != null)
    {
        Console.WriteLine(line);
    }
    ```

    - `using StreamReader reader = ...` opens the file and guarantees it's closed automatically at the end of this block, even if something goes wrong while reading.
    - `(line = reader.ReadLine()) != null` does two things every time through the loop: it reads the next line into `line`, *and* checks whether that line was actually there. When `.ReadLine()` runs out of lines, it returns `null`, and the loop stops.

1. Run the program again with `dotnet run`. You should now see every entry logged so far, printed one per line:

    ```output
    Event logged.

    Event history:
    [09:12:04] Application started
    [09:12:41] Application started
    [09:13:07] Application started
    ```

## Count the logged events

Finally, you'll keep a running count of how many entries were read, so you know at a glance how many times the program has run in total.

1. Beneath the `// Count the logged events` comment, add the following lines:

    ```csharp
    string[] allLines = File.ReadAllLines(logFile);
    Console.WriteLine($"\nTotal events logged: {allLines.Length}");
    ```

    - `File.ReadAllLines()` reads the whole file again, this time as a `string[]` where each element is one line — a quick way to get a count without writing your own loop.
    - `allLines.Length` reports how many lines (and therefore how many logged events) the file contains.

1. Your complete program should now look like this:

    ```csharp
    // Log a new event
    string logFile = "log.txt";
    string timestamp = DateTime.Now.ToString("HH:mm:ss");

    File.AppendAllText(logFile, $"[{timestamp}] Application started\n");

    Console.WriteLine("Event logged.\n");

    // Read back every logged event
    Console.WriteLine("Event history:");

    using StreamReader reader = new StreamReader(logFile);
    string line;

    while ((line = reader.ReadLine()) != null)
    {
        Console.WriteLine(line);
    }

    // Count the logged events
    string[] allLines = File.ReadAllLines(logFile);
    Console.WriteLine($"\nTotal events logged: {allLines.Length}");
    ```

1. Run the program a few more times with `dotnet run` and watch the total climb by one each time.

## Code with AI

Using an AI assistant (like Copilot) is a great way to explore a programming language at your own pace. Try each prompt below, read the response carefully, and test the code examples it gives you in VS Code.

### Discovery 1: Handle a missing log file safely

**AI Prompt:**
> "In C#, what exception is thrown if I try to read a file with StreamReader or File.ReadAllLines and the file doesn't exist yet? How can I check safely as a beginner?"

**After the AI responds:** Delete `log.txt` from your project folder, then run the program once. Since `File.AppendAllText()` creates the file automatically, this particular program won't crash — but take a look at the examples the AI gives you, then try adding a check with `File.Exists(logFile)` before the reading section, so your program could handle a truly missing file gracefully in a program that doesn't create one automatically.

<details>
<summary>Show answer</summary>
`File.Exists()` returns `true` or `false` without throwing an exception, so you can check before you try to read:

```csharp
if (File.Exists(logFile))
{
    string[] allLines = File.ReadAllLines(logFile);
    Console.WriteLine($"\nTotal events logged: {allLines.Length}");
}
else
{
    Console.WriteLine("No log file found yet.");
}
```
</details>

### Discovery 2: Clear the log with a fresh start option

**AI Prompt:**
> "In C#, how can I let a user choose between appending to a file and overwriting it, based on their input?"

**After the AI responds:** Take a look at the examples the AI gives you, then try adding a prompt at the start of your program asking the user whether they want to clear the log, and use `File.WriteAllText()` to erase it if they say yes.

<details>
<summary>Show answer</summary>
You can ask for input first, then choose between `File.WriteAllText()` (overwrite) and `File.AppendAllText()` (append) based on the answer:

```csharp
Console.Write("Clear the log first? (y/n): ");
string answer = Console.ReadLine();

if (answer == "y")
{
    File.WriteAllText(logFile, "");
    Console.WriteLine("Log cleared.\n");
}
```
</details>
