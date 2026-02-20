# 21-chmod-deep-dive.md

## Introduction

### What chmod is

`chmod` (change mode) is a Linux command used to modify file and directory permissions. It controls access rights by defining who can read, write, or execute a file.

### Why modifying permissions must be done carefully

Permission changes directly affect system accessibility and security. Incorrect configurations may expose sensitive data, allow unauthorized modifications, or break application functionality.

### Security relevance

In Linux systems, permissions enforce access control. Proper use of `chmod` prevents unauthorized access, limits privilege abuse, and protects critical system files.

---

## Understanding chmod Syntax

### Basic structure

    chmod [options] mode file

### Components Explained

- `chmod` – Command to modify permissions.
- `[options]` – Optional flags (e.g., `-R` for recursive changes).
- `mode` – Permission changes defined in symbolic or numeric format.
- `file` – Target file or directory.

---

## Symbolic Mode

Symbolic mode modifies permissions using characters to represent users and operations.

### User Classes

- `u` – Owner (user)
- `g` – Group
- `o` – Others
- `a` – All (user, group, others)

### Operators

- `+` – Add permission
- `-` – Remove permission
- `=` – Set exact permission

### Multiple Modifications in One Command

Multiple changes can be applied simultaneously by separating them with commas.

### Practical Examples

Add execute permission for the owner:

    chmod u+x script.sh

Remove write permission from group:

    chmod g-w file.txt

Set read-only for others:

    chmod o=r file.txt

Apply multiple changes:

    chmod u+rwx,g+rx,o-r file.sh

---

## Numeric (Octal) Mode

Numeric mode uses octal values based on binary representation of permissions.

### Binary to Octal Conversion

Each permission has a binary value:

- Read (r) = 4 (100)
- Write (w) = 2 (010)
- Execute (x) = 1 (001)

Permissions are summed per user category:

- 7 = 4 + 2 + 1 = rwx
- 6 = 4 + 2 = rw-
- 5 = 4 + 1 = r-x
- 4 = 4 = r--

The three digits represent:

- First digit – Owner
- Second digit – Group
- Third digit – Others

### Common Examples

755:
- Owner: rwx (7)
- Group: r-x (5)
- Others: r-x (5)

644:
- Owner: rw- (6)
- Group: r-- (4)
- Others: r-- (4)

700:
- Owner: rwx (7)
- Group: --- (0)
- Others: --- (0)

### Example Commands

Set 755 permissions:

    chmod 755 script.sh

Set 644 permissions:

    chmod 644 document.txt

Set 700 permissions:

    chmod 700 private.sh

---

## Recursive Permission Changes

### -R Option

The `-R` option applies permission changes recursively to all files and subdirectories within a directory.

### Risks of Recursive Changes

- May unintentionally modify system-critical files.
- Can expose sensitive files if incorrect permissions are applied.
- Difficult to revert in large directory structures.

### Example Usage

Apply 755 permissions recursively:

    chmod -R 755 project_directory

Remove write permissions for others recursively:

    chmod -R o-w shared_folder

---

## Common Mistakes and Risks

### Setting 777 Permissions

`chmod 777` grants full read, write, and execute permissions to everyone. This removes all access restrictions and poses significant security risks.

### Making Sensitive Files World-Writable

Configuration files, scripts, and system files should never be writable by others. World-writable files allow unauthorized modification and potential compromise.

### Breaking System Functionality

Removing execute permissions from scripts or binaries may prevent programs from running. Restricting read access to required configuration files can cause application failure.

---

## Security Implications

### Privilege Escalation Through Misconfigured Permissions

If critical files are writable by non-privileged users, attackers may modify them to execute malicious code with elevated privileges.

### Writable Configuration Files

Improperly secured configuration files can be altered to change system behavior, redirect services, or insert backdoors.

### Executable Malicious Scripts

Granting execute permission to untrusted or user-modified scripts increases the risk of running malicious code.

---

## Summary

The `chmod` command controls file and directory permissions in Linux systems. It supports symbolic and numeric modes for flexible permission management. Proper configuration is essential to maintaining system security, preventing unauthorized access, and reducing the risk of privilege escalation. Careful and precise permission management is a fundamental component of Linux security administration.