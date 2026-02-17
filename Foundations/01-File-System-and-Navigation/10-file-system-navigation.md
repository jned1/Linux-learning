# 10-file-system-navigation.md

# File System Navigation

## Introduction

File system navigation in Linux refers to the ability to move through directories, locate files, and understand the structure of the filesystem from the command line.

Navigation skills are fundamental for system administration and cybersecurity because almost all tasks—log analysis, configuration review, malware detection, and incident response—require efficient movement across directories. Without strong navigation skills, investigation and troubleshooting become slow and error-prone.

---

# Understanding Paths

## Absolute Paths

An absolute path specifies the complete location of a file or directory starting from the root directory (`/`).

Example:

    /var/log/syslog
    /home/user/Documents/report.txt

Absolute paths are unambiguous and do not depend on the current working directory.

---

## Relative Paths

A relative path specifies the location of a file or directory relative to the current working directory.

Example:

    cd Documents
    cd ../Downloads

Relative paths depend on the directory where the user is currently located.

---

## The Root Directory (/)

The root directory (`/`) is the top-level directory of the Linux filesystem. All other directories branch from this location.

Every absolute path begins with `/`.

---

## Current Working Directory

The current working directory (CWD) is the directory in which the user is currently operating.

Commands executed without absolute paths reference files relative to the current working directory.

---

# Essential Navigation Commands

## pwd

**Purpose:**  
Displays the current working directory.

**Basic Syntax:**  

    pwd

**Example Usage:**  

    pwd

**Importance in Investigations:**  
Confirms the analyst’s location within the filesystem to avoid modifying or analyzing the wrong directory.

---

## ls

**Purpose:**  
Lists directory contents.

**Basic Syntax:**  

    ls [options] [directory]

**Example Usage:**  

    ls
    ls -l
    ls -la /var/log

**Importance in Investigations:**  
Allows analysts to inspect file names, permissions, ownership, and timestamps when examining suspicious directories.

---

## cd

**Purpose:**  
Changes the current working directory.

**Basic Syntax:**  

    cd [directory]

**Example Usage:**  

    cd /var/log
    cd ..
    cd ~

**Importance in Investigations:**  
Enables rapid movement between directories during log review or system inspection.

---

## tree (if installed)

**Purpose:**  
Displays directory contents in a hierarchical tree format.

**Basic Syntax:**  

    tree [directory]

**Example Usage:**  

    tree /etc
    tree -L 2 /var

**Importance in Investigations:**  
Provides a structured overview of directory layouts, helping identify unusual nested directories or suspicious file placement.

---

# Special Directory Symbols

## . (Current Directory)

Represents the current working directory.

Example:

    cd .

Used in scripting and command execution contexts.

---

## .. (Parent Directory)

Represents the parent directory of the current location.

Example:

    cd ..

Allows movement upward in the directory hierarchy.

---

## ~ (Home Directory)

Represents the current user’s home directory.

Example:

    cd ~

Provides quick access to user-specific files.

---

## - (Previous Directory)

Represents the previous working directory.

Example:

    cd -

Useful for switching quickly between two directories during analysis.

---

# Viewing Hidden Files

## Hidden Files

Files that begin with a dot (`.`) are hidden by default in directory listings.

Examples:

    .bashrc
    .profile

Hidden files typically store configuration settings.

---

## ls -a Usage

To view hidden files:

    ls -a
    ls -la

The `-a` option displays all files, including hidden ones. The `-l` option shows detailed information.

---

## Why Hidden Files Matter in Security Investigations

Attackers often store malicious scripts or persistence mechanisms in hidden files within user directories or temporary locations.

Reviewing hidden files can reveal:
- Unauthorized configuration changes
- Suspicious startup scripts
- Concealed payloads

Failure to inspect hidden files may result in missed indicators of compromise.

---

# Practical Security Relevance

## Navigating Logs

Security investigations frequently require reviewing logs in directories such as:

    /var/log

Efficient navigation allows rapid access to authentication logs, system logs, and application logs.

---

## Checking User Directories

User home directories may contain:
- Unauthorized SSH keys
- Suspicious scripts
- Unexpected executable files

Navigating to:

    /home/username

Is often part of privilege escalation or persistence analysis.

---

## Identifying Suspicious Files

By combining navigation with listing commands, analysts can identify:
- Unexpected executable files
- Files with unusual permissions
- Recently modified files in sensitive directories

Navigation skills enable systematic examination of the filesystem during incident response.

---

# Summary

File system navigation in Linux involves understanding directory structure, path types, and essential movement commands. Mastery of commands such as `pwd`, `ls`, `cd`, and `tree`, along with knowledge of path symbols and hidden files, forms the foundation for effective system administration and cybersecurity investigations.

Before advancing to topics such as permissions, process management, or service analysis, strong navigation skills are essential for accurate, efficient, and controlled interaction with the Linux filesystem.
