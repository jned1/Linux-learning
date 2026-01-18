# Bandit Level 0

## Goal
Connect to the Bandit server using SSH and read the password stored in a file.


## What Is SSH 
SSH is a cryptographic network protocol for operating network services securely over unsecured networks. It provides:

    -Secure remote login (replacing insecure Telnet)

    -Secure file transfer

    -Secure command execution

    -Encrypted communication between machines
    
## What I learned

-How SSH connects to a remote Linux system
-Linux is case-sensitive
-Listing files before accessing them prevents mistakes

## Commands used
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220 #first thing is the username then @ IP address or DNS then portal
ls -al ## list the component in the current directory 
cat readme # see the containt of the file (password) 
