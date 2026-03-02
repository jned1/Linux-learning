# 51-environment-variables.md

# Environment Variables in Linux

## 1. Introduction to Environment Variables

### Definition of Environment Variables

Environment variables are dynamic key-value pairs stored by the operating system and used by processes to determine configuration settings and runtime behavior.

They are accessible to the shell and to applications launched from that shell session.

### Purpose in Linux Systems

Environment variables are used to:

- Define system paths for executable files
- Store user-specific information
- Configure application behavior
- Control language, display, and session settings

### Why They Matter in System Administration and Cybersecurity

Environment variables influence how commands and applications execute. Misconfigured variables may:

- Break system functionality
- Introduce security vulnerabilities
- Enable privilege escalation if improperly controlled

Understanding environment variables is essential for secure and predictable system behavior.

---

## 2. Viewing Environment Variables

### Using `printenv`

Displays all environment variables:

    printenv

Display a specific variable:

    printenv PATH

---

### Using `env`

Lists all current environment variables:

    env

Run a command with modified environment:

    env VAR=value command

---

### Using `echo $VARIABLE`

Display the value of a variable:

    echo $HOME
    echo $USER

---

## 3. Common Environment Variables

### PATH

Defines directories where the system searches for executable commands.

### HOME

Specifies the current user's home directory.

### USER

Stores the username of the currently logged-in user.

### SHELL

Indicates the default shell for the current user.

These variables allow programs to adapt to the user and system environment.

---

## 4. The PATH Variable in Detail

### What PATH Controls

`PATH` determines which directories are searched when a command is entered without specifying its full path.

Example:

    echo $PATH

Output may look like:

    /usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin

Directories are separated by colons (`:`).

---

### How Command Lookup Works

When a command is entered:

1. The shell searches directories listed in PATH.
2. The first matching executable found is executed.
3. If no match is found, the shell returns "command not found".

Example:

    which ls

---

### Security Relevance (PATH Hijacking)

If an attacker places a malicious executable in a directory that appears earlier in PATH, the system may execute it instead of the legitimate command.

This is known as PATH hijacking.

For security:
- Avoid including writable directories in PATH.
- Be cautious when modifying PATH, especially for root users.

---

## 5. Creating and Modifying Variables

### Creating a Temporary Variable

    MYVAR="Hello"
    echo $MYVAR

This variable exists only in the current shell session.

---

### Exporting a Variable

Exporting makes it available to child processes:

    export MYVAR="Hello"
    echo $MYVAR

---

### Unsetting a Variable

Remove a variable:

    unset MYVAR

---

## 6. Persistent Environment Variables

### Temporary vs Persistent Variables

- Temporary variables exist only in the current shell session.
- Persistent variables remain after logout and are loaded at login.

### Configuration Files

#### ~/.bashrc

- Loaded for interactive non-login shells
- Commonly used to define user-specific variables

#### ~/.profile

- Loaded at login
- Used for login session configuration

#### /etc/environment

- System-wide environment configuration
- Affects all users

### How They Load at Login

When a user logs in:

1. System-wide files are processed.
2. User-specific files are loaded.
3. Variables defined in these files become part of the session environment.

---

## 7. Practical Examples

### Adding a Custom Directory to PATH

Temporarily:

    export PATH=$PATH:/home/user/scripts

Verify:

    echo $PATH

---

### Making PATH Change Persistent

Add to ~/.bashrc:

    export PATH=$PATH:/home/user/scripts

Then reload:

    source ~/.bashrc

---

### Creating a Custom Variable for a Script

    export BACKUP_DIR="/home/user/backups"
    echo $BACKUP_DIR

---

### Verifying Variable Changes

    printenv BACKUP_DIR
    echo $PATH

---

## 8. Summary

Environment variables are key-value pairs that influence system and application behavior in Linux. Variables such as PATH, HOME, USER, and SHELL define important runtime settings. Administrators must understand how to view, create, modify, and persist these variables to maintain stable and secure systems. Proper management of environment variables helps prevent misconfigurations and reduces security risks such as PATH hijacking.