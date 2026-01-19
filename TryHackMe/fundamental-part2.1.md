##  TryHackME (learn the linux fundamental part -2.1)

## overview
In Part 2, we move away from browser-based terminals and start working directly with real remote systems. You’ll learn one of the most essential Linux skills: connecting to and managing remote machines through the terminal. Along the way, this section will also guide you through:
Expanding your command-line abilities by learning how options and parameters change command behavior
Gaining stronger control over the filesystem by practicing practical tasks like duplicating, relocating, and organizing files
Understanding Linux permission models, including how access is restricted and how to check what actions your user account is allowed to perform
Creating and executing simple scripts and programs to see how Linux handles runnable files
Everything here reflects what I studied, tested, and verified myself.

## First: SSH 
## what is SSH
SSH stands for Secure Shell. It is a cryptographic network protocol that lets you securely connect to another computer over a network, usually to control it from the command line.
Before SSH, people used tools like Telnet and rlogin, which sent usernames and passwords in plain text. Anyone sniffing the network could read them. SSH was created to kill that problem decisively.
## Why we use SSH

We use SSH because it provides three critical guarantees:
Confidentiality
All data is ecrypted. Commands, passwords, and file contents cannot be read by attackers on the network.
Authentication
The server proves its identity, and you prove yours (via password or, more commonly, SSH keys).
Integrity
Data cannot be silently modified in transit. If someone tampers with packets, the connection breaks.


Practically, SSH is used for:
Remote server administration
Managing cloud and VPS machines
Secure file transfer (via scp and sftp)
Port forwarding and tunneling (very important in security work)
## Basic SSH syntax

The most common form looks like this:
```bash
ssh username@hostname
ssh root@192.168.1.10
```
## Second : flag and switches
## what is flag 
A flag is an option that enables or disables a feature of a command. It is usually short and prefixed with a single dash (-).   
```bash
#example
ls -l
```
Here:
ls → list files
-l → flag that tells ls to use long (detailed) format

** note ** u need to look for the most used flags and switches and practice using them
## What is a switch

A switch is an option that usually expects a value or is written in a long, descriptive form. It often uses double dashes (--).
```bash
grep --color=auto "root" /etc/passwd
```
Here:
--color is a switch
auto is the value it switches to
another example :
```bash
ssh -p 2222 user@server
```
-p is a switch #note it's switch not a flag cause it's expects a value
2222 is the value (port number)

# Third : Filesystem interaction continued
from the last part we wil continue the learning of commands for interactions with the filesystem

1) touch
touch creates an empty file or updates the timestamps of an existing file (access and modification time).
```bash
touch notes.txt

```
If notes.txt doesn’t exist, it’s created.
If it does exist, its timestamps are refreshed.
This is commonly used to quickly create files or to manipulate timestamps for builds and scripts.

2) mkdir
mkdir creates directories.
```bash
mkdir projects
mkdir -p lab/linux/basics

```
-p tells Linux to create parent directories if they don’t already exist. Without it, the command fails if the path is incomplete and -p here is a flag.

3) cp
cp copies files or directories.
```bash
cp file.txt backup.txt
```
4) mv
mv moves or renames files and directories.
```bash
mv old.txt new.txt

```
5) rm
rm deletes files and directories.
```bash
rm file.txt

```
6) file
file tells you what kind of data a file contains, not what its name suggests.