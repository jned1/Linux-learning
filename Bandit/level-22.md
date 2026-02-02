# OverTheWire Bandit — Level 22 → Level 23
📘 Personal Learning Notes (Cybersecurity Student)

## Level Goal (In My Own Words)
The goal of this level is to understand how a system-generated filename can be predicted by reading and analyzing an automated script. Instead of searching for a password directly, I needed to figure out how the system decides where sensitive information is stored and then access that location correctly.

This level pushes me to stop thinking randomly and start thinking deterministically.

## Concepts This Level Is Testing
This level focuses on several Linux and scripting fundamentals:
- Cron jobs and automated execution
- Shell variables
- Command substitution
- Hashing concepts
- Predictable file generation
- Reading and understanding shell scripts

It also reinforces the idea that scripts often follow logic that can be reasoned about.

## Why These Concepts Matter in Real Systems or Security
In real systems, automated scripts frequently generate filenames dynamically using variables, timestamps, usernames, or hashes. From a security perspective:
- Predictable naming schemes can leak sensitive data
- Scripts running with higher privileges can expose information indirectly
- Understanding how filenames are generated is critical during system enumeration
- Attackers often reverse-engineer scripts rather than attacking files directly

These ideas are essential for penetration testing, malware analysis, and secure system design.

## Reasoning Process Used to Approach the Level
The level hint suggested automation again, which pointed me back to cron jobs. I inspected the cron configuration to find the relevant job and then read the script it executed. The script did not hardcode a filename. Instead, it generated one dynamically.

The key step was carefully reading the script line by line and asking:
- What input does this script use?
- How does it transform that input?
- Where does it store the result?

Once I understood the logic, I could reproduce the same steps manually to locate the correct file.

## Commands Used (With Clear Explanations)

Listing cron jobs:
```bash
    ls /etc/cron.d
```
This lists system-wide scheduled tasks. It helped identify the cron job associated with this level.

Reading the cron job configuration:
```bash
    cat /etc/cron.d/cronjob_bandit23
```
The cat command displays file contents. This file shows which script is executed automatically and under which user context.

Reading the script executed by cron:
```bash
    cat /usr/bin/cronjob_bandit23.sh
```
This reveals the logic used to generate the output file. Reading the script carefully is more important than running it.

Reproducing the filename logic manually:
```bash
    echo <input> | <hashing_command>
```
This step mirrors the script’s behavior to determine the exact filename being used, without modifying the system.

Reading the generated file:
```bash
    cat /tmp/<predicted_filename>
```
This reads the file created by the automated process and provides the information needed to continue, without exposing the actual secret here.

## Common Mistakes or Misunderstandings
- Trying to search all of /tmp blindly instead of understanding the script
- Assuming filenames are random when they are actually deterministic
- Running scripts without reading them first
- Forgetting that scripts often rely on environment variables or command output
- Ignoring how small transformations like hashing affect filenames

## What This Level Teaches for Future Levels or Real-World Usage
This level teaches the importance of:
- Reading scripts slowly and logically
- Understanding how input becomes output in automation
- Recognizing predictable patterns in supposedly “random” data
- Applying reverse-engineering skills to shell scripts
- Thinking like both a developer and an attacker

These skills are critical for later Bandit levels and real-world Linux privilege escalation scenarios.

## Key Takeaways
Automation follows logic, not magic. Cron jobs and scripts often generate predictable results. Reading and understanding scripts is more powerful than scanning blindly, and small details like variable usage or hashing can completely change where sensitive data lives.
