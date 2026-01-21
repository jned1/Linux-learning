# TryHackME (learn the linux fundamental part -3.1)
## Overview :
in this file we will showcase some useful uitilities and applications that you are likely to use day-to-day .
going to advanced your linux-fu skills by learning about automation , package management , and service/application logging 

Everything here reflects what I studied, tested, and verified myself.

## First :
**deploy linux machine and remotly connect using ssh**
## Second (Termianl Text Editors ):
after we learned simple way to creat and to append text to the file using echo and >,>> , now we will go for nano and vim terminal text editors
### nano
**what is nano**: nano is a simple, terminal-based text editor designed to be easy and forgiving. When you open a file with nano, you can immediately start typing. The most important commands are always shown at the bottom of the screen.
**What nano does well:**
- Easy to learn in minutes.
- Clear on-screen shortcuts (^O to save, ^X to exit).
- Perfect for quick edits of configuration files, notes, or scripts.
- Installed by default on many Linux distributions.
### Vim
**what is Vim:**
Vim (Powerful, Modal Text Editor) ,vim (Vi IMproved) is a highly powerful text editor built around efficiency and keyboard-driven workflows. It uses modes, which is the key idea that confuses beginners and empowers experts.
**Core idea:**
- Normal mode: navigate and manipulate text.
- Insert mode: type text.
- Command mode: save, quit, search, automate.
**Why professionals love vim:**
- Extremely fast once mastered.
- Works everywhere (almost every Linux system has it).
- Ideal for programming, config editing, and remote servers.
- Infinitely extensible via plugins and scripting.

***
## Third (General & Useful Utilities):
### Downloading Files Using (wget)
**what is wget :**
wget is a non-interactive command-line tool used to download files from the web. “Non-interactive” means it works without a graphical interface and doesn’t need user input once started. This makes it perfect for servers, scripts, automation, and… late-night Linux adventures over SSH.
At a deep level, wget speaks common internet protocols like HTTP, HTTPS, and FTP, asks a remote server for a file, and saves that file to your local system. Simple idea, powerful consequences
```bash 
wget https://example.com/file.zip
```
**note** :u can use with this command alot of flags so i u want to go advance go man wget

### Transferring Files From your Host - SCP(SSH) :
**What SCP Is :**
scp stands for secure copy. It’s a command-line tool that lets you copy files securely between different computers over a network, using SSH (Secure Shell) for encryption and authentication. That means both the file and the password (or SSH key) are encrypted during the transfer. SSH must be running on the machines involved.

**Copying a Local File to a Remote Server:**
To upload a file from your local machine to a remote host:
```bash
scp myfile.txt user@192.168.1.100:/home/user/
```
This sends myfile.txt into the /home/user/ directory on the remote machine. The remote server will prompt you for the user’s password (unless you use SSH keys).

**Copying a Remote File to Your Local Machine**
To pull a file from a remote server to your local system:
```bash
scp user@192.168.1.100:/home/user/myfile.txt .
```
The . at the end means “current directory” on your local machine.


### Receving files from your host-WEB 
#### Receiving files from your host via the web (HTTP/HTTPS)

This is the classic setup: your host machine shares a file using a web server, and your Linux machine downloads it using the terminal. No SSH, no login—just the web doing what it was invented to do: moving files around.

At a conceptual level, your host becomes a temporary web server, and your Linux system becomes a client that asks for a file using HTTP or HTTPS.
### python3 -m http.server
This command turns your machine into a simple HTTP web server in seconds. No installation, no configuration files, no ceremony. It is one of those tools that looks innocent but teaches you a lot about how the web actually works.

**What it does**

python3 -m http.server starts a basic HTTP server that serves files from the current directory over the network.
Under the hood:

- Python loads its built-in http.server module

- It listens for HTTP requests (GET requests from browsers, wget, curl, etc.)

- When a client asks for a file, the server sends it back over HTTP

- This is a real web server, just a very small and honest one.

Basic usage

From the directory you want to share:
```bash
python3 -m http.server
```

**Mental model**
**scp → locked tunnel**
**python3 -m http.server → open table**
**wget / curl → hands reaching across the table**

## Fourth (Processes 101):
**Processes 101**
A Linux system is never “idle.” Even when the screen is quiet, dozens (often hundreds) of processes are alive, running, sleeping, or waiting. Understanding processes is understanding how Linux breathes.

### What is a process?
A process is a running instance of a program.
Key idea:
A program is a file on disk (for example: /bin/ls)
A process is that program in memory, actively executed by the CPU

When you type:

ls
Linux:
1) Loads the ls program into memory
2) Assigns it a Process ID (PID)
3) Runs it
4) Cleans it up when it finishes
Some processes live for milliseconds. Others (like system services) run for days or months.

**Why processes matter :**

