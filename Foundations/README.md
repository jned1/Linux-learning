# Linux Fundamentals

This folder documents my Linux foundation as part of my cybersecurity learning journey.

The goal of this section is not just to memorize commands, but to understand:

- How Linux systems work internally  
- Why certain design decisions exist  
- How misconfigurations create security risks  
- How attackers and defenders both interact with Linux  

This is my structured knowledge base for mastering Linux from the ground up.

---

##  Objective

To build strong Linux fundamentals that support:

- System administration skills  
- Capture The Flag challenges  
- Privilege escalation understanding  
- Security auditing  
- Real-world cybersecurity work  

Linux is the backbone of modern infrastructure. Mastering it is non-negotiable.

---

## 📂 Structure of This Folder

Each file focuses on one core area of Linux fundamentals.

### 1️ File System & Navigation
Covers:
- Directory structure (/home, /etc, /var, /usr, etc.)
- Absolute vs relative paths
- File types
- Hidden files

Why it matters:
Understanding the file system is critical for enumeration, troubleshooting, and privilege escalation.

---

### 2️ File Permissions & Ownership
Covers:
- rwx permissions
- chmod (change mode)
- chown (change owner)
- chgrp (change group)
- Numeric vs symbolic permissions
- SUID, SGID, sticky bit

Why it matters:
Misconfigured permissions are one of the most common security weaknesses in Linux systems.

---

### 3️ Users & Groups
Covers:
- /etc/passwd
- /etc/shadow
- /etc/group
- User IDs (UID)
- Group IDs (GID)
- Authentication vs authorization

Why it matters:
User management directly affects system access control and privilege boundaries.

---

### 4️ Process Management
Covers:
- ps (process status)
- top / htop
- kill
- Background jobs
- Process IDs (PID)
- Daemons

Why it matters:
Processes represent running programs. Understanding them is essential for monitoring, defense, and exploitation.

---

### 5️ Networking Basics
Covers:
- IP addressing basics
- Open ports
- ssh
- curl
- netstat / ss

Why it matters:
Every Linux system communicates over networks. Misconfigured services expose attack surfaces.

---

###  6 Bash & Shell Fundamentals
Covers:
- Environment variables
- $PATH
- Input/output redirection
- Pipes
- Command chaining
- Aliases

Why it matters:
The shell is the primary interface for both administrators and attackers.

---

### 7️ Searching & Text Processing
Covers:
- grep
- find
- awk
- sed
- sort
- uniq
- wc

Why it matters:
Logs and system data are large. Efficient searching is critical for investigation and analysis.

---

###  System Logs & Monitoring
Covers:
- /var/log
- journalctl
- dmesg
- Authentication logs

Why it matters:
Logs are the foundation of incident response and forensic analysis.

---

## Security Perspective

For each topic, I focus on:

- How it works
- Why it exists
- How it can be misconfigured
- How it can be abused
- How to secure it properly

Linux fundamentals are security fundamentals.

---

##  Learning Philosophy

This repository reflects:

- Practical experimentation  
- Hands-on command usage  
- Mistakes and lessons learned  
- Security-oriented thinking  

The goal is mastery, not memorization.

---

##  Long-Term Vision

By mastering these fundamentals, I am building a foundation for:

- Privilege escalation techniques  
- System hardening  
- Malware analysis  
- Penetration testing  
- Red team and blue team operations  

Strong fundamentals turn complex attacks into understandable mechanics.

---

Linux is not just an operating system — it is an ecosystem.  
Understanding it deeply is a competitive advantage in cybersecurity.
