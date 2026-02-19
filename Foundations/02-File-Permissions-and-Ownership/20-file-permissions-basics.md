# 20-file-permissions-basics.md

# File Permissions Basics

## Introduction

File permissions in Linux define who can read, write, or execute a file or directory. They are a core component of the Linux security model and control access to system resources.

Permissions are critical in multi-user systems because multiple users share the same operating system. Without proper permission controls, users could access, modify, or delete each other’s files or sensitive system data.

From a cybersecurity perspective, misconfigured permissions can lead to unauthorized access, data exposure, or privilege escalation.

---

# Viewing File Permissions

File permissions can be viewed using:

    ls -l

Example output:

    -rwxr-xr-- 1 user group 4096 Jan 10 10:00 script.sh
    drwxr-x--- 2 user group 4096 Jan 10 10:05 Documents

## Breaking Down the Permission String

Example:

    -rwxr-xr--

The permission string consists of:

1. File type indicator (first character)
2. Owner permissions (next three characters)
3. Group permissions (next three characters)
4. Others permissions (last three characters)

## File Type Indicator

The first character indicates the file type:

- `-` Regular file  
- `d` Directory  
- `l` Symbolic link  

The remaining nine characters represent permissions.

---

# Permission Categories

## Owner (User)

The owner is typically the user who created the file. The first set of three permission characters applies to the owner.

---

## Group

The group represents a collection of users. The second set of three permission characters applies to users who belong to that group.

---

## Others

Others refers to all users who are neither the owner nor part of the file’s group. The last set of three permission characters applies to them.

---

## How Access Is Evaluated

When a user attempts to access a file, Linux evaluates permissions in the following order:

1. If the user is the owner, owner permissions apply.
2. If not the owner but part of the group, group permissions apply.
3. Otherwise, others permissions apply.

Only one category is applied per access check.

---

# Permission Types

## Read (r)

For files:
- Allows viewing file contents.

For directories:
- Allows listing directory contents.

---

## Write (w)

For files:
- Allows modifying or deleting file content.

For directories:
- Allows creating, deleting, or renaming files within the directory.

---

## Execute (x)

For files:
- Allows executing the file as a program or script.

For directories:
- Allows entering the directory and accessing files within it.

---

# Numeric (Octal) Representation

Permissions can also be represented numerically using octal values.

Each permission has a numeric value:

- Read (r) = 4  
- Write (w) = 2  
- Execute (x) = 1  

Values are added together for each category.

Examples:

- rwx = 4 + 2 + 1 = 7  
- rw- = 4 + 2 = 6  
- r-x = 4 + 1 = 5  
- r-- = 4  

Common permission sets:

- 755 = rwxr-xr-x  
- 644 = rw-r--r--  
- 700 = rwx------  

Example:

    chmod 755 script.sh

This sets full permissions for the owner and read-execute permissions for group and others.

---

# Changing Permissions

## Basic chmod Usage

The `chmod` command modifies file permissions.

Numeric mode example:

    chmod 644 file.txt

---

## Symbolic Mode

Symbolic mode uses letters to represent categories:

- u = user (owner)
- g = group
- o = others
- a = all

Operators:

- + add permission
- - remove permission
- = set exact permission

Example commands:

    chmod u+x script.sh
    chmod g-w file.txt
    chmod o-r file.txt
    chmod u=rwx,g=rx,o= file.txt

Symbolic mode allows precise modification without recalculating numeric values.

---

# Why File Permissions Matter in Cybersecurity

## Preventing Unauthorized Access

Proper permissions prevent unauthorized users from reading sensitive files such as configuration files, private keys, or system logs.

---

## Identifying Misconfigurations

Files or directories that are world-writable (e.g., permission 777) may expose the system to tampering or data loss.

---

## Privilege Escalation Risks

Improper permissions on executable files may allow attackers to:

- Modify scripts executed by privileged users
- Replace system binaries
- Inject malicious code

---

## Writable Sensitive Files

If sensitive files such as:

- System configuration files
- Scheduled task scripts
- Authentication files

Are writable by non-privileged users, attackers may gain elevated access.

---

# Summary

Linux file permissions control access to files and directories through a structured model based on owner, group, and others. Permissions define read, write, and execute rights and can be represented symbolically or numerically.

Understanding how to view, interpret, and modify permissions is essential for maintaining system integrity, preventing unauthorized access, and detecting security misconfigurations in multi-user environments.