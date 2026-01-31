## Bandit level 20 

### Goal
There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

### Theory
Netcat or nc was introduced in level 15. To create a server on localhost, the -l flag (which means listening) is needed. To specify a port, the -p flag is needed. To create a “onetime server”, a server that sends one message and then disconnects, we can use the pipe (| - level 6) and echo to input the message.

If a command needs to be run, but you don’t need to interact with it for a while and want to keep using the same terminal with other commands while the command is executing, you can use &. The ampersand will send the command in the background. This is a part of the Linux process management. Specifically, if you want to learn more about this, also look into the jobs command, it shows processes/commands/jobs running in the background and foreground.

Setuid binaries were introduced and explained in the previous level.

### Solution
Using ’netcat’, we can create a connection in server mode - which listens for inbound connection. To have netcat send the password, I use echo and pipe it into netcat. The -n flag is to prevent newline characters in the input. Lastly, we let the process run in the background with &.
```bash
bandit20@bandit:~$ echo -n 'GbKksEFF4yrVs6il55v6gwY5aVje5f0j' | nc -l -p 1234 &
[1] 24661
```
Running the setuid binary with port 1234 means it will connect to our netcat server, receive the password inputted through echo and sends back the next password.
```bash
bandit20@bandit:~$ ./suconnect 1234
Read: GbKksEFF4yrVs6il55v6gwY5aVje5f0j
Password matches, sending next password
gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
[1]+  Done                    
```