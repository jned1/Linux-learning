# 45-cron-jobs.md

# Cron Jobs in Linux

## 1. Introduction to Cron

### What is Cron?

Cron is a time-based job scheduling system in Linux and Unix-like operating systems. It allows users and administrators to automatically run commands or scripts at specified times and intervals.

### What is a Cron Job?

A cron job is a scheduled task configured to execute automatically according to a defined time pattern.

### Why Task Scheduling Is Important

Task scheduling is essential for:

- Automating backups
- Rotating logs
- Running maintenance scripts
- Performing security checks
- Monitoring system health

In cybersecurity, cron jobs can be used for automated audits and alerts, but misconfigured jobs may also create security risks.

---

## 2. Cron Daemon

### Role of the Cron Service

The cron daemon (`cron` or `crond`) runs in the background and continuously checks configuration files for scheduled tasks to execute.

### How Cron Runs

- Starts automatically at system boot
- Reads crontab files
- Executes commands when the specified time matches

### Checking Cron Service Status

    systemctl status cron
    systemctl status crond

---

## 3. Crontab Basics

### What is Crontab?

Crontab (cron table) is a file that contains scheduled jobs and their execution times.

### User Crontab vs System Crontab

- **User crontab:** Specific to each user account.
- **System crontab:** Located in `/etc/crontab`, used for system-wide scheduling and includes a user field.

### Editing Crontab

    crontab -e

This opens the current user’s crontab file in a text editor.

### Listing Crontab Entries

    crontab -l

Displays existing scheduled jobs for the current user.

### Removing Crontab

    crontab -r

Removes all cron jobs for the current user.

---

## 4. Cron Time Format

Cron uses five time fields followed by the command.

### Time Fields

1. Minute (0–59)
2. Hour (0–23)
3. Day of Month (1–31)
4. Month (1–12)
5. Day of Week (0–7)  
   (0 and 7 represent Sunday)

### Format Structure

    * * * * * command_to_execute

Each asterisk (*) represents "every possible value" for that field.

### Common Schedule Examples

Run every day at 2:30 AM:

    30 2 * * * /path/to/script.sh

Run every Monday at 8:00 AM:

    0 8 * * 1 /path/to/script.sh

Run every hour:

    0 * * * * /path/to/script.sh

---

## 5. Creating Cron Jobs

### Run a Script Every Day

    0 1 * * * /home/user/backup.sh

### Run a Task Every 5 Minutes

    */5 * * * * /home/user/check.sh

### Run a Task at Reboot

    @reboot /home/user/startup_script.sh

---

## 6. Cron Job Security Considerations

### File Permissions for Scripts

- Ensure scripts are owned by the correct user.
- Restrict write permissions to prevent unauthorized modification.

Example:

    chmod 700 /home/user/backup.sh

### Absolute Paths Requirement

Cron uses a minimal environment. Always use full paths to:
- Scripts
- Commands
- Binaries

Example:

    0 2 * * * /usr/bin/python3 /home/user/script.py

### Risks of Misconfigured Cron Jobs

- Running scripts as root unnecessarily
- World-writable script files
- Executing untrusted input

### Privilege Escalation Considerations

If a root-owned cron job executes a writable script, attackers may modify it to gain elevated privileges. Proper permissions and monitoring are critical.

---

## 7. Practical Examples

### Create a Simple Backup Script

Create a script:

    nano /home/user/backup.sh

Example content:

    #!/bin/bash
    tar -czf /home/user/backup.tar.gz /home/user/Documents

Make it executable:

    chmod +x /home/user/backup.sh

Schedule it daily at midnight:

    0 0 * * * /home/user/backup.sh

---

### Verify Cron Job Execution

Check crontab entries:

    crontab -l

Check system logs (distribution dependent):

    journalctl -u cron
    grep CRON /var/log/syslog

---

### Troubleshooting Basic Issues

- Ensure cron service is running:

      systemctl status cron

- Verify script permissions
- Use absolute paths
- Test the script manually before scheduling

---

## 8. Summary

Cron is a powerful task scheduling tool that automates routine operations in Linux systems. By understanding crontab structure, time format, and service behavior, administrators can reliably schedule maintenance, backups, and monitoring tasks. Proper configuration and secure permissions are essential to prevent misuse and privilege escalation risks.