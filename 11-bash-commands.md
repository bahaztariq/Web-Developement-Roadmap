# 💻 Bash Scripting & Terminal Commands

## Summary

This document covers Bash scripting and terminal commands for developers. Topics include navigation commands, file and directory operations, viewing and searching files, permissions and ownership management, system and process monitoring, redirection and pipes for command composition, networking basics, bash scripting fundamentals (variables, conditionals, loops), and shell customization.

## Sommaire

- [1. Introduction](#1-introduction)
  - [What is Bash?](#what-is-bash)
- [2. Navigation Commands](#2-navigation-commands)
  - [Examples:](#examples)
- [3. File & Directory Operations](#3-file-&-directory-operations)
  - [Examples:](#examples)
- [4. Viewing & Searching Files](#4-viewing-&-searching-files)
  - [Examples:](#examples)
- [5. Permissions & Ownership](#5-permissions-&-ownership)
  - [Numeric Permissions (chmod):](#numeric-permissions-chmod)
- [6. System & Process Management](#6-system-&-process-management)
- [7. Redirection & Pipes](#7-redirection-&-pipes)
  - [Pipes (`|`)](#pipes-`|`)
  - [Redirection (`>`, `>>`)](#redirection-`>`-`>>`)
- [8. Networking Basics](#8-networking-basics)
- [9. Bash Scripting Basics](#9-bash-scripting-basics)
  - [The Shebang](#the-shebang)
  - [Variables](#variables)
  - [Conditional Logic (If Statements)](#conditional-logic-if-statements)
  - [Loops (For Loops)](#loops-for-loops)
- [10. Useful Keyboard Shortcuts](#10-useful-keyboard-shortcuts)
- [11. Customizing Your Shell (.bashrc / .zshrc)](#11-customizing-your-shell-bashrc-/-zshrc)



> The terminal (command line) is a developer's most powerful tool. It allows you to interact with your computer's operating system directly, automate tasks, and manage files faster than with a GUI.

---

## 1. Introduction

### What is Bash?

**Definition:** Bash (Bourne Again SHell) is a command-line interpreter that runs in a terminal window. It allows users to type commands to perform actions. It is the default shell for most Linux distributions and macOS (though macOS now defaults to Zsh, which is very similar).

**Why learn it?**
- **Speed:** Perform complex file operations instantly.
- **Power:** Automate repetitive tasks with scripts.
- **Remote Access:** Manage servers via SSH (where there is no GUI).
- **Tooling:** Git, npm, Composer, and Docker all run primarily in the terminal.

---

## 2. Navigation Commands

Navigating the file system is the most fundamental skill.

| Command | Definition | Example |
|---------|------------|---------|
| `pwd` | **Print Working Directory** - Shows the full path of where you currently are. | `pwd` → `/home/user/project` |
| `ls` | **List** - Lists files and directories in the current folder. | `ls -la` (list all, including hidden files, with details) |
| `cd` | **Change Directory** - Moves you to a different folder. | `cd my-project` |
| `cd ..` | Move up one directory level (parent directory). | `cd ..` |
| `cd ~` | Move to your home directory. | `cd ~` |
| `cd -` | Move to the previous directory you were in. | `cd -` |

### Examples:

```bash
# Where am I?
pwd

# List files with details (permissions, size, date)
ls -l

# Go into a folder
cd Documents

# Go back up
cd ..
```

---

## 3. File & Directory Operations

Creating, moving, and deleting files and folders.

| Command | Definition | Example |
|---------|------------|---------|
| `mkdir` | **Make Directory** - Creates a new folder. | `mkdir new-folder` |
| `touch` | Creates an empty file or updates the timestamp of an existing one. | `touch new-file.txt` |
| `cp` | **Copy** - Copies files or directories. | `cp file.txt copy.txt` |
| `cp -r` | Copy a directory and all its contents (recursive). | `cp -r folder/ backup/` |
| `mv` | **Move** - Moves or **renames** files/directories. | `mv old.txt new.txt` |
| `rm` | **Remove** - Deletes files. **Warning: This is permanent.** | `rm file.txt` |
| `rm -rf` | Force remove a directory and everything inside it. **Use with caution!** | `rm -rf folder/` |

### Examples:

```bash
# Create a robust project structure
mkdir my-project
cd my-project
touch index.html style.css script.js README.md
mkdir assets images
```

---

## 4. Viewing & Searching Files

| Command | Definition | Example |
|---------|------------|---------|
| `cat` | **Concatenate** - Displays the entire content of a file. | `cat README.md` |
| `less` | View a file one page at a time (use arrows to scroll, `q` to quit). | `less huge-log-file.log` |
| `head` | View the first 10 lines of a file. | `head -n 5 file.txt` |
| `tail` | View the last 10 lines of a file. | `tail -n 5 file.txt` |
| `grep` | **Global Regular Expression Print** - Search for text within files. | `grep "error" app.log` |
| `find` | Search for files in a directory hierarchy. | `find . -name "*.css"` |

### Examples:

```bash
# Search for "function" in all JavaScript files recursively
grep -r "function" .

# Find all PHP files in the current folder
find . -name "*.php"
```

---

## 5. Permissions & Ownership

Linux/Unix file systems have strict permissions (Read, Write, Execute).

| Command | Definition | Example |
|---------|------------|---------|
| `chmod` | **Change Mode** - Change file permissions. | `chmod +x script.sh` (make executable) |
| `chown` | **Change Owner** - Change file owner and group. | `chown user:group file.txt` |
| `sudo` | **SuperUser Do** - Run a command with administrative (root) privileges. | `sudo apt update` |

### Numeric Permissions (chmod):
- **Read (r)** = 4
- **Write (w)** = 2
- **Execute (x)** = 1

Example: `chmod 755 file` (Owner=7 (r+w+x), Group=5 (r+x), Others=5 (r+x))

---

## 6. System & Process Management

| Command | Definition | Example |
|---------|------------|---------|
| `top` / `htop` | View running processes and system resource usage (CPU, RAM). | `htop` |
| `ps` | **Process Status** - Snapshot of current processes. | `ps aux` |
| `kill` | Terminate a process by its ID (PID). | `kill 1234` |
| `df` | **Disk Free** - View disk space usage. | `df -h` (human readable) |
| `du` | **Disk Usage** - View space used by files/directories. | `du -sh folder/` |

---

## 7. Redirection & Pipes

Combine commands to build powerful workflows.

### Pipes (`|`)
Takes the output of the command on the left and uses it as input for the command on the right.

```bash
# List all files, then search for "json" in that list
ls -la | grep "json"

# View running processes, then count them (`wc -l` counts lines)
ps aux | wc -l
```

### Redirection (`>`, `>>`)
Sends the output of a command to a file.

```bash
# Overwrite file with output
echo "Hello World" > hello.txt

# Append to file (add to the end)
echo "Another line" >> hello.txt
```

---

## 8. Networking Basics

| Command | Definition | Example |
|---------|------------|---------|
| `ping` | Check connectivity to a host. | `ping google.com` |
| `curl` | Transfer data from/to a server. Great for testing APIs. | `curl https://api.github.com` |
| `ssh` | **Secure Shell** - Log into a remote machine. | `ssh user@192.168.1.50` |
| `ip a` / `ifconfig` | Show network interface information (IP address). | `ip a` |

---

## 9. Bash Scripting Basics

You can save commands in a file (usually ending in `.sh`) to run them all at once.

### The Shebang
Every script starts with a "shebang" line telling the system what interpreter to use.

```bash
#!/bin/bash
```

### Variables
No spaces around the `=` sign.

```bash
NAME="Tariq"
echo "Hello, $NAME!"
```

### Conditional Logic (If Statements)

```bash
#!/bin/bash

if [ -f ".env" ]; then
    echo ".env file exists."
else
    echo ".env file is missing!"
fi
```

### Loops (For Loops)

```bash
#!/bin/bash

# Loop through all .txt files and rename them
for file in *.txt; do
    echo "Processing $file..."
    mv "$file" "backup_$file"
done
```

---

## 10. Useful Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Tab` | Auto-complete file or directory names. |
| `Ctrl + C` | Kill (stop) the currently running command. |
| `Ctrl + L` | Clear the terminal screen. |
| `Ctrl + A` | Move cursor to the beginning of the line. |
| `Ctrl + E` | Move cursor to the end of the line. |
| `Up Arrow` | Scroll through command history. |
| `Ctrl + R` | Search command history. |

---

## 11. Customizing Your Shell (.bashrc / .zshrc)

You can create aliases for commands you use often in your configuration file (`~/.bashrc` for Bash, `~/.zshrc` for Zsh).

```bash
# Add this to your config file
alias laravel="php artisan"
alias gs="git status"
alias ll="ls -la"
```

After editing, run `source ~/.bashrc` (or `~/.zshrc`) to apply changes.
