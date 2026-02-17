# 11-file-types.md

# Linux File Types

## Introduction

In Linux, almost everything is treated as a file. Regular data, directories, hardware devices, and even inter-process communication mechanisms are represented within the filesystem.

Understanding Linux file types is essential for system administration and cybersecurity because different file types behave differently, have distinct permission models, and may introduce unique security risks.

---

# Identifying File Types

File types can be identified using the `ls -l` command.

    ls -l

The first character of the permission string indicates the file type.

Example output:

    -rw-r--r--  1 user user   1200 Jan 10 10:00 file.txt
    drwxr-xr-x  2 user user   4096 Jan 10 10:05 Documents
    lrwxrwxrwx  1 user user      9 Jan 10 10:10 link -> file.txt
    crw-rw----  1 root dialout 188, 0 Jan 10 10:15 ttyUSB0
    brw-rw----  1 root disk     8, 0 Jan 10 10:20 sda
    prw-r--r--  1 user user      0 Jan 10 10:25 pipefile
    srwxr-xr-x  1 user user      0 Jan 10 10:30 socketfile

First character meanings:

- `-` Regular file  
- `d` Directory  
- `l` Symbolic link  
- `c` Character device  
- `b` Block device  
- `p` Named pipe  
- `s` Socket  

---

# Regular Files (-)

## Definition

A regular file stores data such as text, binaries, scripts, or multimedia content.

## Examples

- Text files
- Executable binaries
- Configuration files
- Log files

## Security Relevance

Regular files may contain:
- Sensitive configuration data
- Credentials
- Malicious scripts
- Compromised binaries

Monitoring file integrity and permissions is critical to prevent unauthorized modification or execution.

---

# Directories (d)

## Definition

A directory is a special file that stores references to other files and directories.

## Role in File Organization

Directories organize the filesystem into a hierarchical structure. They enable logical grouping of system files, user data, and applications.

## Security Relevance

Directory permissions control access to contained files. Misconfigured directory permissions may allow unauthorized file creation, modification, or deletion.

---

# Symbolic Links (l)

## Definition

A symbolic link (symlink) is a special file that points to another file or directory.

## How They Work

A symbolic link contains a path reference to another file. When accessed, the system follows the link to the target file.

Example:

    ln -s file.txt link.txt

## Security Implications

Symbolic links can be abused in:
- Symlink race condition attacks
- Redirecting legitimate processes to malicious files
- Bypassing access controls if not properly validated

Security monitoring should verify unexpected or suspicious symbolic links, especially in sensitive directories.

---

# Character Devices (c)

## Definition

Character device files represent devices that transfer data one character at a time.

## Examples

- Terminals
- Serial ports
- Input devices

Typically located in:

    /dev/

## Why Device Files Matter

Access to character device files may allow direct interaction with hardware. Improper permissions can expose sensitive system interfaces.

---

# Block Devices (b)

## Definition

Block device files represent devices that transfer data in fixed-size blocks.

## Difference from Character Devices

Block devices support buffered I/O and random access, while character devices operate sequentially without buffering.

## Examples

- Hard drives
- Solid-state drives
- USB storage devices

Example location:

    /dev/sda

Block devices are critical because they represent entire storage media. Unauthorized access may allow data extraction or disk manipulation.

---

# Named Pipes (p)

## Definition

A named pipe (FIFO) is a special file used for inter-process communication (IPC).

## Basic Concept of Inter-Process Communication

Named pipes allow one process to send data to another through the filesystem interface.

Example creation:

    mkfifo mypipe

Named pipes are temporary communication channels and do not store persistent data.

---

# Sockets (s)

## Definition

A socket file represents a communication endpoint between processes.

## Role in Communication Between Processes

Sockets allow processes to communicate locally or over a network using standardized protocols.

Socket files often appear in directories such as:

    /run/
    /var/run/

Sockets enable service communication and client-server interactions.

---

# Why File Types Matter in Cybersecurity

## Detecting Suspicious Symbolic Links

Unexpected symbolic links in system directories may indicate:
- Privilege escalation attempts
- Redirection of system processes
- Persistence mechanisms

---

## Identifying Unusual Device Files

Malicious creation of fake device files or manipulation of device permissions may indicate advanced compromise attempts.

---

## Investigating Persistence Techniques

Attackers may:
- Hide malicious scripts as regular files
- Use symbolic links to redirect execution
- Abuse writable directories for named pipes or sockets

Understanding file types helps differentiate legitimate system files from abnormal artifacts.

---

# Summary

Linux supports multiple file types, including regular files, directories, symbolic links, character devices, block devices, named pipes, and sockets. Each file type has a specific role within the operating system and unique security implications.

Recognizing file types using `ls -l` and understanding their behavior enables effective system monitoring, investigation, and defense against misuse or exploitation.
