# 31-etc-passwd-and-shadow.md

# /etc/passwd and /etc/shadow

## Introduction

The `/etc/passwd` and `/etc/shadow` files are core components of Linux user authentication. They store essential account and credential-related information used by the system to identify users and validate login attempts.

These files are critical to Linux authentication because they define user identities, associated privileges, and password verification mechanisms.

From a security perspective, improper access or misconfiguration of these files can lead to unauthorized access, privilege escalation, and credential compromise.

---

## /etc/passwd

### Purpose

The `/etc/passwd` file stores basic user account information required for login and identification. It does not store actual password hashes in modern systems.

### File Format Structure

Each line in `/etc/passwd` contains seven fields separated by colons (`:`).

### Fields Explained

1. Username  
   The login name of the user.

2. Password Placeholder (`x`)  
   Indicates that the encrypted password is stored in `/etc/shadow`.

3. UID (User ID)  
   Numeric identifier used internally by the system.

4. GID (Group ID)  
   Primary group identifier for the user.

5. Comment/Description  
   Optional field for user information (e.g., full name).

6. Home Directory  
   Path to the user’s home directory.

7. Login Shell  
   Default shell executed upon login.

### Example Entry

    student:x:1001:1001:Student User:/home/student:/bin/bash

---

## /etc/shadow

### Purpose

The `/etc/shadow` file stores encrypted password hashes and password policy information.

### Why Password Hashes Are Stored Separately

Historically, password hashes were stored in `/etc/passwd`, which is readable by all users. To enhance security, hashes were moved to `/etc/shadow`, which has restricted access.

### Restricted Permissions

Only privileged users (typically root) can read `/etc/shadow`, protecting password hashes from unauthorized access.

### Key Fields Explained

Each line in `/etc/shadow` contains fields separated by colons.

1. Username  
   Corresponds to the username in `/etc/passwd`.

2. Password Hash  
   Encrypted password string. Special values may indicate locked or disabled accounts.

3. Last Password Change  
   Number of days since January 1, 1970, when the password was last changed.

4. Password Aging Settings  
   Includes minimum days between changes, maximum validity period, warning period, and account expiration parameters.

### Example Entry

    student:$6$randomsalt$encryptedhashvalue:19500:0:99999:7:::

---

## File Permissions and Protection

### Typical Permissions for /etc/passwd

    -rw-r--r--

Readable by all users because system processes require access to account information.

### Typical Permissions for /etc/shadow

    -rw-------

Readable only by root to protect password hashes.

### Why Shadow Must Be Restricted

If password hashes are exposed, attackers can attempt offline brute-force or dictionary attacks to recover passwords.

---

## Security Implications

### Password Hash Exposure Risks

Access to `/etc/shadow` enables attackers to extract hashes for offline cracking attempts, potentially leading to account compromise.

### Privilege Escalation via Misconfiguration

If `/etc/passwd` or `/etc/shadow` permissions are misconfigured, attackers may modify user IDs, change shells, or inject unauthorized accounts.

### Detecting Suspicious User Entries

Unusual UIDs (especially UID 0), unexpected login shells, or unfamiliar usernames may indicate unauthorized account creation.

---

## Summary

The `/etc/passwd` and `/etc/shadow` files define user identities and authentication mechanisms in Linux. `/etc/passwd` stores public account information, while `/etc/shadow` securely stores password hashes and aging policies. Proper permission management and regular auditing of these files are essential to maintaining system security and preventing credential compromise.