# 54-pipes-and-streams.md

# Pipes and Streams in Bash

## 1. Introduction

### What Are Pipes in Linux?

A pipe is a mechanism in Bash that connects the output of one command directly to the input of another command. Pipes allow multiple commands to work together in sequence.

### Concept of Data Streams

Linux commands use data streams to send and receive information. These streams can be redirected, filtered, or passed between commands.

### Why Pipes Are Important in Linux Philosophy

Pipes reflect a core Linux philosophy: build small, focused tools and combine them to perform complex tasks. Instead of writing large programs, users connect simple commands to solve problems efficiently.

---

## 2. Understanding Data Streams

### Standard Input (stdin)

- File descriptor: 0
- Default input source (usually keyboard)

### Standard Output (stdout)

- File descriptor: 1
- Default output destination (usually terminal)

### Standard Error (stderr)

- File descriptor: 2
- Used for error messages

### How Streams Flow Between Commands

When using a pipe (`|`):

- The stdout of the first command becomes the stdin of the next command.
- Only standard output is passed through the pipe.
- Standard error is not included unless explicitly redirected.

---

## 3. The Pipe Operator (|)

### Basic Syntax

    command1 | command2

### How It Works

1. `command1` executes.
2. Its standard output is captured.
3. That output becomes the standard input for `command2`.
4. `command2` processes the data and produces its own output.

This creates a continuous flow of processed data.

### Example

    ls | wc -l

This counts the number of files listed by `ls`.

---

## 4. Practical Pipe Examples

### Using `ls` with `grep`

Filter files containing a specific name:

    ls | grep ".txt"

---

### Using `ps` with `grep`

Find a running process:

    ps aux | grep ssh

---

### Using `cat` with `sort`

Sort contents of a file:

    cat names.txt | sort

---

### Using `history` with `grep`

Search command history:

    history | grep ssh

---

## 5. Combining Pipes with Redirection

### Redirecting Final Output to a File

Save filtered output:

    ps aux | grep nginx > nginx_processes.txt

---

### Logging Filtered Output

Log errors or results:

    dmesg | grep error > errors.log

Pipes process the data, and redirection saves the final result.

---

## 6. Filtering and Processing Concepts

### Small Tools Working Together

Linux commands are designed to perform specific tasks:

- `grep` filters text
- `sort` orders lines
- `wc` counts lines, words, or characters
- `uniq` removes duplicate lines

By chaining them, complex operations become simple and readable.

Example:

    cat access.log | grep "404" | sort | uniq

---

### Linux Philosophy: “Do One Thing Well”

Each command focuses on a single function. Combining them through pipes increases flexibility without increasing complexity.

### Why Chaining Commands Increases Power

Pipelines allow:

- Real-time data processing
- Efficient resource usage
- Quick analysis without temporary files

---

## 7. Basic Security Relevance

### Log Analysis

Search for suspicious login attempts:

    cat /var/log/auth.log | grep "Failed password"

---

### Filtering Suspicious Processes

    ps aux | grep root

---

### Extracting System Information

    netstat -tuln | grep LISTEN

Pipes allow administrators to quickly isolate relevant information during security investigations.

---

## 8. Summary

Pipes (`|`) connect commands by passing standard output from one command to standard input of another. This enables powerful command chaining and efficient data processing. Understanding data streams and pipelines is fundamental for automation, troubleshooting, and cybersecurity workflows in Linux environments.