# Bandit Level 5

## Goal
find the password
The password stored in :
1) human-readable files
2) size of the file 1033 byte
3) have no executable premission 
 


## What is premission in linux 
it's Who can do what to files/folders

Three Types:
Read (r) - View file/list directory
Write (w) - Modify/delete
Execute (x) - Run file/enter directory

Three Users:
Owner (u) - File creator
Group (g) - Users in same group
Others (o) - Everyone else
example:
rwx rwx rwx

## Commands used
```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220 ##using the password u found last level
cd inhere
ls -al 
find . -type f ! -executable -size 1033c -exec file{} \; | grep -i text
cat ./hereiam/file03
```
## explenation 
1) find . -type f
    This part answers one question: what files should we look at?

    find → walks through directories recursively.

    . → start from the current directory.

    -type f → only regular files (no directories, no sockets, no devices).

    So at this stage, Linux is saying:
    “Give me every normal file under here
2) ! -executable

    Exclude files that have the executable bit set.

    This checks Linux permission bits, not file content.
3) ! -executable

    Exclude files that have the executable bit set.

    This checks Linux permission bits, not file content.

4) -exec file {} \;

    Now we inspect the content of each file.

    -exec → run a command on each result from find.

    file → analyzes the file contents, not the name.

    {} → placeholder for the current filename.

    \; → ends the -exec command (escaped so the shell doesn’t eat it).

5) | grep -i text

    | : this called pipline take the output from the first command and put it as input for the next command

    Keep only files whose file output contains the word text (ASCII, UTF-8, scripts, etc.).

    This is what enforces human-readable.
6) cat the file :
    after finding the human-readable file, now u can open the file and take the password