Processes:
Compete for CPU, memory, disk, and network
Can be controlled, paused, or killed
Are the foundation of multitasking
Are often the first clue in debugging or security incidents
In cybersecurity, “something weird is happening” often translates to:
“There’s a suspicious process running.”
### Viewing processes with ps
**ps (process status)**
The ps command shows a snapshot of processes at a single moment in time.
Basic usage:
```bash
ps
```
This only shows processes started in your current terminal session.

**ps aux (the classic)**
This is the most common and useful form.
```bash
ps aux
```
What it means:
a → processes from all users
u → user-oriented format (shows owner, CPU, memory)
x → include processes without a terminal (daemons)

Important columns:
USER → who owns the process
PID → process ID
%CPU → CPU usage
%MEM → memory usage
COMMAND → what is actually running

**Real-time process viewing with** **top**
```bash
top
```
Unlike ps, top is dynamic. It refreshes every few seconds and shows what is happening right now.
What top shows:
Load average (system stress)
CPU usage (user vs system time)
Memory and swap usage
A live list of processes sorted by activity
Key controls:

q → quit

k → kill a process (by PID)

P → sort by CPU

M → sort by memory

**htop (human-friendly top)**
htop is an improved, interactive process viewer. It is not always installed by default, but it is widely used.
```bash
htop
```

Why people love it:
- Color-coded output
- Mouse support
- Easy scrolling
- Simple process tree view
- Kill processes without memorizing PIDs
Think of it as top with empathy.

### Managing processes in Linux

Seeing processes is only half the story. Managing processes is about control: starting them, stopping them, pausing them, prioritizing them, and understanding how Linux negotiates peace between competing workloads.

#### Signals: how Linux talks to processes

A signal is a small message sent to a process to tell it something happened or to ask it to do something.
Common signals:
1) SIGTERM (15): polite request to stop
2) SIGKILL (9): immediate termination, no cleanup
3) SIGSTOP: pause the process
4) SIGCONT: resume a stopped process

#### Stopping processes with kill

Despite the name, kill does not always kill. It sends a signal.
Basic usage:
```bash
kill PID
```
By default, this sends SIGTERM. The process can clean up before exiting.

Force kill:
```bash
kill -9 PID
```
This sends SIGKILL. The kernel ends the process immediately.
Use this only when a process refuses to cooperate.

### How processes start in Linux
Linux does not “just run programs.” It follows a very strict birth ritual. Once you see that ritual, processes stop feeling mysterious and start feeling engineered.
1. The first process: PID 1
When a Linux system boots, the kernel is loaded first. The kernel then starts one single user-space process:
PID 1 → usually systemd on modern distributions
Every other process on the system is either:
- a direct child, or
- a descendant of PID 1
If PID 1 dies, the system panics. That tells you how fundamental it is.

2. Fork + exec: how a process is born
Almost all processes are created using a two-step pattern:
fork()
The parent process creates a copy of itself.
exec()
The child replaces its memory with a new program.

This is why:
Shells can start programs
Services can spawn workers
Malware hides as child processes
This mechanism is ancient, stable, and brutally efficient.

### namespaces
A namespace is a kernel feature that makes a process believe it has its own private view of the system.
Namespaces isolate things like:
Process IDs (PID namespace)
Network interfaces (NET namespace)
Mount points (MNT namespace)
Users and permissions (USER namespace)

Inside a namespace:
A process might think it is PID 1
It may only see its own processes
It may have “root” privileges that don’t exist outside
This is the foundation of containers (Docker, Podman, Kubernetes).

### How services start on boot (systemd)
Modern Linux systems use systemd to manage services.
systemd:
Starts services in parallel
Respects dependencies
Restarts crashed services
Controls what runs at boot
A service is just a managed process with rules.

### Enabling a service to start at boot
To start a service automatically when the system boots:
```bash
sudo systemctl enable ssh
```
What this really does:
Creates symbolic links
Tells systemd: “start this when reaching the boot target”

Start it immediately:
```bash
sudo systemctl start ssh
```
Check status:
```bash
systemctl status ssh
```

### Backgrounding and foregrounding in Linux

Linux assumes something simple and profound: you are capable of doing more than one thing at a time. Backgrounding and foregrounding are how the shell lets you juggle processes without losing control.
This is called job control, and it lives mostly in the shell (like bash), not in the kernel itself.
Foreground vs background (the core idea)

**Foreground process**
A process attached to your terminal.
It receives your keyboard input and blocks the shell until it finishes.

**Background process**
A process running without blocking the terminal.
You get your prompt back while it keeps working.

Only foreground jobs can read from the keyboard.

#### Running a command in the background
Add & at the end:
```bash
sleep 60 &
```
#### Pausing a foreground process
While a process is running in the foreground:
Ctrl + Z
This sends SIGSTOP and pauses the process.

Example:
```BASH
ping google.com
Ctrl + Z
```
#### Resuming a process
Bring it back to the foreground:
```BASH
fg %1
```
