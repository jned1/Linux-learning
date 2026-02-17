# 03-filesystem-hierarchy-standard.md

# Filesystem Hierarchy Standard (FHS)

## Introduction

### Define FHS

The Filesystem Hierarchy Standard (FHS) defines the directory structure and directory contents in Linux systems. It specifies how files and directories should be organized so that software, administrators, and users can rely on consistent paths across different distributions.

FHS ensures that essential system files, configuration data, binaries, and logs are stored in predictable locations.

---

### Explain Why Standardization Matters in Linux Systems

Standardization allows:

- Software to function consistently across distributions
- Administrators to manage systems efficiently
- Security teams to investigate systems using known directory paths
- Automation tools to operate reliably

Without FHS, each distribution could organize files differently, increasing complexity and reducing interoperability.

---

# Root Directory (/)

## Purpose

The root directory, represented as `/`, is the top-level directory in Linux. All other directories and files branch from this location.

It serves as the starting point of the entire filesystem hierarchy.

---

## Why Everything Starts from Root

Linux uses a unified directory tree. Unlike some operating systems that use multiple drive letters, Linux mounts all storage devices under the root directory.

Every file path in the system begins with `/`. For example:

    /etc/passwd
    /var/log/syslog
    /home/user/

This centralized structure simplifies management and access control.

---

# Core Directories

## /bin

**Purpose:**  
Contains essential user command binaries.

**Data Stored:**  
Basic commands required for system operation, such as file manipulation and process inspection tools.

**Security Importance:**  
If binaries in this directory are modified, attackers can replace legitimate commands with malicious versions. Integrity monitoring of this directory is critical.

---

## /sbin

**Purpose:**  
Stores essential system binaries used for system administration.

**Data Stored:**  
Administrative commands typically executed by the root user.

**Security Importance:**  
These binaries often require elevated privileges. Unauthorized modification may allow privilege escalation or persistent compromise.

---

## /etc

**Purpose:**  
Contains system-wide configuration files.

**Data Stored:**  
Configuration for services, network settings, authentication files, and system initialization.

**Security Importance:**  
Misconfigurations in this directory can create vulnerabilities. Files such as user account and authentication configurations are frequently targeted during attacks.

---

## /home

**Purpose:**  
Stores personal directories for regular users.

**Data Stored:**  
User files, personal configurations, and application data.

**Security Importance:**  
User directories are common locations for malware payloads and unauthorized scripts. Monitoring unusual files in this directory is important during investigations.

---

## /root

**Purpose:**  
Home directory of the root user.

**Data Stored:**  
Administrative files and root user configurations.

**Security Importance:**  
Unauthorized access to this directory indicates full system compromise.

---

## /var

**Purpose:**  
Contains variable data that changes frequently.

**Data Stored:**  
Logs, mail queues, print jobs, temporary files, and application data.

**Security Importance:**  
Log files stored here are essential for forensic analysis. Attackers may attempt to modify or delete logs to hide activity.

---

## /tmp

**Purpose:**  
Stores temporary files created by applications and users.

**Data Stored:**  
Short-lived temporary data.

**Security Importance:**  
World-writable permissions make this directory a common location for malicious scripts or privilege escalation exploits. Monitoring suspicious executable files in this directory is important.

---

## /usr

**Purpose:**  
Contains user applications and read-only data.

**Data Stored:**  
Secondary binaries, libraries, documentation, and shared resources.

**Security Importance:**  
Software installed here should remain stable. Unexpected changes may indicate compromise or unauthorized installations.

---

## /opt

**Purpose:**  
Stores optional or third-party software packages.

**Data Stored:**  
Commercial or manually installed applications.

**Security Importance:**  
Applications installed here may not be managed by the system package manager. This increases the risk of outdated or vulnerable software.

---

## /boot

**Purpose:**  
Contains files required for system booting.

**Data Stored:**  
Kernel images, bootloader configuration files, and initial RAM disk images.

**Security Importance:**  
Tampering with this directory can allow persistent low-level compromise before the operating system fully loads.

---

## /dev

**Purpose:**  
Contains device files representing hardware components.

**Data Stored:**  
Device interfaces for disks, terminals, and other hardware.

**Security Importance:**  
Access to certain device files can grant direct hardware access. Proper permissions are critical to prevent misuse.

---

## /proc

**Purpose:**  
Virtual filesystem providing runtime system information.

**Data Stored:**  
Process details, kernel parameters, memory usage, and system state.

**Security Importance:**  
Used for monitoring running processes and detecting suspicious activity. Attackers may inspect this directory to gather system intelligence.

---

## /lib and /lib64

**Purpose:**  
Store essential shared libraries required by system binaries.

**Data Stored:**  
Dynamic libraries needed for core commands and applications.

**Security Importance:**  
If a shared library is replaced with a malicious version, all dependent programs may become compromised. Library integrity is critical for system trust.

---

# Why FHS Matters in Cybersecurity

## Log Investigation Relevance

Knowing standard log locations such as those within `/var` allows analysts to quickly locate evidence during incident investigations.

---

## Malware Persistence Locations

Attackers commonly use predictable directories such as:
- `/tmp` for temporary execution
- `/home` for user-level persistence
- `/etc` for modifying startup configurations
- `/var` for hiding malicious scripts among application data

Understanding FHS helps identify abnormal file placements.

---

## Privilege Escalation Relevance

Misconfigured permissions in directories like:
- `/bin`
- `/sbin`
- `/usr`
- `/etc`

May allow attackers to modify executables or configuration files, leading to elevated privileges.

---

## Incident Response Benefits

FHS knowledge allows responders to:
- Identify abnormal files
- Validate system integrity
- Understand service configurations
- Locate startup mechanisms

A standardized layout accelerates forensic analysis and containment.

---

# Summary

The Filesystem Hierarchy Standard defines a consistent directory structure for Linux systems. It ensures predictable placement of binaries, configuration files, logs, libraries, and user data.

Understanding the purpose and security implications of each core directory enables effective system administration, log investigation, malware detection, and incident response. Mastery of the Linux directory structure is essential for secure system operation and cybersecurity analysis.
