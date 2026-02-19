# 14-mounting-and-devices.md

# Mounting and Devices

## Introduction

In Linux, storage devices are not accessed directly through drive letters. Instead, devices are integrated into a single unified directory tree through a process called mounting.

Understanding how mounting and device files work is essential for system administration and cybersecurity because storage configuration errors, unauthorized mounts, or malicious device usage can lead to data exposure, persistence, or privilege escalation.

---

# Devices in Linux

## What Are Device Files?

In Linux, hardware devices are represented as special files located in:

    /dev/

These files provide an interface between user space and hardware through the kernel.

Device files do not contain data themselves. They act as communication endpoints managed by the kernel.

---

## Types of Storage Devices

### Block Devices

Block devices transfer data in fixed-size blocks and support random access.

Examples:

    /dev/sda
    /dev/sdb1
    /dev/nvme0n1

These typically represent:
- Hard drives
- Solid-state drives
- USB storage devices
- Disk partitions

Block devices are commonly mounted to access their filesystems.

---

### Character Devices

Character devices transfer data sequentially, one character at a time.

Examples:

    /dev/tty
    /dev/random

Character devices are generally not mounted like storage devices but are used for system input/output operations.

---

# What Is Mounting?

## Definition

Mounting is the process of attaching a filesystem on a storage device to a specific directory within the Linux filesystem hierarchy.

After mounting, the contents of the device become accessible through the chosen directory.

---

## Mount Points

A mount point is an empty directory where a filesystem is attached.

Example:

    /mnt
    /media/usb

When a device is mounted to a directory, the original contents of that directory (if any) are temporarily hidden until the device is unmounted.

---

# Viewing Mounted Devices

To display currently mounted filesystems:

    mount

Or:

    lsblk

These commands show:
- Device names
- Mount points
- Filesystem types

Understanding active mounts is important when investigating unauthorized storage usage.

---

# Mounting a Device

## Basic Syntax

    mount /dev/device_name /mount/point

Example:

    mount /dev/sdb1 /mnt

This attaches the filesystem on `/dev/sdb1` to the `/mnt` directory.

The system must have appropriate permissions to perform mount operations.

---

# Unmounting a Device

To detach a filesystem:

    umount /mount/point

Example:

    umount /mnt

Unmounting ensures that all data is properly written and prevents corruption.

---

# Automatic Mounting

Modern Linux systems use configuration files and service managers to mount devices automatically at boot.

Common mechanisms include:
- Static configuration in system files
- Dynamic mounting through system services

Improper configuration can expose sensitive filesystems or allow unauthorized device access.

---

# Security Implications

## Unauthorized Device Mounting

An attacker with sufficient privileges may:
- Mount external storage devices
- Access sensitive data
- Introduce malicious files

Monitoring mount activity is important in secure environments.

---

## Sensitive Filesystem Exposure

Mounting sensitive partitions (such as backup disks or encrypted volumes) without proper access controls may expose confidential data.

---

## Removable Media Risks

USB drives or external disks can:
- Introduce malware
- Exfiltrate data
- Bypass network-based security controls

Systems should enforce policies regarding removable media usage.

---

## Forensic Relevance

During incident response, investigators must:
- Identify mounted filesystems
- Check for unusual mount points
- Examine external devices connected to the system

Unexpected mounts may indicate data staging or persistence mechanisms.

---

# Summary

In Linux, devices are represented as special files within `/dev`, and storage devices are integrated into the filesystem through mounting. Mounting attaches a device’s filesystem to a directory, making its contents accessible.

Understanding mounting and device management is critical for secure system configuration, monitoring unauthorized storage activity, and performing effective forensic investigations.