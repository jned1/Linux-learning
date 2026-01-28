# Bandit Level 12

## Goal
find the password
The password stored in :
file name data.txt
file is a hexdump
data was compressed multiple times using different formats
### Commands used
```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
mkdir /tmp/bandit12
cp data.txt /tmp/bandit12
cd /tmp/bandit12
xxd -r data.txt > data
file data
```
## explenation
mkdir /tmp/bandit12

create a temporary working directory
used to safely extract files

cp data.txt /tmp/bandit12

copy the file to the temporary directory

xxd -r data.txt > data

xxd → create hex dump
-r → reverse hex dump back to binary

this converts the hexdump into a binary file

file data

identify the file type
this tells which compression was used
## Decompression process
depending on the output of file, repeat these steps:

if gzip:
```bash
mv data data.gz
gzip -d data.gz
```
if bzip2:
```bash
mv data data.bz2
bzip2 -d data.bz2
```
if tar:
```bash
tar -xf data
```
after each step:
```bash
file data

```
repeat until the file becomes readable text
cat the final file
```bash
cat data
```
this prints the password for Bandit Level 13