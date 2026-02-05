# OverTheWire Bandit — Level 27 → Level 28
📘 Personal Learning Notes (Cybersecurity Student)

## Level Goal (In My Own Words)
The goal of this level is to retrieve information from a version-controlled project rather than from a single file or automated process. Instead of searching the filesystem blindly, I needed to understand how developers store and share data using Git and how to inspect a repository properly.

This level introduces real developer workflows into the security learning path.

## Concepts This Level Is Testing
This level focuses on:
- Git version control basics
- Cloning remote repositories
- Exploring repository contents
- Understanding how information can be stored in project files
- Navigating directories safely

It also reinforces that sensitive data can live in places developers don’t always expect.

## Why These Concepts Matter in Real Systems or Security
In real-world environments:
- Source code repositories often contain configuration files, secrets, or credentials
- Public and private Git repositories are frequent targets during security assessments
- Many breaches occur because sensitive data is accidentally committed

For security professionals, knowing how to inspect repositories is as important as knowing how to scan servers.

## Reasoning Process Used to Approach the Level
The level instructions hinted that the information was stored in a Git repository. That immediately suggested that I should clone the repository rather than search system directories.

My approach was:
- Create a safe working directory
- Clone the repository locally
- Inspect the files inside the project
- Read documentation or configuration files carefully

The challenge was not exploiting Git, but understanding how to use it correctly.

## Commands Used (With Clear Explanations)

Creating a working directory:
```bash
    mkdir /tmp/bandit27
```
The mkdir command creates a new directory. Using /tmp keeps work isolated and avoids cluttering the home directory.

Cloning the repository:
```bash
    git clone <repository_url>
```
The git clone command downloads a full copy of the repository, including its files and history.

Entering the repository directory:
```bash
    cd <repository_name>
```
The cd command changes the current working directory so files inside the repository can be explored.

Listing repository contents:
    ls
The ls command shows files and directories tracked by the repository.

Reading project files:
```bash
    cat <filename>
```
The cat command displays file contents, allowing inspection of documentation or configuration data.

## Common Mistakes or Misunderstandings
- Trying to search the entire filesystem instead of cloning the repository
- Forgetting to work in a writable directory
- Assuming secrets must be hidden or encrypted
- Ignoring README or documentation files
- Treating Git as a security feature rather than a storage system

A common misunderstanding is assuming version control hides information. It does not.

## What This Level Teaches for Future Levels or Real-World Usage
This level teaches:
- How Git repositories can expose sensitive information
- Why repository inspection is a standard security practice
- How to navigate developer tools as a security professional
- The importance of reviewing code and documentation carefully

These skills are essential for source code audits, bug bounty work, and penetration testing.

## Key Takeaways
Source code is a treasure map. Git is not just for developers, and security often starts by reading what others have written. Understanding development workflows makes security analysis far more effective.
