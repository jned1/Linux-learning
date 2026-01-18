##  TryHackME (learn the linux fundamental part -1)
## overview

This section documents my learning from **TryHackMe Linux Fundamentals – Part 1**.
The goal of this part is to understand basic Linux concepts, commands, and file system navigation.
This is a learning log, not a tutorial. Everything here reflects what I studied, tested, and verified myself.

## Introduction 
Linux is not one program. It’s a family of operating systems built around the Linux kernel (the core that talks to hardware) plus a large ecosystem of tools, utilities, and shells. Most of what beginners feel as “Linux” is actually the command line (CLI): small programs that do one thing well and can be chained together like LEGO bricks.

Development began in 1991 while Torvalds was a student.
The project was publicly announced on August 25, 1991.
The first kernel release (0.01) was made available on September 17, 1991.

## first basic commands(echo,whoami)
echo prints text to standard output (usually the terminal). It’s deceptively simple but crucial because it shows how data flows in Linux.
```bash
echo "hello github"
```
whoami
whoami tells you which user account you are currently using. Linux is multi-user by design, and permissions depend on who you are.

## interacting with the file system(ls,cd,cat,pwd)
ls 
ls lists files and directories in ur current directory.
```bash
ls -l #dont worry about -l we will explain it later
 ```
cd
cd changes the current working directory. Linux always assumes you are somewhere in the filesystem tree.
```bash
cd /user/github
cd .. # this is used to go back 
```
cat
cat outputs the contents of a file to the terminal. Despite the name, it’s about concatenation, not animals.
```bash
cat file.txt
```
pwd
pwd prints the full path of your current directory.
```bash
pwd
```
## Searching for files(find,grep)
find
find searches for files and directories based on rules: name, size, type, time, permissions.
```bash
find  -name "*.txt" 

```
grep
grep searches inside text for patterns.
```bash
grep "root" /etc/passwd
```
## Introduction to shell operator(&,&&,>,>>)
These are not commands; they control how commands interact.

& :Runs a command in the background.
The shell doesn’t wait; you get your prompt back immediately.
```bash
sleep 60 &
```
&&
Logical AND between commands. The second command runs only if the first succeeds.
This is defensive programming at the shell level.
```bash
mkdir test && cd test
```
>
Redirects output to a file, overwriting it.
Standard output is quietly rerouted from screen to disk.
```bash
echo "hello" > file.txt
```
>>
Redirects output to a file, appending instead of overwriting.
Same idea as >, but kinder to existing data.
```bash
echo "another line" >> file.txt
```
## Notes:
 i have practice within the terminal provided by THM and my own one also and us should also so u can remeber very will