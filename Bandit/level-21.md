# OverTheWire Bandit — Level 21 → Level 22  
📘 Personal Learning Notes (Cybersecurity Student)

---

## Level Goal (In My Own Words)

The goal of this level is to discover how **scheduled tasks (cron jobs)** can run commands automatically on a Linux system and how files created or modified by those tasks can reveal information needed to move forward. Instead of manually searching files, the challenge pushes me to think about **what runs automatically in the background** and **where its output goes**.

No passwords are meant to be guessed. The system itself is doing the work — I just need to observe it correctly.

---

## Concepts This Level Is Testing

This level focuses on a few important Linux and security fundamentals:

- **Cron jobs** (`cron`): a Linux service that runs commands automatically at scheduled times
- **System-wide cron directories** like `/etc/cron.d`
- **Shell scripts** executed by the system
- **File permissions and ownership**
- **Temporary or generated files**
- **Reading scripts to understand behavior**

---

## Why These Concepts Matter in Real Systems

Cron jobs are everywhere in real-world systems:
- Log rotation
- Backups
- Cleanup tasks
- Automated admin scripts

From a security perspective:
- Misconfigured cron jobs can leak sensitive data
- Writable scripts or output files can be abused for privilege escalation
- Attackers often look for **automated processes** running as more powerful users

Understanding cron is essential for:
- Linux administration
- Penetration testing
- Incident response
- Malware analysis (persistence mechanisms)

---

## Reasoning Process (How I Approached the Level)

The level description hints that *something is running automatically*. That immediately suggests cron.

So my thought process was:
1. Find where cron jobs are defined
2. Identify which job is related to this level
3. Read the script being executed
4. Understand **what file it creates or modifies**
5. Read that file carefully

The key mindset shift here:
> Don’t try to “find the password directly” — instead, **understand the system behavior**.

---

## Commands Used (With Explanations)

### 1️⃣ Listing cron jobs

```bash
ls /etc/cron.d
```
ls — lists directory contents
/etc/cron.d — directory containing system cron job definitions
This shows custom cron jobs created for Bandit levels.

### 2️⃣ Reading the cron job file
```bash
cat /etc/cron.d/cronjob_bandit22
```
cat — prints file contents to the terminal
The cron file shows:
Who runs the job
What script is executed
How often it runs
This step is critical. The cron file tells me exactly what happens automatically.

### 3️⃣ Reading the referenced script
```bash
cat /usr/bin/cronjob_bandit22.sh
```
This script is executed by cron
Reading it reveals:
Commands being run
Files being written to
Logic that produces the output
I didn’t run the script manually — I just read and understood it.

### 4️⃣ Inspecting the output file
From the script, I learned which file is created/updated. Then I viewed it:
```bash
cat /tmp/<generated_file>
```
/tmp — temporary directory, often used by automated scripts
The file content is updated regularly by cron