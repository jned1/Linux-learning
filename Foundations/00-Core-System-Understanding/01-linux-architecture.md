# 01-linux-architecture.md

# Linux Architecture

## What is Operating System Architecture?

### Define Operating System Architecture

Operating system architecture refers to the structural design of an operating system (OS). It defines how hardware resources (CPU, memory, storage, network interfaces) interact with software components such as applications and system services.

In Linux, the architecture follows a **monolithic kernel model**, meaning the core operating system functions run within a single large kernel operating in privileged mode.

Understanding this structure is essential for cybersecurity because attacks often exploit weaknesses at specific architectural layers.

---

### User Space vs Kernel Space

Linux operates in two primary execution modes:

**Kernel Space**
- Runs with full hardware privileges.
- Has unrestricted access to memory and system resources.
- Executes core OS functions.

**User Space**
- Where applications run.
- Limited access to hardware.
- Must request services from the kernel.

This separation is enforced by the CPU using privilege levels (often called "rings").

---

### Why This Separation Matters for Security

This boundary is one of the most important security controls in Linux.

If an attacker compromises an application in user space:
- They do not automatically gain full system control.
- They must escalate privileges to reach kernel space.

Most exploitation techniques (e.g., privilege escalation) aim to cross this boundary. Understanding where a process runs helps in analyzing impact during incident response.

---

# The Linux Kernel

## What the Kernel Is

The kernel is the core component of the Linux operating system. It acts as an intermediary between hardware and software.

It is always running in memory and controls everything from process scheduling to device communication.

---

## Responsibilities of the Kernel

### Process Management

The kernel:
- Creates and terminates processes
- Schedules CPU time
- Manages process states (running, sleeping, stopped)

Security relevance:
Compromised processes can spawn malicious child processes. Monitoring process trees is critical in SOC investigations.

---

### Memory Management

The kernel:
- Allocates and deallocates memory
- Manages virtual memory
- Isolates processes from each other

Security relevance:
Memory corruption vulnerabilities (buffer overflows, use-after-free) often target kernel memory structures.

---

### Device Drivers

Device drivers allow the kernel to communicate with hardware such as:
- Disk drives
- Network cards
- USB devices

Security relevance:
Malicious drivers or vulnerable drivers can lead to kernel-level compromise.

---

### File Systems

The kernel:
- Manages file storage
- Controls permissions
- Enforces access control

Security relevance:
File permission misconfigurations are common attack vectors.

---

### Networking

The kernel:
- Handles TCP/IP stack
- Manages sockets
- Controls firewall rules (via subsystems)

Security relevance:
Network-based attacks interact directly with kernel networking components.

---

## Why Kernel Security Is Critical

If the kernel is compromised:
- The attacker gains complete system control.
- Logging and monitoring mechanisms can be bypassed.
- Persistence mechanisms become difficult to detect.

Kernel-level attacks are rare compared to user-space attacks, but they are far more dangerous.

---

# User Space

## What Runs in User Space

User space contains:

- Applications
- User programs
- Background services
- System utilities

---

### Applications

Examples:
- Web browsers
- SSH clients
- Database servers

These programs rely on the kernel to perform privileged operations.

---

### System Libraries

Libraries (such as standard C libraries) provide reusable functions that applications depend on.

Security relevance:
If a shared library is compromised, every application using it may be affected.

---

## Why Most Attacks Start in User Space

Attackers typically exploit:
- Vulnerable applications
- Misconfigured services
- Weak credentials

User space is accessible and exposed to users and networks. From there, attackers attempt:
- Privilege escalation
- Lateral movement
- Persistence

---

# The Shell

## What the Shell Is

The shell is a command-line interface that allows users to interact with the operating system.

It acts as a bridge between user commands and the kernel.

---

## How It Interacts with the Kernel

When a user types a command:
1. The shell parses the command.
2. It creates a process.
3. That process makes system calls to the kernel.

Example:

    ls -la

This command triggers system calls to read directory contents.

---

## Examples of Shells

- bash (Bourne Again Shell)
- sh (Bourne Shell)
- zsh (Z Shell)

---

## Why Understanding the Shell Is Important for SOC Analysts

Many attacks involve:
- Reverse shells
- Web shells
- Command injection

SOC analysts must understand:
- How commands are executed
- What suspicious command patterns look like
- How to interpret shell history and logs

---

# System Calls

## What System Calls Are

System calls are controlled entry points into the kernel.

They allow user-space programs to request services such as:
- Opening files
- Creating processes
- Sending network packets

---

## How Programs Communicate with the Kernel

Applications cannot directly access hardware. Instead, they use system calls like:

    open()
    read()
    write()
    execve()

These calls transition execution from user space to kernel space.

---

## Why Monitoring System Calls Is Important in Security

Malware ultimately interacts with the system through system calls.

Security tools may monitor:
- Process execution (execve)
- File access (open)
- Network activity (connect)

Abnormal system call patterns can indicate malicious behavior.

---

# Daemons and Services

## What Daemons Are

Daemons are background processes that run without direct user interaction.

They typically start during boot and provide system or network services.

---

## Examples

- sshd (SSH server)
- cron (task scheduler)
- systemd (init system and service manager)

---

## Why Services Are Common Attack Targets

Services:
- Often run with elevated privileges
- Listen on network ports
- Operate continuously

If misconfigured or vulnerable, they provide attackers with persistent access points.

---

# Boot Process (High-Level Overview)

## BIOS / UEFI

The system firmware initializes hardware and prepares to load the operating system.

---

## Bootloader

The bootloader loads the Linux kernel into memory.

---

## Kernel Loading

The kernel:
- Initializes hardware
- Mounts the root filesystem
- Starts essential subsystems

---

## Init System (systemd Overview)

The init system is the first user-space process (PID 1).

systemd:
- Starts services
- Manages dependencies
- Handles logging and service supervision

Security relevance:
Compromise at this stage can grant full persistence and control.

---

# Why Linux Architecture Matters in Cybersecurity

## Privilege Escalation Relevance

Understanding:
- User vs kernel boundaries
- SUID binaries
- Process permissions

Helps identify escalation vectors.

---

## Log Investigation

Knowing where processes run and how services start:
- Improves log correlation
- Helps identify abnormal parent-child relationships

---

## Malware Behavior

Malware must:
- Execute in user space
- Make system calls
- Interact with files and networks

Architecture knowledge clarifies how malicious code operates internally.

---

## Incident Response Impact

When responding to incidents:
- Kernel compromise changes containment strategy.
- User-space compromise may allow recovery without full rebuild.
- Understanding services helps isolate infected components.

---

# Personal Reflection

Studying Linux architecture helped me understand that security is not only about tools but about system design.
