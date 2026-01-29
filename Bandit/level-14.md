## Bandit level 14

### goal
The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

### note:
Localhost is a hostname and its IP address is ‘127.0.0.1’. It is used to access network services on the same device that is running these services.

nc or netcat is a command that allows to read and write data over a network connection. It can be used for TCP and UDP connections. To connect to a service (as client) on a network the command syntax is the following: nc <host> <port>. To create a server that listens to incoming packets, the command looks like this: nc -l <port>.

Solution
First, we need to find the password for bandit14. The previous levels stated that the password is in /etc/bandit_pass/bandit14.
```bash
bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
```
Next, we need to submit the password to port 30000 on localhost. I used nc to connect to localhost port 3000 and write the password.1
```bash
bandit14@bandit:~$ nc localhost 30000
4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e
Correct!
BfMYroe26WYalil77FoDi9qh59eK5xNr
```