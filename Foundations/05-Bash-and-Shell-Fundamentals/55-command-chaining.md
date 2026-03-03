# 55-command-chaining.md

## 1. Introduction

### What is Command Chaining?

Command chaining in Bash allows multiple commands to be executed on a single command line using specific operators. These operators control how commands are executed and determine whether subsequent commands depend on the success or failure of previous ones.

Chaining improves efficiency and allows simple execution logic directly in the terminal.

### Difference Between Chaining and Piping

Although they may appear similar, chaining and piping serve different purposes:

- **Chaining** controls execution flow between commands.
- **Piping (`|`)** sends the output of one command as input to another.

In simple terms:
- Chaining controls *when* commands run.
- Piping controls *what data* flows between commands.

### Why Chaining Is Useful in Linux Workflows

Command chaining:

- Saves time by running multiple commands in one line
- Introduces simple conditional logic
- Improves terminal productivity
- Helps create safer administrative workflows

It is commonly used in system administration and cybersecurity tasks.

---

## 2. Sequential Execution (`;`)

### Syntax and Behavior

The semicolon (`;`) runs commands sequentially:

    command1 ; command2

Bash executes `command1` and then immediately executes `command2`, regardless of whether the first command succeeds or fails.

### Commands Run Regardless of Success or Failure

The `;` operator does not check exit status. Every command runs in order.

### Example Commands

    pwd ; date

    mkdir test ; cd test

    ls /invalid_directory ; echo "This command still runs"

---

## 3. Conditional Execution (`&&`)

### Syntax and Behavior

The `&&` operator runs the second command only if the first command succeeds:

    command1 && command2

### Exit Status Explanation (Basic)

Every Linux command returns an **exit status**:

- `0` indicates success
- Any non-zero value indicates failure

When using `&&`, Bash checks if the first command returns `0`. If it does, the second command runs. If not, the second command is skipped.

### Example Commands

    mkdir project && cd project

    touch file.txt && echo "File created successfully"

    ls /etc && echo "Directory exists"

If the first command fails, the second command will not execute.

---

## 4. Conditional Execution (`||`)

### Syntax and Behavior

The `||` operator runs the second command only if the first command fails:

    command1 || command2

If `command1` returns a non-zero exit status, `command2` is executed.

### Example Commands

    ls /nonexistent || echo "Directory not found"

    mkdir existing_dir || echo "Directory may already exist"

    grep root /etc/passwd || echo "User not found"

This operator is commonly used for error handling or fallback actions.

---

## 5. Combining Operators

### Mixing `&&` and `||`

Operators can be combined to create more controlled execution flows:

    command1 && command2 || command3

### Logical Flow Explanation

The execution logic works as follows:

- If `command1` succeeds, `command2` runs.
- If `command1` fails, `command3` runs.
- If `command2` fails, `command3` also runs.

### Example Commands

    mkdir test && cd test || echo "Operation failed"

    ls /etc && echo "Success" || echo "Failure"

    grep admin /etc/passwd && echo "User found" || echo "User missing"

---

## 6. Practical Examples

### Create Directory and Move Into It Safely

    mkdir secure_folder && cd secure_folder

This ensures you only enter the directory if it was created successfully.

### Run Command and Handle Failure

    cp important.txt /backup/ || echo "Backup failed"

If the copy operation fails, a message is displayed.

### Install Package and Verify Success (Generic Example)

    sudo apt install package_name && echo "Installation successful" || echo "Installation failed"

This provides immediate feedback based on the installation result.

---

## 7. Basic Security Relevance

### Safe Execution Patterns

Using `&&` helps prevent unintended actions:

    cd /secure/location && rm old_file

This prevents file deletion if changing directories fails.

### Avoiding Unintended Command Execution

Using `;` can cause commands to run even after a failure. Conditional operators reduce this risk by verifying success before continuing.

### Importance in Automation and Scripting

Understanding exit statuses and chaining operators is essential for:

- Reliable automation
- Safe system updates
- Controlled administrative tasks
- Reducing configuration errors

In cybersecurity environments, predictable command execution is critical.

---

## 8. Summary

Command chaining allows multiple commands to be executed in a single line while controlling their execution behavior.

Key operators:

- `;` runs commands sequentially, regardless of outcome.
- `&&` runs the next command only if the previous one succeeds.
- `||` runs the next command only if the previous one fails.

Understanding exit status is fundamental when using conditional chaining. Command chaining improves efficiency, safety, and reliability in Linux administration and cybersecurity workflows.