## Bandit17
### Goal
There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

### Theory
The diff command prints the difference between two files.

Solution
Find the one line that is different between two files.
```bash
bandit17@bandit:~$ diff passwords.old passwords.new 
42c42
< w0Yfolrc5bwjS4qw5mq1nnQi6mF03bii
---
> kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd
```
So since I wrote ‘passwords.new’ in second place, the new password is also printed in the second part.