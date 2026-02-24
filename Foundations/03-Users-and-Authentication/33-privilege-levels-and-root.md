# 33-privilege-levels-and-root.md

# Privilege Levels and Root

## Introduction

Privilege levels in Linux define the scope of actions a user or process is permitted to perform. These levels control access to files, system configurations, hardware resources, and administrative functions.

Privilege separation exists to reduce risk by limiting user capabilities to only what is necessary. This separation prevents accidental system damage and restricts the impact of compromised accounts.

From a security standpoint, controlled privilege boundaries are fundamental to maintaining system integrity and preventing unauthorized escalation.

---

## Normal Users

### Definition

Normal users are standard accounts created for human interaction with the system. They operate within restricted permission boundaries.

### Default Capabilities

Normal users can:

- Access their own files
- Execute permitted programs
- Modify data within authorized directories

### Restrictions

Normal users cannot:

- Modify system-critical files
- Install system-wide software without elevated privileges
- Access other users’ protected data

### UID Range Overview

- UID 0: Root user
- UID 1–999: System or service accounts (distribution dependent)
- UID 1000 and above: Regular user accounts

The UID determines internal identity and privilege evaluation by the kernel.

---

## Root User (UID 0)

### Definition

The root user is the superuser account in Linux with UID 0.

### Full System Control

Root can:

- Read, write, and execute any file
- Modify system configurations
- Manage users and groups
- Install and remove software
- Control services and processes

### Why Root Bypasses Permission Checks

The Linux kernel treats UID 0 as privileged and bypasses standard file permission enforcement. This allows root unrestricted system access.

### Risks of Operating as Root

- Accidental deletion or modification of critical files
- Increased impact if malicious code is executed
- Expanded attack surface if credentials are compromised

Operating continuously as root reduces system safety.

---

## Switching Privileges

### su Command

The `su` (substitute user) command switches to another user account, commonly root.

Basic usage:

    su

Switch to a specific user:

    su username

### sudo Command

The `sudo` (superuser do) command executes a single command with elevated privileges.

Basic usage:

    sudo command

Open a root shell:

    sudo -i

### Difference Between su and sudo

- `su` switches the entire session to another user.
- `sudo` grants temporary elevated privileges for specific commands.

`sudo` provides better auditing and controlled privilege delegation.

---

## Principle of Least Privilege

### Definition

The principle of least privilege states that users and processes should have only the minimum permissions required to perform their tasks.

### Why It Is Critical in Security

Limiting privileges reduces the potential damage caused by errors, vulnerabilities, or compromised accounts.

### Real-World Relevance in System Administration

Administrators commonly use `sudo` for controlled elevation instead of logging in directly as root. Services are configured to run under restricted accounts rather than with full superuser privileges.

---

## Risks and Misuse

### Running Services as Root

Services running as root increase the severity of exploitation. A vulnerability in such a service may grant full system control.

### Unrestricted sudo Access

Granting broad sudo permissions to users undermines privilege separation and increases security risk.

### Privilege Escalation Impact

If an attacker gains root access, they can:

- Modify system binaries
- Install persistent backdoors
- Access all user data
- Disable security controls

Root compromise typically results in total system compromise.

---

## Summary

Linux enforces a privilege hierarchy centered on normal users and the root account (UID 0). Normal users operate under restricted permissions, while root has unrestricted control and bypasses standard checks. Controlled privilege elevation through tools like `sudo`, combined with adherence to the principle of least privilege, is essential for maintaining secure and stable Linux systems.