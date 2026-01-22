# Bandit Level 6

## Goal
find the password
The password stored in :
owned by user bandit7
owned by group bandit6
size of the file 33 bytes
located somewhere on the system

### What is ownership in linux
 
#### every file in linux has:

user (owner) → who owns the file
group → which group owns the file
ownership works together with permissions to control access

### Commands used
```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
cat /path/to/file
```
### explenation
ssh bandit6@bandit.labs.overthewire.org
 -p 2220

connect to the bandit server using ssh
use the password from level 5

find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
find /

find → search files recursively
/ → start from root directory

means:
“search the whole filesystem”

-user bandit7

match only files owned by bandit7

-group bandit6

match only files owned by group bandit6

-size 33c

33 → size
c → bytes

means:
“only files that are exactly 33 bytes”

2>/dev/null

2 → standard error
/dev/null → discard output

used to hide permission denied errors

cat the file

after finding the correct file path:

cat /path/to/file


this prints the password for Bandit Level 7

### what you learned

files can be found using ownership

size filtering is precise and reliable

searching from / needs error redirection

metadata is more important than filenames