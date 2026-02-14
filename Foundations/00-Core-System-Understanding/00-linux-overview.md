# Linux Overview

This document marks the beginning of my structured journey into Linux fundamentals as part of my cybersecurity learning path. Before diving into commands and tools, I need to understand what Linux actually is, how it works, and why it is so critical in cybersecurity and SOC environments.

---

## What is Linux?

### Definition of Linux

Linux is an operating system built around the Linux kernel. It manages hardware resources, runs applications, handles processes, and controls access to the system.

When I use a Linux machine, I am interacting with a system that:

- Manages CPU and memory usage  
- Controls storage devices  
- Handles networking  
- Enforces permissions  
- Runs multiple processes securely  

Linux powers servers, cloud infrastructure, embedded devices, enterprise networks, and cybersecurity platforms.

---

### Kernel vs Operating System

One important clarification I learned early:

- The **kernel** is the core component that interacts directly with hardware.
- The **operating system** includes the kernel plus tools, utilities, libraries, and user interfaces.

The Linux kernel handles:

- Process management  
- Memory allocation  
- Device drivers  
- System calls  

A Linux distribution (such as Ubuntu or Debian) includes:

- The Linux kernel  
- Package managers  
- Command-line tools  
- Desktop environments (optional)  

Understanding this distinction is important because in cybersecurity, many exploits target kernel vulnerabilities or misconfigured system services.

---

### Open-Source Philosophy

Linux is open-source. This means:

- Its source code is publicly available.
- Anyone can review, modify, or improve it.
- Security researchers can inspect how it works internally.

This transparency has two major implications:

- Defenders can audit the system.
- Attackers can also study the code.

Open-source culture promotes rapid patching and collaborative security improvement, which is why Linux is widely trusted in enterprise environments.

---

## Why Linux is Important in Cybersecurity

### Dominance in Servers

Most web servers and enterprise servers run Linux. That means:

- Web applications  
- Databases  
- Email servers  
- DNS servers  

are often hosted on Linux systems.

If I want to understand real-world attack surfaces, I must understand Linux.

---

### Use in Cloud Environments

Cloud providers heavily rely on Linux for:

- Virtual machines  
- Containers  
- Orchestration systems  

Modern infrastructure, especially in AWS and other cloud platforms, is largely Linux-based. Security monitoring in the cloud requires strong Linux knowledge.

---

### Penetration Testing Distributions

Many penetration testing environments use Linux-based distributions. These systems are optimized for:

- Network scanning  
- Exploitation  
- Digital forensics  
- Reverse engineering  

This shows that Linux is not just the target of attacks, but also the platform used to perform security assessments.

---

### SOC Analyst Relevance

In a Security Operations Center (SOC), Linux knowledge is essential because:

- Logs are stored on Linux servers.
- Intrusions often target Linux web servers.
- Analysts investigate suspicious processes and services.
- Threat hunting frequently involves analyzing Linux artifacts.

Without understanding Linux file paths, processes, and permissions, log analysis becomes guesswork.

---

## Linux Architecture Basics

To understand Linux from a security perspective, I need a clear mental model of its architecture.

---

### Kernel

The kernel is the core of the system.

It:

- Manages hardware
- Allocates memory
- Controls processes
- Enforces permission checks

Every action performed by a user or application goes through the kernel.

---

### Shell

The shell is the interface between the user and the operating system.

When I type a command like:

    ls

The shell interprets it and sends instructions to the kernel.

The shell is powerful because it allows automation, scripting, and system control. In cybersecurity, attackers and defenders both rely heavily on shell access.

---

### File System

Linux organizes everything into a hierarchical file system.

Even devices and processes are represented as files. This design makes the system consistent and scriptable.

Understanding the file system is critical for:

- Locating logs  
- Identifying persistence mechanisms  
- Investigating malware  

---

### Processes

A process is a running program.

Each process:

- Has a unique Process ID (PID)
- Runs with specific user permissions
- Consumes system resources

In incident response, identifying suspicious processes is a core skill.

---

## Linux File System Structure

Linux follows a structured hierarchy starting from the root directory:

    /

Some key directories I need to understand:

### /

The root directory. Everything in Linux branches from here.

---

### /home

Stores user home directories.

Example:

    /home/username

This is where personal files, configurations, and user data are stored.

In investigations, compromised user accounts often leave traces here.

---

### /etc

Contains configuration files.

Examples include:

- User account definitions
- Service configurations
- Network settings

If an attacker modifies persistence settings, it often happens in /etc.

---

### /var

Stores variable data such as:

- Logs
- Mail queues
- Caches

For SOC analysts, /var/log is especially important for incident detection.

---

### /bin

Contains essential binary executables required for system operation.

Basic commands like:

    ls
    cp
    mv

are typically located here.

---

### /usr

Contains user programs and applications.

It holds installed software and libraries.

---

### /tmp

Temporary storage.

Files here are often deleted automatically. Attackers sometimes use /tmp to stage malicious scripts because it is commonly writable.

---

### Why Structure Matters in Investigations

Knowing where data lives allows me to:

- Locate logs quickly  
- Identify suspicious file placements  
- Detect abnormal binaries  
- Spot privilege escalation attempts  

Without understanding the directory structure, incident response becomes inefficient.

---

## Users and Permissions (High-Level Overview)

Linux is built around multi-user security.

---

### Root User

The root user has full control over the system.

Root can:

- Read any file  
- Modify system configurations  
- Install software  
- Create or delete users  

If an attacker gains root access, the system is fully compromised.

---

### Normal Users

Normal users have limited permissions.

They:

- Can access their own files  
- Cannot modify critical system files  
- Operate within restricted boundaries  

This separation is essential for security.

---

### Basic Permission Model (rwx Overview)

Linux uses a permission model based on:

- r (read)
- w (write)
- x (execute)

Permissions are defined for:

- Owner
- Group
- Others

This model prevents unauthorized access and limits damage if an account is compromised.

Misconfigured permissions are a common cause of privilege escalation.

---

## Why I Need to Master Linux

As someone pursuing cybersecurity and SOC roles, Linux is not optional.

Most:

- Web infrastructure
- Security tools
- Cloud systems
- Monitoring agents

run on Linux.

If I want to:

- Investigate alerts
- Perform threat hunting
- Analyze suspicious processes
- Detect persistence mechanisms

I must understand Linux at a foundational level.

Mastery of Linux turns log entries into meaningful context.

It allows me to understand attacker behavior instead of just memorizing indicators.

---

## What I Will Study Next

To build deeper competence, my next areas of focus are:

- File system navigation and command-line fluency  
- File permissions and ownership in detail  
- User and group management  
- Process monitoring and signals  
- Bash fundamentals and input/output redirection  

This overview establishes the foundation.  
Next, I will move into practical Linux file system exploration and command mastery.
