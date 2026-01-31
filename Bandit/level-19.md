## Bandit level19

### Goal
To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

### Theory
Linux permissions is a very big topic. Each file has an owner and a group that owns the file. For the user, the group and the rest of the users the permissions can be set separately. It can be chosen if the file is readable, writable or executable. The permissions and owners of a file can be seen using the ls -l command. The third column shows the user, the fourth the group and the first column shows the permissions. The permissions are written the following rwxrwxrwx, the first three letters indicate the user has all permissions (read=r, write=w and execute=x). The next three letters indicate the permission of the group and the last of everyone else. If one of the letters is replaced with -, this means the permission is not granted.

Suid is a special permission. It will replace the x of the user permission. It means the binary will be run as the owner of the binary, not the one executing it. To give a binary suid permissions the following command needs to be used: chmod u+s <filename>.

### sol
First, we check who the owner of the setuid binary is:
```bash
bandit19@bandit:~$ ls -la
total 28
drwxr-xr-x  2 root     root     4096 May  7  2020 .
drwxr-xr-x 41 root     root     4096 May  7  2020 ..
-rwsr-x---  1 bandit20 bandit19 7296 May  7  2020 bandit20-do
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r--r--  1 root     root     3526 May 15  2017 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
```
In this case, the owner is badit20 and the group is bandit19, this with ‘-rwsr-x—’ means the user bandit19 can execute the binary, but the binary is executed as user bandit20.

Executing the binary says it simply executes another command as another user (as already explained, this user is bandit20). This means we can access the bandit20 users password file, which can only be read by the user bandit20.

```bash
bandit19@bandit:~$ ./bandit20-do 
Run a command as another user.
  Example: ./bandit20-do id
bandit19@bandit:~$ ./bandit20-do ls /etc/bandit_pass
bandit0   bandit12  bandit16  bandit2   bandit23  bandit27  bandit30  bandit4  bandit8
bandit1   bandit13  bandit17  bandit20  bandit24  bandit28  bandit31  bandit5  bandit9
bandit10  bandit14  bandit18  bandit21  bandit25  bandit29  bandit32  bandit6
bandit11  bandit15  bandit19  bandit22  bandit26  bandit3   bandit33  bandit7
bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
GbKksEFF4yrVs6il55v6gwY5aVje5f0j
```