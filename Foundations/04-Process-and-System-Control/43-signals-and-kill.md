# 43-signals-and-kill.md

# Signals and Kill in Linux

## 1. Introduction

### Definition of Signals

Signals are software interrupts used in Linux to notify processes of events or to request specific actions, such as termination or suspension.

### Importance in Process Management

- Allows controlled termination or communication between processes
- Facilitates multitasking and system stability
- Enables administrators to manage unresponsive processes

### Relevance to Cybersecurity and System Administration

- Detect and terminate rogue or malicious processes
- Ensure critical services remain operational
- Prevent privilege escalation through misbehaving processes

---

## 2. Common Signals

### SIGTERM (15)

- Requests graceful termination
- Process can perform cleanup before exiting
- Example:

    kill -15 1234

### SIGKILL (9)

- Forces immediate termination
- Cannot be ignored by the process
- Example:

    kill -9 1234

### SIGINT (2)

- Interrupt signal sent from terminal (e.g., CTRL+C)
- Allows the process to terminate or handle interruption
- Example:

    ./long_running_process
    CTRL+C

### SIGHUP (1)

- Sent when terminal closes or to reload configuration
- Often used to signal daemons to reload
- Example:

    kill -SIGHUP 1234

---

## 3. Sending Signals

### `kill` Command

- Sends signals to processes by PID
- Syntax:

    kill -SIGNAL PID
    kill -9 1234

### `killall` Command

- Sends signals to all processes with a given name
- Syntax:

    killall -SIGNAL process_name
    killall -9 sleep

### `pkill` Command

- Sends signals based on process name patterns
- Syntax:

    pkill -SIGNAL pattern
    pkill -15 "python"

---

## 4. Listing Available Signals

### `kill -l`

- Lists all signals by name and number
- Numeric vs symbolic notation:

    kill -l
    1) SIGHUP       2) SIGINT       3) SIGQUIT
    9) SIGKILL      15) SIGTERM     18) SIGCONT

---

## 5. Handling Signals in Processes

### Default Action vs Custom Handling

- By default, signals like SIGTERM terminate the process
- Programs can implement custom handlers for signals

### Example: Handling SIGINT

    #!/bin/bash
    trap "echo 'SIGINT received, exiting'; exit" SIGINT
    while true; do sleep 1; done

- Press CTRL+C to trigger the trap

---

## 6. Practical Examples

### Terminate a Process by PID

    kill 1234

### Kill All Instances of a Command

    killall sleep

### Send a Specific Signal to a Process

    pkill -SIGHUP nginx

---

## 7. Summary

Linux signals provide a structured method for process control and communication. Key signals like SIGTERM, SIGKILL, SIGINT, and SIGHUP allow administrators to gracefully or forcefully manage processes. Proper understanding of signal usage is critical for system stability, troubleshooting, and cybersecurity, ensuring rogue or misbehaving processes do not compromise the system.