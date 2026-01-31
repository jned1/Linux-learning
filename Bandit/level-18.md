## Bandit level 18

### Goal
The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

### Theory
‘.bashrc’ is a file that is run every time a terminal is loaded. This means it is also run when logging in through SSH because this also loads a terminal.

In the walkthrough to Level 0 I have given a short introduction to SSH. Something I have not mentioned is that SSH does not just allows us to log into a machine remotely, but it also allows remote execution of commands by adding the commands after the common SSH expression.

Solution
Instead of logging into the machine with SSH, we execute a command through SSH instead. First, we use ls to make sure the readme file is in the folder then we can use cat to read it.

```bash
$ ssh bandit18@bandit.labs.overthewire.org -p 2220 ls         
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
readme

$ ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme

This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
bandit18@bandit.labs.overthewire.org's password: 
IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x
```