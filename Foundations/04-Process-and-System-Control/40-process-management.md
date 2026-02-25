# 40-process-management.md

# Process Management

## 1. What Is a Process in Linux?

### Definition

A process is an instance of a running program. When a program is executed, the Linux kernel creates a process to manage its execution, memory, and system resources.

Each process has its own:
- Process ID (PID)
- Memory space
- File descriptors
- Execution state

### Process vs Program

- A **program** is a static file stored on disk (e.g., `/bin/ls`).
- A **process** is the active execution of that program in memory.

One program can have multiple running processes.

### Process Lifecycle Overview

A typical process lifecycle includes:
1. Creation (fork/exec)
2. Execution (running or waiting)
3. Termination (normal exit or signal-based termination)

When a process finishes, it returns an exit status to its parent.

---

## 2. Process States

Linux processes move through different states during execution.

### Running (R)

The process is either actively executing on the CPU or ready to run.

### Sleeping

#### Interruptible Sleep (S)

The process is waiting for an event (e.g., user input or I/O). It can be interrupted by signals.

#### Uninterruptible Sleep (D)

The process is waiting for a system resource (usually I/O) and cannot be interrupted until the operation completes.

### Stopped (T)

The process has been suspended, usually by a signal such as `SIGSTOP` or by pressing `CTRL+Z`.

### Zombie (Z)

The process has completed execution but still has an entry in the process table. The parent process has not yet read its exit status.

---

## 3. Viewing Processes

### ps Command

Displays a snapshot of running processes.

Common usage:

    ps aux
    ps -ef

Important columns:

- PID: Process ID
- TTY: Terminal associated with the process
- TIME: Total CPU time used
- CMD: Command that started the process
- %CPU: CPU usage percentage
- %MEM: Memory usage percentage

### top

Displays real-time system process activity.

    top

It shows CPU usage, memory usage, running tasks, and resource consumption.

### htop

An enhanced interactive version of `top` with improved visualization. It may need to be installed separately.

    htop

---

## 4. Process Identifiers

### PID (Process ID)

A unique number assigned to each running process.

### PPID (Parent Process ID)

Indicates which process created the current process.

### init/systemd as PID 1

The first process started by the kernel is PID 1. On modern systems, this is usually `systemd`. It manages system initialization and service control.

### Process Tree

Processes form a hierarchical tree structure where each process has a parent.

Display the process tree:

    pstree

This shows parent-child relationships between processes.

---

## 5. Foreground vs Background Processes

### Foreground Process

Runs in the terminal and occupies it until completion.

### Background Process

Runs without blocking the terminal.

Start a background process:

    command &

### jobs

Lists background jobs in the current shell:

    jobs

### CTRL+Z

Suspends the current foreground process and places it in a stopped state.

### bg

Resumes a suspended job in the background:

    bg %1

### fg

Brings a background job to the foreground:

    fg %1

---

## 6. Signals and Process Control

### What Is a Signal?

A signal is a notification sent to a process to trigger a specific action, such as termination or interruption.

### Common Signals

- SIGTERM (15): Requests graceful termination.
- SIGKILL (9): Forces immediate termination.
- SIGINT (2): Interrupt signal (e.g., CTRL+C).
- SIGHUP (1): Hangup signal, often used to reload configuration.

### kill Command

Sends a signal to a specific PID:

    kill PID
    kill -9 PID

### killall Command

Sends a signal to processes by name:

    killall process_name

### pkill Command

Kills processes matching a pattern:

    pkill process_name

---

## 7. Nice and Process Priority

### What Is Nice Value?

The nice value determines a process's scheduling priority. It influences how much CPU time a process receives relative to others.

### Default Nice Value

The default nice value is 0.

### Priority Range

- Nice values range from -20 (highest priority) to 19 (lowest priority).
- Only privileged users can assign negative nice values.

### nice Command

Start a process with a specific nice value:

    nice -n 10 command

### renice Command

Change the nice value of a running process:

    renice 5 -p PID

---

## 8. Process Monitoring Best Practices

- Regularly monitor system processes using `top` or `ps`.
- Investigate processes with unusually high CPU or memory usage.
- Terminate unresponsive processes using SIGTERM before SIGKILL.
- Avoid running unnecessary processes with elevated privileges.
- Review zombie processes and identify parent process issues.

---

# Summary

A process in Linux is an active instance of a program managed by the kernel. Each process has a unique PID, belongs to a process tree, and transitions through defined states. Administrators can view, control, prioritize, and terminate processes using standard tools such as `ps`, `top`, `kill`, and `nice`. Understanding process management is fundamental to system stability and security.

---

# Command Cheat Sheet

View processes:

    ps aux
    ps -ef
    top
    htop

Show process tree:

    pstree

Run in background:

    command &

Manage jobs:

    jobs
    bg %1
    fg %1

Send signals:

    kill PID
    kill -9 PID
    killall name
    pkill name

Set priority:

    nice -n 10 command
    renice 5 -p PID