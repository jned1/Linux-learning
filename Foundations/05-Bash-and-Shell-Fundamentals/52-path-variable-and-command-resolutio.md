# 52-path-variable-and-command-resolution.md

# PATH Variable and Command Resolution

## 1. Introduction

### What is the PATH Variable?

The `PATH` variable is an environment variable that defines a list of directories where the shell searches for executable commands. The directories are separated by colons (`:`).

### Why Command Resolution Matters in Linux

When a user types a command without specifying its full location, the shell must determine which executable file to run. This process is called command resolution.

### Importance in System Administration and Cybersecurity

Understanding how command resolution works is essential for:

- Predictable system behavior
- Avoiding command conflicts
- Preventing execution of malicious binaries
- Securing privileged environments

Improper PATH configuration can lead to security vulnerabilities.

---

## 2. How Command Resolution Works

### What Happens When a User Types a Command

When a command is entered (e.g., `ls`), the shell follows these steps:

1. Check if the command is a shell built-in.
2. Check if the command matches an alias.
3. Search each directory listed in the `PATH` variable, in order.
4. Execute the first matching executable found.
5. If no match is found, return "command not found".

---

### Search Order Using PATH

The shell searches directories from left to right as listed in `PATH`.

Example structure:

    /usr/local/bin:/usr/bin:/bin

If a command exists in both `/usr/local/bin` and `/usr/bin`, the one in `/usr/local/bin` will be executed.

---

### Absolute Path vs Relative Path vs Command Name

- **Absolute path**: Full path starting from root (`/`).

      /bin/ls

- **Relative path**: Path relative to current directory.

      ./script.sh

- **Command name only**: Relies on PATH lookup.

      ls

Using absolute paths bypasses PATH search.

---

## 3. Viewing the PATH Variable

Display PATH using echo:

    echo $PATH

Display PATH using printenv:

    printenv PATH

---

## 4. Command Lookup Tools

### which

Displays the path of the executable that will run.

    which ls
    which python3

---

### whereis

Shows binary, source, and manual page locations.

    whereis ls

---

### type (Built-in)

Indicates how the shell interprets a command.

    type ls
    type cd
    type python3

This helps determine whether a command is built-in, an alias, or an external binary.

---

## 5. Order of Precedence

### Multiple Binaries with the Same Name

If multiple executables share the same name, the one located in the earliest directory in PATH is used.

Example:

    echo $PATH
    which ls

If a custom version of `ls` exists in `/home/user/bin` and that directory appears before `/bin`, it will take precedence.

---

### Demonstration Example

Create a custom directory and test precedence:

    mkdir ~/mybin
    echo 'echo Custom LS' > ~/mybin/ls
    chmod +x ~/mybin/ls
    export PATH=~/mybin:$PATH
    ls

The custom version will execute if it appears first in PATH.

---

## 6. Security Implications

### PATH Hijacking Concept

PATH hijacking occurs when an attacker places a malicious executable in a directory that appears earlier in PATH than legitimate system directories.

If the system executes that malicious file instead of the intended binary, it may lead to privilege escalation or system compromise.

---

### Risks of Writable Directories in PATH

If directories in PATH are writable by non-privileged users, attackers may:

- Replace system commands
- Insert malicious executables
- Intercept administrative operations

---

### Root PATH Handling

The root user should:

- Avoid including user-writable directories in PATH
- Use absolute paths for sensitive commands
- Keep PATH minimal and controlled

---

### Basic Best Practices

- Avoid adding `.` (current directory) to PATH
- Keep system directories before user directories for administrative accounts
- Regularly review PATH configuration

---

## 7. Modifying PATH

### Temporarily Modifying PATH

    export PATH=/new/directory:$PATH

This change applies only to the current session.

---

### Adding a Directory to PATH

Append a directory:

    export PATH=$PATH:/home/user/scripts

Prepend a directory:

    export PATH=/home/user/scripts:$PATH

---

### Verifying Changes

    echo $PATH
    which script_name

---

## 8. Practical Examples

### Creating a Custom Script and Executing via PATH

Create a script:

    mkdir ~/scripts
    nano ~/scripts/hello.sh

Add content:

    #!/bin/bash
    echo "Hello from custom script"

Make it executable:

    chmod +x ~/scripts/hello.sh

Add to PATH:

    export PATH=$PATH:~/scripts

Run it:

    hello.sh

---

### Observing Command Resolution Behavior

Check command source:

    which hello.sh
    type hello.sh

Modify PATH order and observe which binary executes.

---

## 9. Summary

The PATH variable controls how Linux resolves commands entered in the shell. The shell searches directories in PATH sequentially and executes the first matching binary. Understanding command resolution helps prevent command conflicts, improves troubleshooting, and reduces security risks such as PATH hijacking. Proper PATH configuration is essential for stable and secure Linux system operation.