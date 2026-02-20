# Numeric vs Symbolic Permissions

## Introduction

Linux file permissions can be modified using two primary methods: numeric (octal) mode and symbolic mode. Both approaches control read, write, and execute permissions for users and groups.

Understanding both methods is essential for effective system administration and security management. Numeric mode offers concise precision, while symbolic mode provides flexibility for incremental changes.

---

## Recap of Permission Structure

### Owner, Group, Others

Linux permissions are divided into three categories:

- Owner (user who owns the file)
- Group (users belonging to the file’s group)
- Others (all other users on the system)

### Read, Write, Execute

Each category can have the following permissions:

- Read (r) – View file contents or list directory contents
- Write (w) – Modify file contents or directory entries
- Execute (x) – Run a file as a program or access a directory

### Permission String Format

Example:

    -rwxr-xr--

Breakdown:

- First character: file type (`-` for regular file)
- Next three: owner permissions (rwx)
- Next three: group permissions (r-x)
- Last three: others permissions (r--)

---

## Numeric (Octal) Mode

### Mapping rwx to Numeric Values

Each permission has a binary-based value:

- Read (r) = 4
- Write (w) = 2
- Execute (x) = 1

### Summing Values

Permissions are calculated by summing values:

- 7 = 4 + 2 + 1 = rwx
- 6 = 4 + 2 = rw-
- 5 = 4 + 1 = r-x
- 4 = 4 = r--

Each digit represents:

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

## Symbolic Mode

### User Identifiers

- u – Owner (user)
- g – Group
- o – Others
- a – All (u, g, and o)

### Operators

- + – Add permission
- - – Remove permission
- = – Set exact permission

### Adding, Removing, and Setting Permissions

Add execute permission for owner:

    chmod u+x script.sh

Remove write permission from group:

    chmod g-w file.txt

Set read-only permission for others:

    chmod o=r file.txt

Apply multiple changes in one command:

    chmod u+rwx,g+rx,o-r file.sh

---

## Key Differences

### Flexibility

Symbolic mode allows incremental changes without affecting other permission bits. Numeric mode replaces the entire permission set at once.

### Precision

Numeric mode is precise and compact, making it suitable for setting exact permission configurations quickly.

### Readability

Symbolic mode is often easier to interpret because it explicitly states which permissions are being modified.

### Use Cases

Numeric mode is efficient for standardized permission sets. Symbolic mode is useful when adjusting specific permissions without altering others.

---

## When to Use Each Method

### Situations Where Numeric Mode Is Preferred

- Applying standard permission templates (e.g., 755 for scripts)
- Writing deployment or automation scripts
- Quickly setting known permission configurations

### Situations Where Symbolic Mode Is Preferred

- Modifying a single permission without changing others
- Adjusting permissions during troubleshooting
- Making controlled incremental security changes

---

## Security Considerations

### Risks of Incorrect Numeric Values

Using incorrect numeric values may unintentionally grant excessive permissions or remove required access.

### Over-Permissive Configurations

Values such as 777 grant full access to all users and significantly weaken system security.

### Maintaining Principle of Least Privilege

Permissions should grant only the minimum access required for functionality. Both numeric and symbolic modes must be used carefully to enforce strict access control.

---

## Summary

Linux permissions can be modified using numeric (octal) or symbolic modes. Numeric mode provides concise and precise full-permission settings, while symbolic mode allows flexible and incremental adjustments. Understanding the differences between these methods is essential for maintaining secure, properly configured Linux systems.