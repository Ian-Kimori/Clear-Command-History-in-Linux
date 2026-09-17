# Clear-Command-History-in-Linux

To clear your command history in Linux, you can **use the** **`history -c`** **command to wipe the current session's memory and overwrite the permanent log file using** **`history -w`**. Because Linux caches history in RAM before writing it to a file, completely erasing it requires clearing both locations.

## 1. Clear All History Completely (Recommended)

To erase your history from both the terminal's active memory and the permanent history file (`~/.bash_history`), run:

```bash
history -c && history -w
````

* `history -c`: Clears the history of your current active terminal session.
* `history -w`: Forces the shell to write this now-empty session state over your permanent history file, effectively blanking it out.

> **Note:** If you use Zsh instead of Bash, your history file is typically `~/.zsh_history` rather than `~/.bash_history`.

## 2. Delete the History File Directly

Alternatively, you can empty the history file itself and clear your current memory:

```bash
rm ~/.bash_history
history -c
```

Alternatively, to keep the file but empty its contents, use:

```bash
cat /dev/null > ~/.bash_history && history -c
```

## 3. Delete a Specific Command Line

If you don't want to clear everything but need to remove a specific entry (like an accidentally typed password):

1. Type `history` to view your commands with their corresponding line numbers.

2. Delete the specific line using the `-d` flag:

```bash
history -d <line_number>
```

3. Save the changes to your permanent file:

```bash
history -w
```
## 4. Delete a Specific Command Line Range

If you don't want to clear everything but need to remove a specific entry (like an accidentally typed password):

1. Type `history` to view your commands with their corresponding line numbers.

2. Delete the specific range using:

### Method A: Use a Backward Loop (Most Reliable)
Line numbers shift down as each item is deleted, so deleting from highest to lowest prevents errors. Replace 105 and 100 with your end and start numbers:

```bash
for i in {105..100}; do history -d $i; done
```

### Method B: Direct Range (If Supported)
In some Bash versions, you can specify a direct range:

```bash
history -d 100-105
```
3. Save the changes to your permanent file:

```bash
history -w
```

## 5. Prevent Commands from Being Recorded

### Add a Leading Space

By default on many distributions, if you type a **space** before typing a command (e.g., `  cat secret.txt`), the shell will execute it but won't log it to your history file.

```bash
  cat secret.txt
```

### Disable History for the Current Session

If you are about to do sensitive work, run:

```bash
unset HISTFILE
```

This stops the terminal from saving anything you type after that point to your history file when you log out.

## Additional Options

Would you like to know how to **automate clearing history on logout**, or are you looking to configure your system to **permanently ignore specific commands**?

```
```
