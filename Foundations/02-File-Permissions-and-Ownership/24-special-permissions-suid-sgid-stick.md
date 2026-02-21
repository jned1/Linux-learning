# 24-special-permissions-suid-sgid-sticky.md

# Special Permissions: SUID, SGID, Sticky Bit

## Introduction

Special permission bits in Linux extend the standard read, write, and execute permission model. These bits modify how executables and directories behave during access and execution.

They exist to support controlled privilege delegation and shared collaboration environments. However, because they alter normal permission behavior, they are security-sensitive and must be managed carefully.

---

## Understanding the Permission Field

In the output of:

    ls -l

Permissions appear as a 10-character string, for example:

    -rwsr-xr-x

Special bits replace or modify the execute (`x`) position:

- `s` in the user execute position indicates SUID.
- `s` in the group execute position indicates SGID.
- `t` in the others execute position indicates Sticky Bit.

If execute permission is not set, uppercase letters (`S` or `T`) appear instead.

---

## SUID (Set User ID)

### Definition

SUID (Set User ID) is a special permission applied to executable files that allows users to run the file with the file owner's privileges.

### How It Works

When an executable with SUID is run, the process temporarily assumes the effective user ID of the file owner rather than the user executing it.

### Effect When Applied to Executable Files

If owned by root, the program runs with root privileges regardless of who executes it. This is commonly required for system utilities that need elevated access.

### Numeric Representation

4000

### Example of Setting SUID

    chmod 4755 program

The leading `4` enables the SUID bit.

### Security Implications

Improperly configured SUID binaries can enable privilege escalation. If a vulnerable SUID program is exploited, attackers may gain elevated privileges.

---

## SGID (Set Group ID)

### Definition

SGID (Set Group ID) modifies execution and directory behavior based on group ownership.

### Behavior on Executable Files

When applied to an executable, the process runs with the file’s group ID rather than the executing user’s primary group.

### Behavior on Directories

When applied to a directory, newly created files inherit the directory’s group ownership instead of the creator’s primary group. This supports collaborative environments.

### Numeric Representation

2000

### Example of Setting SGID

    chmod 2755 directory_or_program

The leading `2` enables the SGID bit.

### Security Implications

Misconfigured SGID executables may expose group-level privilege escalation risks. Incorrect directory permissions can unintentionally grant broader group access.

---

## Sticky Bit

### Definition

The Sticky Bit restricts file deletion within directories.

### Primarily Used on Directories

It is most commonly applied to shared directories to prevent users from deleting files owned by others.

### Behavior in Shared Directories (e.g., /tmp)

In directories with the Sticky Bit set, users can delete only:

- Files they own
- Files owned by root

Even if write permission exists for all users.

### Numeric Representation

1000

### Example of Setting Sticky Bit

    chmod 1777 shared_directory

The leading `1` enables the Sticky Bit.

### Security Implications

Without the Sticky Bit, users in shared writable directories could delete or rename other users’ files. Proper configuration prevents unauthorized file removal.

---

## Identifying Special Permissions

### Using ls -l

Special bits appear as:

- `rws` (SUID active)
- `rwxr-s` (SGID active)
- `rwxrwxrwt` (Sticky Bit active)

Uppercase letters (`S` or `T`) indicate the special bit is set without execute permission.

### Using find to Locate SUID/SGID Files

Find SUID files:

    find / -perm -4000 2>/dev/null

Find SGID files:

    find / -perm -2000 2>/dev/null

---

## Security Considerations

### Privilege Escalation Risks

SUID and SGID binaries can be leveraged by attackers if vulnerabilities exist within them.

### Auditing SUID Binaries

Regular auditing of SUID and SGID files is essential to ensure only necessary system binaries have these permissions.

### Misconfigured Shared Directories

Directories without the Sticky Bit and with world-write permissions may allow users to interfere with other users’ data.

---

## Summary

SUID, SGID, and Sticky Bit extend the Linux permission model to support controlled privilege execution and collaborative directory management. SUID grants execution with file owner privileges, SGID influences group behavior, and the Sticky Bit protects shared directories from unauthorized file deletion. Because these permissions alter standard access control behavior, they require careful configuration and regular auditing to maintain system security.