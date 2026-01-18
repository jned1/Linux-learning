# Bandit Level 3

## Goal
To find the password stored at hidden file named inside inhere directory 

## What they are the hidden files:
Files/directories starting with a dot (.) like .bashrc, .ssh/

## Why We Use Them:
Organization - Hide config files to avoid clutter
Safety - Prevent accidental deletion/modification
Privacy - Hide sensitive data (tokens, history)
System - Store user/application preferences
## To View:
ls -a        # Show ALL including hidden
ls -la 

## Commands used
```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220 #using the password u found last level
cd inhere
ls -al 
cat .iamhere
