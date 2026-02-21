# 25-permission-misconfigurations.md

# Permission Misconfigurations

## Introduction

Permission misconfigurations occur when file or directory access rights are set incorrectly, allowing unintended users to read, modify, or execute resources.

They are a common cause of security incidents because Linux systems rely heavily on file permissions to enforce access control. Incorrect settings can expose sensitive data, enable privilege escalation, or disrupt system integrity.

---

## World-Writable Files (777 Risk)

### What 777 Means

The permission value 777 grants:

- Owner: read, write, execute
- Group: read, write, execute
- Others: read, write, execute

This provides full access to every user on the system.

### Why It Is Dangerous

World-writable files allow any user to modify or replace content. If applied to scripts, configuration files, or binaries, it creates a high-risk attack surface.

### Realistic Risk Scenarios

- A world-writable script executed by root can be modified by a low-privileged user.
- Shared directories without proper restrictions can allow file tampering.
- Malicious code can be inserted into writable application files.

---

## Incorrect Ownership

### Files Owned by Wrong Users

Files critical to system operation should be owned by appropriate system accounts. Incorrect ownership may allow unauthorized modification.

### Sensitive Files Owned by Non-Root Users

Configuration files, system binaries, or service files owned by non-root users increase the risk of compromise if those users are exploited.

### Security Impact

Improper ownership can lead to privilege abuse, unauthorized changes, and weakened access control enforcement.

---

## Misconfigured SUID/SGID Binaries

### Risk of Unnecessary SUID Binaries

SUID and SGID permissions allow programs to execute with elevated privileges. If assigned unnecessarily, they expand the attack surface.

### Privilege Escalation Implications

A vulnerable SUID binary may allow attackers to execute arbitrary commands with elevated permissions.

### Why Auditing Is Important

Regular audits ensure only required binaries retain SUID or SGID bits and reduce the likelihood of exploitation.

---

## Writable Configuration Files

### Risk of Modifying System Configurations

If configuration files are writable by non-privileged users, attackers may alter service behavior or inject malicious parameters.

### Service Hijacking Scenarios

- Modifying web server configuration to redirect traffic.
- Altering startup scripts to execute unauthorized commands.
- Changing authentication settings to weaken security controls.

---

## Writable Directories in System Paths

### PATH Manipulation Risks

If directories included in the system PATH are writable by non-privileged users, attackers can place malicious executables in those directories.

### Executable Replacement Scenarios

A malicious file with the same name as a legitimate command may be executed instead, especially if executed by a privileged user.

---

## Detecting Permission Issues

### Using find to Locate World-Writable Files

    find / -type f -perm -0002 2>/dev/null

### Checking SUID/SGID Files

Find SUID files:

    find / -perm -4000 2>/dev/null

Find SGID files:

    find / -perm -2000 2>/dev/null

### Reviewing Ownership with ls -l

    ls -l filename

This command displays file permissions, ownership, and group information for review.

---

## Mitigation Best Practices

### Principle of Least Privilege

Grant only the minimum permissions required for functionality.

### Regular Audits

Periodically review file permissions, ownership, and special bits to detect misconfigurations.

### Avoiding 777 Permissions

Avoid assigning full permissions to all users. Use more restrictive numeric values where appropriate.

### Proper Ownership Management

Ensure sensitive files are owned by root or appropriate service accounts and protected from unauthorized modification.

---

## Summary

Permission misconfigurations in Linux systems commonly include world-writable files, incorrect ownership, unnecessary SUID/SGID binaries, writable configuration files, and insecure directories within system paths. These issues can lead to privilege escalation, service compromise, and data tampering. Proper permission management, regular auditing, and adherence to the principle of least privilege are essential to maintaining system security.