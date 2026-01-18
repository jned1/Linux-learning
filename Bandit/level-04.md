# Bandit Level 4

## Goal
The password stored in the only-human-readable files (this is not a name)


## Human-Readable Files What They Are:
Files that humans can read and understand without special tools.

## Examples:
.txt  - Text files (notes, documents)
.md   - Markdown files (like this!)
.csv  - Spreadsheet data (Excel compatible)
.json - Structured data (easy to read)
.yaml - Configuration files
.html - Web pages (view in browser)


## Commands used
```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220 ##using the password u found last level
cd inhere
ls -al 
find . -type f -exec file{} \;
cat ./-file07
```
## explenation 
1) find . -type f
    This part answers one question: what files should we look at?

    find → walks through directories recursively.

    . → start from the current directory.

    -type f → only regular files (no directories, no sockets, no devices).

    So at this stage, Linux is saying:
    “Give me every normal file under here
2) -exec file {} \;

    Now we inspect the content of each file.

    -exec → run a command on each result from find.

    file → analyzes the file contents, not the name.

    {} → placeholder for the current filename.

    \; → ends the -exec command (escaped so the shell doesn’t eat it).
3) cat the file :
    after finding the human-readable file, now u can open the file and take the password
