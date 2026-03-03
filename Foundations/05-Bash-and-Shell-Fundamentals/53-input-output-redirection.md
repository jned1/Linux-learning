# 53-input-output-redirection.md

# Input and Output Redirection in Bash

## 1. Introduction

### What is Input/Output Redirection?

Input/output redirection is a Bash feature that allows users to control where command input comes from and where command output goes. Instead of displaying output on the screen or reading input from the keyboard, data can be redirected to or from files.

### Why Redirection Is Important in Linux

Redirection is essential for:

- Saving command results to files
- Logging program output
- Automating tasks
- Troubleshooting errors
- Controlling noisy command output

### Basic Concept of Data Streams

In Linux, processes communicate using data streams. By default:

- Input comes from the keyboard
- Output goes to the terminal screen
- Errors are displayed on the terminal

Redirection modifies this default behavior.

---

## 2. Standard Streams

Every Linux process has three standard data streams:

### Standard Input (stdin)

- Default source of input
- Usually the keyboard
- File descriptor: 0

### Standard Output (stdout)

- Default destination for normal output
- Usually the terminal screen
- File descriptor: 1

### Standard Error (stderr)

- Used for error messages
- Also displayed on the terminal by default
- File descriptor: 2

Understanding file descriptor numbers (0, 1, 2) is important for advanced redirection control.

---

## 3. Output Redirection

### Using `>`

Redirects standard output to a file. If the file exists, it is overwritten.

    ls > files.txt

---

### Using `>>`

Appends standard output to a file without overwriting existing content.

    ls >> files.txt

---

### Overwriting vs Appending

- `>` replaces file contents
- `>>` adds new content to the end of the file

Example:

    echo "First line" > output.txt
    echo "Second line" >> output.txt

---

## 4. Error Redirection

### Using `2>`

Redirects standard error to a file.

    ls nonexistentfile 2> error.txt

---

### Redirecting Errors to a File

Errors will be written to the specified file instead of appearing on the terminal.

---

### Combining stdout and stderr (`2>&1`)

Redirect both standard output and standard error to the same file.

    ls validfile nonexistentfile > all_output.txt 2>&1

This ensures both normal output and errors are logged together.

---

## 5. Input Redirection

### Using `<`

Redirects input from a file instead of the keyboard.

Example:

    sort < names.txt

This sends the contents of `names.txt` to the `sort` command as input.

---

## 6. Redirecting to /dev/null

### Purpose of /dev/null

`/dev/null` is a special device file that discards all data written to it. It is commonly referred to as a "black hole" for output.

### Silencing Output

Suppress standard output:

    ls > /dev/null

Suppress error output:

    ls nonexistentfile 2> /dev/null

Suppress both:

    ls validfile nonexistentfile > /dev/null 2>&1

---

## 7. Practical Examples

### Save Command Output to a File

    ps aux > processes.txt

---

### Log Both Output and Errors

    python3 script.py > script.log 2>&1

---

### Suppress Unwanted Output

    grep "pattern" largefile.txt > /dev/null

---

## 8. Summary

Input and output redirection allows precise control over data streams in Bash. By understanding stdin (0), stdout (1), and stderr (2), users can redirect output, capture errors, read input from files, and suppress unnecessary output. These fundamentals are critical for automation, logging, and troubleshooting in Linux system administration and cybersecurity workflows.