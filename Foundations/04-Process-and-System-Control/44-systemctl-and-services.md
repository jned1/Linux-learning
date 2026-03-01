# 44-systemctl-and-services.md

# systemctl and Services in Linux

## 1. Introduction to systemd

### What is systemd?

`systemd` is the initialization and service management system used by most modern Linux distributions. It is responsible for bootstrapping the system and managing system processes after the kernel loads.

### Role of systemd in Modern Linux Distributions

- Initializes the system during boot
- Manages background services (daemons)
- Handles dependencies between services
- Tracks and controls system state

Most major distributions such as Ubuntu, Debian, CentOS, Fedora, and Arch Linux use `systemd` as their default init system.

### PID 1 Explanation

When the Linux kernel starts, it launches the first user-space process with **Process ID (PID) 1**. In modern systems, this process is `systemd`.

Because it is PID 1:
- It starts other essential services
- It manages orphaned processes
- It maintains overall system stability

### Why Services Matter in System Administration and Cybersecurity

Services provide core system functionality such as:
- Web servers
- SSH remote access
- Logging systems
- Firewalls

Improperly managed services can:
- Expose attack surfaces
- Consume excessive resources
- Fail silently and impact availability

---

## 2. What Is a Service?

### Definition of a Service (Daemon)

A service, also called a daemon, is a background process that runs continuously to provide system functionality.

Services typically:
- Start at boot
- Run without user interaction
- Listen for requests or monitor system events

### Background Processes vs Services

- A **background process** may be started manually and is tied to a user session.
- A **service** is managed by `systemd` and designed to run persistently and reliably.

### Examples of Common Linux Services

- `sshd` – Secure Shell server
- `nginx` or `apache2` – Web servers
- `cron` – Task scheduler
- `firewalld` – Firewall management service

---

## 3. The systemctl Command

### Purpose of systemctl

`systemctl` is the primary command-line tool used to interact with `systemd`. It allows administrators to control services and inspect system state.

### Basic Syntax

    systemctl [action] [unit]

---

### Checking Service Status

    systemctl status ssh
    systemctl status nginx

---

### Starting a Service

    sudo systemctl start nginx

---

### Stopping a Service

    sudo systemctl stop nginx

---

### Restarting a Service

    sudo systemctl restart nginx

---

### Reloading a Service

Reload applies configuration changes without fully restarting the service (if supported).

    sudo systemctl reload nginx

---

## 4. Enabling and Disabling Services

### What "Enable" Means

Enabling a service configures it to start automatically at boot.

    sudo systemctl enable nginx

### What "Disable" Means

Disabling a service prevents it from starting at boot.

    sudo systemctl disable nginx

Disabling does not stop a currently running service.

---

## 5. Checking Service and System State

### List Active Units

    systemctl list-units

---

### List All Unit Files

    systemctl list-unit-files

---

### Check If a Service Is Active

    systemctl is-active nginx

---

### Check If a Service Is Enabled

    systemctl is-enabled nginx

---

## 6. Understanding Service Status Output

When running:

    systemctl status nginx

Important fields include:

### Loaded

Indicates whether the service unit file is properly loaded.

Example:
- loaded (/lib/systemd/system/nginx.service; enabled)

### Active

Shows whether the service is currently running.

Common states:
- active (running)
- inactive
- failed

### Enabled vs Disabled

- Enabled: Service starts automatically at boot
- Disabled: Service does not start at boot

### Failed State

Indicates the service encountered an error during startup or runtime. Logs should be checked for details.

---

## 7. Practical Examples

### Start and Enable a Web Server Service

    sudo systemctl start nginx
    sudo systemctl enable nginx
    systemctl status nginx

---

### Stop and Disable a Service

    sudo systemctl stop nginx
    sudo systemctl disable nginx

---

### Identify a Failed Service

    systemctl list-units --failed
    systemctl status service_name

---

## 8. Summary

`systemd` is the core initialization and service management system in modern Linux distributions. Using `systemctl`, administrators can start, stop, restart, enable, disable, and monitor services. Understanding service states and proper management practices is essential for maintaining system stability, reducing attack surfaces, and troubleshooting service-related issues in Linux environments.