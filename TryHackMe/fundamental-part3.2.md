## TryHackME (learn the linux fundamental part -3.2)
### Overview :
in this file we will continue the second section of part 3.
with maintaining the sysytem (automation,package management, logs)
Everything here reflects what I studied, tested, and verified myself.

## 1) Maintaining Your System: Automation

Modern Linux systems shine because they can take care of themselves. Automation means letting the system perform routine tasks for you—on time, every time—without human babysitting. Backups, updates, log cleanup, monitoring scripts… all of these are ideal candidates.

At the heart of classic Linux automation lives a small, relentless worker: cron.
### Scheduling Certain Actions

Scheduling is the act of telling the system what to do and when to do it.
Examples of scheduled actions:
Run a backup script every night at 2:00 AM
Clean temporary files once a week
Restart a service every Sunday
Check disk usage every hour and log the result
Instead of remembering these tasks, Linux remembers for you.
This is usually done with:
cron (time-based scheduling)
systemd timers (modern alternative, more structured)
This section focuses on cron, because it exists on almost every Unix-like system.

### The Cron Process

cron is a daemon (a background service) that wakes up every minute, checks its schedule, and executes any task that matches the current time.
Important characteristics:
Runs continuously in the background
Executes commands automatically
Uses configuration files called crontabs
Runs tasks with the permissions of the user who owns the crontab
You can check if cron is running with:
```bash
systemctl status cron
```
(or crond on some distributions)
### Interacting with Cron Using Crontabs

A crontab (cron table) is a file that defines scheduled jobs.
Each user can have their own crontab, and there is also a system-wide crontab.
Common Crontab Commands
Edit your crontab:
```bash
crontab -e
```

List your current jobs:
```bash
crontab -l
```

Remove all scheduled jobs:
```bash
crontab -r
```

Behind the scenes, these files are stored in:
```bash
/var/spool/cron/
```
You usually never edit them directly—crontab -e does that safely.
### Crontab Syntax (Crontab Values)
Each cron job is written on one line, with this structure:
```bash
* * * * * command_to_execute

┌──────── minute (0–59)
│ ┌────── hour (0–23)
│ │ ┌──── day of month (1–31)
│ │ │ ┌── month (1–12)
│ │ │ │ ┌─ day of week (0–7) (Sunday = 0 or 7)
│ │ │ │ │
* * * * * command
```
Special Characters
1) * → any value
2) */n → every n units
3) , → multiple values (e.g. 1,15)
4) - → range (e.g. 1-5)
### Why Cron Matters in System Maintenance

Cron is simple, old, and brutally reliable. It doesn’t care about GUIs, moods, or weekends. It just executes instructions on time.
For system administrators and security professionals, cron is essential because it enables:
Automated backups
Log rotation
Security scans
Health checks
Scheduled updates
In short: automation reduces human error, and cron is one of the oldest tools we trust to do exactly that.

## Maintaining Your System: Package Management

A Linux system is not maintained by downloading random installers from the internet. Instead, software is installed, updated, and removed in a controlled, verifiable way using packages and software repositories.
This approach improves stability, security, and reproducibility across systems.
Package management is one of Linux’s greatest strengths—and one of the main reasons servers can run unattended for years.

### What Are Packages?

A package is a compressed archive that contains:
Program files (binaries or source code)
Configuration files
Documentation
Metadata (name, version, dependencies, checksums)
Instead of installing software file-by-file, Linux installs packages as a single managed unit.

Common package formats:
.deb → Debian, Ubuntu, Kali
.rpm → Red Hat, CentOS, Fedora
.pkg.tar.* → Arch Linux

Each package knows:
What it need to run (dependencies)
What files it installs
How to cleanly remove itself
This prevents the “dependency hell” common in unmanaged systems.

### What Is a Package Manager?

A package manager is the tool that:
Downloads packages
Verifies their integrity
Resolves dependencies
Installs, updates, or removes software

Examples:
apt / apt-get → Debian-based systems
dnf / yum → Red Hat-based systems
pacman → Arch Linux
For example, on Debian/Ubuntu:
```bash
sudo apt install nginx
```

This single command:
Finds the package
Downloads it from a trusted source
Installs required dependencies
Configures the software

### APT (Advanced Package Tool)

APT is a high-level package management system built on top of lower-level tools like dpkg.
Common APT commands:
```bash
sudo apt update        # refresh package lists
sudo apt upgrade       # upgrade installed packages
sudo apt install pkg   # install software
sudo apt remove pkg    # remove software
sudo apt purge pkg     # remove software + configs
sudo apt autoremove    # clean unused dependencies
```
### GPG and Package Security

Linux repositories are secured using GPG (GNU Privacy Guard) keys.

Why GPG Matters
When you install software, APT verifies:
The package has not been modified
The package comes from a trusted source
The repository owner signed it
Without GPG verification, a malicious mirror could inject malware silently.

## Maintaining Your System: Logs

Logs are the system’s memory. Every important action—services starting, users logging in, firewalls blocking traffic, attacks being stopped—is written down. When something breaks or gets compromised, logs are where the truth hides.

On Linux, logs are mostly plain text files, which makes them powerful, searchable, and script-friendly.

### Apache2 Logs

Apache is one of the most widely used web servers, and it generates detailed logs about every request and error.

Apache Log Location
/var/log/apache2/

Important Apache Log Files
Access Log
/var/log/apache2/access.log

Records:
Client IP address
Requested URL
HTTP method (GET, POST)
Response code (200, 404, 403)
User-Agent

Example entry:
```bash
192.168.1.10 - - [23/Jan/2026:12:10:45 +0000] "GET /index.html HTTP/1.1" 200 1024
```
Error Log
```bash
/var/log/apache2/error.log
```

Records:
Server startup/shutdown messages
Misconfigurations
Permission issues
Module failures

Apache logs are essential for:
Debugging website issues
Detecting suspicious requests
Forensic analysis after attacks

### Fail2Ban Logs

Fail2Ban is a security tool that protects services from brute-force attacks by banning malicious IP addresses automatically.

Fail2Ban Log Location
/var/log/fail2ban.log

What Fail2Ban Logs Contain
Detected authentication failures
Triggered bans
Unbans after timeout
Which service (SSH, Apache, FTP) was attacked

Example:
```bash
2026-01-23 14:32:10,123 fail2ban.actions [1234]: NOTICE [sshd] Ban 203.0.113.45
```

Fail2Ban works by:
Reading other logs (like /var/log/auth.log)
Detecting repeated failures
Writing actions to its own log
This log is critical for:
Identifying attack patterns
Confirming protection is working
Incident response

### UFW Logs (ufw.log)

UFW (Uncomplicated Firewall) is a front-end for iptables / nftables. When logging is enabled, it records blocked and allowed network traffic.

UFW Log Location
/var/log/ufw.log

What UFW Logs Show
Blocked incoming connections
Blocked outgoing connections
Protocol used (TCP/UDP)
Source and destination IP
Ports involved

Example:
```bash
UFW BLOCK IN=eth0 OUT= MAC=... SRC=198.51.100.23 DST=192.168.1.5 LEN=60 PROTO=TCP SPT=44444 DPT=22
```
This tells you:
Someone tried to access SSH (port 22)
The firewall blocked it
From which IP the attempt came

Enable UFW logging:
sudo ufw logging on