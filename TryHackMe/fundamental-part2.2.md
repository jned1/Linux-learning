## TryHackME (learn the linux fundamental part -2.2)
## Overview :
in this file we will continue the second section of part 2.
- file permission 
- important directories
Everything here reflects what I studied, tested, and verified myself.

## What are file permissions in Linux

File permissions define who is allowed to read, write, or execute a file or directory.
They are enforced by the Linux kernel, not by applications, which means they are foundational security controls, not optional features.

Every file and directory in Linux has:
1) an owner
2) a group
3) a set of permissions
## Why we use the permission in linux 
Linux was designed from day one as a multi-user operating system. Multiple users can be logged in at the same time, running programs, accessing files, and sharing a system.

Without permissions:
Any user could read private files
Any program could modify system binaries
Malware would have unrestricted access
Permissions enforce least privilege: each user and process gets only the access it needs.

## Types of permission
The three permission types
Linux permissions are expressed using three basic actions:
1) read (r)
File: view contents
Directory: list contents
2) write (w)
File: modify or delete contents
Directory: create, delete, or rename files inside
3) execute (x)
File: run it as a program or script
Directory: enter it (cd)
## The three permission scopes
Each permission applies to three categories of users:
1) Owner (u) – the user who owns the file

2) Group (g) – users in the file’s group

3) Others (o) – everyone else
Together, permissions look like this:
```bash
-rwxr-xr--
rwxrwxrwx #full access
```

## The differnece bw users  and groups 
## users 
A user is an individual account that can log in, run processes, and own files.
Each user has:
a username
a UID (User ID – a number the kernel actually uses)
a home directory
a default shell
## group

A group is a collection of users.
It exists to make permission management scalable.
Instead of giving permissions to many users one by one, you:
create a group
add users to it
assign permissions to the group
each group has:
a group name
a GID (Group ID)

## some of the most important directory (/etc,/root,/var,/tmp)
## /etc
Contains system-wide configuration files.
Most files here are plain text and control how services and the system behave.
If you are configuring Linux, you are almost always editing something in /etc.
## /root
The home directory of the root (administrator) user.
It stores root’s personal files, scripts, and configuration.
It is separate from /home so the administrator can still work even if user filesystems are unavailable.

## /var
Holds variable data—files that constantly change while the system runs.
This includes logs, caches, databases, and spool files.
When disks suddenly fill up, /var is often the reason.
## /tmp
Used for temporary files created by programs and users.
Contents are usually deleted on reboot.
It is writable by all users but protected to prevent users from deleting each other’s files.
