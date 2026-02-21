# 30-users-and-groups.md

# Users and Groups

## Introduction

Linux is designed as a multi-user operating system where multiple accounts can access and operate on the same system. Users and groups provide a structured method for managing access control, ownership, and resource isolation.

In multi-user environments, proper user and group management ensures separation of privileges, controlled collaboration, and system stability.

From a security perspective, users and groups enforce accountability, limit unauthorized access, and support the principle of least privilege.

---

## User Accounts

### Definition of a User Account

A user account represents an identity within the system. Each account has associated credentials, permissions, and ownership of files and processes.

### UID (User ID) Concept

Each user is assigned a unique numeric identifier called a UID (User ID). The operating system uses the UID internally to determine access rights rather than relying on usernames.

Common UID conventions:

- UID 0: Root user
- UID 1–999: System users (distribution dependent)
- UID 1000 and above: Regular users

### System Users vs Regular Users

System users are created to run services and background processes. They typically do not have login shells.

Regular users are human users who log into the system and perform interactive tasks.

### Root User Overview

The root user has UID 0 and unrestricted access to all system resources. Root bypasses standard permission checks and can modify any file or configuration.

---

## Group Accounts

### Definition of a Group

A group is a collection of users that share common access permissions to files and system resources.

### GID (Group ID) Concept

Each group has a unique numeric identifier called a GID (Group ID). Like UIDs, GIDs are used internally by the system to enforce group-based access control.

### Primary vs Secondary Groups

Primary group:
- Assigned at user creation
- Determines default group ownership of newly created files

Secondary groups:
- Additional groups a user belongs to
- Provide extended access permissions

---

## Key System Files

### /etc/passwd

Stores basic user account information including:

- Username
- UID
- GID
- Home directory
- Default shell

Passwords are not stored in plain text in this file.

### /etc/shadow

Stores encrypted password hashes and password policy information. Access is restricted to privileged users.

### /etc/group

Stores group definitions including:

- Group name
- GID
- List of group members

---

## Managing Users

### useradd

Creates a new user account.

    sudo useradd username

Create a user with home directory:

    sudo useradd -m username

### userdel

Deletes a user account.

    sudo userdel username

Remove user and home directory:

    sudo userdel -r username

### passwd

Sets or changes a user password.

    sudo passwd username

---

## Managing Groups

### groupadd

Creates a new group.

    sudo groupadd groupname

### groupdel

Deletes a group.

    sudo groupdel groupname

### usermod -aG

Adds a user to a secondary group.

    sudo usermod -aG groupname username

The `-a` flag appends the group membership without removing existing groups.

---

## Security Considerations

### Principle of Least Privilege

Users should be granted only the permissions required to perform their tasks. Avoid unnecessary administrative privileges.

### Protecting /etc/shadow

The `/etc/shadow` file must remain readable only by privileged users to prevent password hash exposure.

### Monitoring New User Creation

Unauthorized user accounts may indicate compromise. Regular review of user lists and login activity is recommended.

### Group-Based Privilege Control

Using groups to assign permissions reduces complexity and improves manageability compared to granting permissions to individual users.

---

## Summary

Users and groups form the foundation of access control in Linux systems. Each user is identified by a UID, and each group by a GID. System files such as `/etc/passwd`, `/etc/shadow`, and `/etc/group` store account and credential data. Proper management of users and groups, combined with adherence to the principle of least privilege, is essential for maintaining system security and operational integrity.