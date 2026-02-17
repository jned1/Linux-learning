# 12-hidden-files-and-dotfiles.md

# Hidden Files and Dotfiles

## Introduction

In Linux, hidden files are files that are not displayed by default when listing directory contents. These files are typically used to store configuration data or system-related information.

Dotfiles are hidden files whose names begin with a period (`.`). This naming convention signals the system and user interfaces to hide them from standard directory listings.

Hidden files exist primarily to reduce visual clutter and separate configuration or system data from regular user files.

---

# How Hidden Files Work

## Naming Convention

Any file or directory whose name begins with a period (`.`) is treated as hidden.

Examples:

    .bashrc
    .profile
    .config

The leading dot is the only characteristic that makes the file hidden.

---

## How the System Treats Them

Hidden files behave like regular files in all other respects. They:

- Follow the same permission model
- Can be read, modified, or executed according to permissions
- Are included in backups unless specifically excluded

They are only hidden from default directory listings for convenience.

---

## Not Encrypted or Protected by Default

Hidden files are not encrypted or inherently protected. The hidden attribute does not provide security. Access control is determined solely by file permissions and ownership.

---

# Viewing Hidden Files

## ls -a

The `-a` option displays all files, including hidden ones.

    ls -a

---

## ls -la

The `-l` option provides detailed information, and `-a` includes hidden files.

    ls -la

Example output:

    drwxr-xr-x  3 user user 4096 Jan 10 10:00 .
    drwxr-xr-x 20 user user 4096 Jan 10 09:50 ..
    -rw-r--r--  1 user user  220 Jan 10 10:00 .bash_logout
    -rw-r--r--  1 user user 3526 Jan 10 10:00 .bashrc
    -rw-r--r--  1 user user  807 Jan 10 10:00 .profile
    drwx------  2 user user 4096 Jan 10 10:05 .ssh

The `.` entry represents the current directory, and `..` represents the parent directory.

---

# Common Dotfiles

## .bashrc

Stores configuration for the Bash shell, including environment variables, aliases, and custom commands executed when a new shell session starts.

---

## .bash_history

Stores the command history of a user’s shell sessions. This file records previously executed commands.

---

## .profile

Contains login shell configuration settings. It is executed when a user logs into the system.

---

## .ssh Directory

Stores SSH-related data, including:

- Private keys
- Public keys
- Authorized keys
- SSH configuration files

The `.ssh` directory typically has strict permissions to prevent unauthorized access.

---

# Security Implications

## Storing SSH Keys

Private SSH keys stored in `.ssh` directories provide authentication access. Improper permissions may allow attackers to copy keys and gain remote access.

---

## Persistence Techniques

Attackers may modify:

- `.bashrc`
- `.profile`

To automatically execute malicious commands whenever a user logs in or starts a shell session.

---

## Hiding Malicious Scripts

Malware or unauthorized scripts may be stored as hidden files in user home directories or temporary directories to avoid detection during casual inspection.

Example:

    .malicious_script.sh

---

## Reviewing User History Files

The `.bash_history` file may reveal:

- Suspicious commands
- Privilege escalation attempts
- Data exfiltration activity

However, attackers may delete or manipulate history files to conceal activity.

---

# Best Practices

## Monitoring User Home Directories

Regularly inspect user home directories for:

- Newly created hidden files
- Unexpected modifications
- Suspicious scripts

---

## Checking Unexpected Dotfiles

Files with unusual names, unexpected timestamps, or incorrect ownership should be investigated.

---

## Reviewing Permissions

Sensitive dotfiles such as:

    ~/.ssh

Should have restricted permissions. For example, private keys should not be world-readable.

---

# Summary

Hidden files and dotfiles in Linux are files whose names begin with a period, causing them to be excluded from default directory listings. They are primarily used for configuration and system-related data but are not inherently protected.

Understanding how hidden files work, how to view them, and how they are commonly used is essential for effective system administration and cybersecurity investigations. Hidden files are frequent targets for persistence techniques and unauthorized modifications, making them a critical area of inspection during security analysis.
