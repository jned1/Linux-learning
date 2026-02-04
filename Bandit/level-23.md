# OverTheWire Bandit — Level 23 → Level 24
📘 Personal Learning Notes (Cybersecurity Student)

## Level Goal (In My Own Words)
The goal of this level is to understand how a system executes **user-provided scripts automatically** and how file permissions can allow one user to influence actions performed by another. Instead of reading an output file like previous levels, I needed to realize that I could *inject behavior* by placing a script in the correct location and letting the system execute it for me.

This level is about controlling execution flow, not reading static data.

## Concepts This Level Is Testing
This level focuses on several important Linux fundamentals:
- Cron jobs and scheduled execution
- Writable directories used by automated tasks
- Shell scripting basics
- File ownership and permissions
- Standard input and output redirection
- Understanding how scripts are executed non-interactively

It also introduces the idea of **indirect execution**, where code runs because the system decides to run it.

## Why These Concepts Matter in Real Systems or Security
In real-world systems, automated execution is extremely common. Cron jobs often process files placed in specific directories, such as:
- Upload folders
- Temporary task queues
- Maintenance directories

From a security perspective:
- Writable execution paths are dangerous
- Automated execution can be abused for privilege escalation
- Many real attacks rely on placing malicious scripts where trusted automation will run them

This level mirrors real vulnerabilities seen in production systems.

## Reasoning Process Used to Approach the Level
The level description hinted that a cron job was involved again, but this time the behavior was different. After locating the cron job and reading the script it executed, I noticed something important: the script **executed all files inside a specific directory**.

The key questions I asked were:
- Who owns this directory?
- Can I write to it?
- What happens to scripts placed there?
- Under which user do they run?

Once I realized I could write my own script into that directory, the solution became clear: let the system execute my logic for me.

## Commands Used (With Clear Explanations)

Listing cron jobs:
```bash
    ls /etc/cron.d
```
This command lists system-wide scheduled tasks and helps identify which cron job is relevant to the current level.

Reading the cron job configuration:
```bash
    cat /etc/cron.d/cronjob_bandit24
```
This shows which script runs automatically, how often it runs, and under which user account.

Reading the executed script:
```bash
    cat /usr/bin/cronjob_bandit24.sh
```
This reveals that the script processes and executes files from a specific directory, rather than reading from a fixed file.

Checking directory permissions:
```bash
    ls -ld /var/spool/<directory_name>
```
The -l flag shows detailed permissions, and -d ensures the directory itself is listed. This confirms whether files can be written there.

Creating a custom script:
```bash
    nano /var/spool/<directory_name>/my_script.sh
```
This creates a shell script that will be executed automatically. The script contains simple commands to capture sensitive output safely.

Making the script executable:
```bash
    chmod +x /var/spool/<directory_name>/my_script.sh
```
The chmod command changes file permissions. The +x flag allows the script to be executed.

Redirecting output to a readable location:
```bash
    command > /tmp/output_file
```
This redirects command output to a file I can read later, without exposing the secret here.

## Common Mistakes or Misunderstandings
- Trying to read files directly instead of influencing execution
- Forgetting to make the script executable
- Writing the script in the wrong directory
- Using absolute paths incorrectly inside the script
- Assuming cron jobs only read files instead of executing them

Another common mistake is impatience — cron jobs run on a schedule, not instantly.

## What This Level Teaches for Future Levels or Real-World Usage
This level teaches one of the most important security lessons so far:
- Writable execution paths are extremely dangerous
- Automation can be exploited without breaking permissions directly
- Understanding *who executes what* is as important as *who owns a file*

These ideas are foundational for Linux privilege escalation, malware persistence, and real-world exploitation techniques.

## Key Takeaways
Automation is powerful and dangerous. If a system automatically executes files from a writable location, control over that directory means control over execution. Reading scripts carefully and understanding permissions turns the system itself into a tool.
