# 50-bash-basics.md

# Bash Basics

## 1. Introduction to Bash

### What is Bash?

Bash (Bourne Again Shell) is a command-line interpreter used to interact with the Linux operating system. It allows users to execute commands, run programs, and automate tasks.

### Role of a Shell in Linux

A shell acts as an interface between the user and the Linux kernel. It:

- Interprets user commands
- Executes programs
- Manages input and output
- Provides scripting capabilities

### Bash as Default Shell

Bash is the default shell in many Linux distributions, including Ubuntu, Debian, CentOS, Fedora, and others.

### Importance in System Administration and Cybersecurity

Bash is essential for:

- Managing files and processes
- Configuring systems
- Running security tools
- Automating administrative tasks
- Performing incident response and system auditing

---

## 2. Basic Command Structure

### Command Syntax

Basic command structure:

    command [options] [arguments]

- **Command**: The program to execute
- **Options (flags)**: Modify command behavior (usually start with `-` or `--`)
- **Arguments**: Targets such as files or directories

### Example Commands

List files with detailed information:

    ls -l /home

Search for a word inside a file:

    grep "error" logfile.txt

Display current directory:

    pwd

---

## 3. Getting Help in Bash

### man Command

Displays the manual page for a command.

    man ls

### --help Option

Provides a brief description and available options.

    ls --help
    grep --help

### info Command

An alternative documentation system for some commands.

    info ls

---

## 4. Command History

### Viewing History

Display previously executed commands:

    history

### Re-running Previous Commands

Run the last command again:

    !!

Run a specific command by number:

    !25

Search previous commands:

    CTRL+R

### Clearing History

Clear current session history:

    history -c

---

## 5. Tab Completion and Shortcuts

### Tab Auto-Completion

Press `Tab` to automatically complete:
- Commands
- File names
- Directory names

This reduces typing errors and improves efficiency.

### CTRL+C

- Sends SIGINT
- Terminates the current running command

### CTRL+Z

- Suspends the current process
- Moves it to background (stopped state)

### CTRL+L

- Clears the terminal screen
- Equivalent to the `clear` command

---

## 6. Basic Environment Variables

### What Are Environment Variables?

Environment variables are dynamic values that influence system and program behavior.

Common examples:
- HOME
- USER
- PATH

### Viewing Variables

Display a variable value:

    echo $HOME
    echo $PATH

List all environment variables:

    env

### PATH Variable Explanation

`PATH` defines directories where Bash searches for executable commands.

Example:

    echo $PATH

If a command’s directory is not in PATH, you must use its full path.

---

## 7. Input and Output Redirection (Basic)

Linux uses three standard streams:

- stdin (0) – Standard input
- stdout (1) – Standard output
- stderr (2) – Standard error

### Redirect Standard Output

Overwrite file:

    ls > output.txt

Append to file:

    ls >> output.txt

### Redirect Standard Error

    ls nonexistentfile 2> error.txt

---

## 8. Pipes

### Concept of Piping

A pipe (`|`) sends the output of one command as input to another command.

This allows chaining commands together.

### Example

Search for a process and filter results:

    ps aux | grep ssh

Count number of files:

    ls | wc -l

---

## 9. Summary

Bash is the primary command-line interface in many Linux systems. Understanding command structure, history, environment variables, redirection, and pipes forms the foundation for effective Linux usage. These skills are critical for system administration, automation, and cybersecurity workflows, enabling efficient system management and analysis.