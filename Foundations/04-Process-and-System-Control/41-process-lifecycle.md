# 41-process-lifecycle.md

# Linux Process Lifecycle

## 1. Introduction

### Definition of Process Lifecycle

The process lifecycle in Linux refers to the stages a process goes through from creation to termination. It encompasses the creation, execution, state transitions, and eventual cleanup of a process by the kernel.

### Importance in Linux and Cybersecurity

Understanding the process lifecycle is essential for:
- Monitoring system health and resource usage
- Troubleshooting unresponsive or misbehaving applications
- Detecting abnormal or suspicious processes in security investigations
- Managing zombie and orphan processes to maintain system stability

---

## 2. Process Creation

### fork() System Call

`fork()` is used to create a new process by duplicating the calling process. The new process is called the child, while the original is the parent. Both continue execution independently.

### exec() Family of Functions

`exec()` replaces the current process image with a new program. It is commonly used after `fork()` to run a different program in the child process.

### Parent and Child Relationship

- The parent process initiates the child process.
- The child inherits environment, open file descriptors, and scheduling attributes.
- Each child has a unique PID and the parent’s PID as its PPID.

### Example Commands

Create a background process:

    sleep 60 &

Run a command replacing the current shell process:

    exec ls -l

---

## 3. Process States

Linux processes move through specific states during their lifecycle.

### New

The process is being created but has not yet been scheduled to run.

### Running (R)

The process is either executing on the CPU or ready to run.

### Waiting

#### Interruptible Sleep (S)

The process waits for an event (e.g., I/O) and can be interrupted by signals.

#### Uninterruptible Sleep (D)

The process waits for a resource (e.g., disk I/O) and cannot be interrupted.

### Stopped (T)

The process has been suspended, usually via `SIGSTOP` or `CTRL+Z`.

### Zombie (Z)

The process has completed execution but still has an entry in the process table until the parent reads its exit status.

### Viewing Process State

Using `ps`:

    ps aux
    ps -eo pid,ppid,state,cmd

Using `top`:

    top

State is displayed in the `STAT` column.

---

## 4. Process Termination

### Normal Exit

A process terminates by completing its execution and returning an exit status to its parent.

### Kill Signals

- SIGTERM (15): Requests graceful termination.
- SIGKILL (9): Forces immediate termination.

### Zombie and Orphan Processes

- **Zombie:** Completed processes waiting for parent to read exit status.
- **Orphan:** Child processes whose parent has exited; adopted by `init/systemd` (PID 1) and reaped.

---

## 5. Process Hierarchy

### PID and PPID

- PID: Unique identifier for a process.
- PPID: Identifier of the parent process.

### Process Tree Concept

Processes form a hierarchical tree, showing parent-child relationships.

### Using pstree

    pstree
    pstree -p

Displays the process hierarchy with PIDs.

---

## 6. Practical Examples

### Creating Foreground and Background Processes

Foreground:

    sleep 30

Background:

    sleep 60 &

### Observing State Changes

Check process state:

    ps -ef | grep sleep
    top

### Sending Signals

Terminate a process:

    kill PID
    kill -9 PID
    killall sleep
    pkill sleep

---

## 7. Summary

The Linux process lifecycle encompasses creation, execution, state transitions, and termination. Processes are created using `fork()` and optionally `exec()`, move through states such as running, sleeping, stopped, and zombie, and are eventually terminated or reaped. Understanding the lifecycle is critical for system monitoring, troubleshooting, and maintaining security hygiene.
