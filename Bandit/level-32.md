# OverTheWire Bandit — Level 32 → Level 33
📘 Personal Learning Notes (Cybersecurity Student)

## Level Goal (In My Own Words)

The goal of this level was to escape from a restricted shell environment and gain access to a normal shell in order to read the password for the next level.

When I logged in, I was not placed into a standard Bash shell. Instead, I was dropped into a restricted environment that limited what commands I could run. The challenge was figuring out how to break out of that restriction safely and legally within the rules of the level.

In simple terms: I had to escape a limited shell to regain normal command execution.

---

## Concepts This Level Is Testing

This level focuses on:

- Restricted shells
- Environment limitations
- Command execution context
- Understanding how shells interpret input
- Escaping limited environments

A restricted shell is a modified shell that prevents certain actions such as changing directories, running specific commands, or executing arbitrary programs.

This level tests whether I understand that not all shells behave the same way.

---

## Why These Concepts Matter in Real Systems or Security

Restricted shells are used in:

- Shared hosting environments
- Capture The Flag challenges
- Limited access service accounts
- Secure remote systems

From a security perspective:

- Administrators use restricted shells to reduce attack surface.
- Attackers try to escape restricted environments.
- Misconfigurations can allow privilege escalation.

Understanding how shells interpret commands helps in both defending and exploiting systems.

---

## Reasoning Process

When I logged in, I noticed unusual behavior:

- Regular commands did not work as expected.
- The shell responded differently from normal Bash.

Instead of guessing randomly, I asked:

- What shell am I inside?
- How does this shell process input?
- Can I execute another shell from inside it?

I realized that the shell was interpreting uppercase commands in a specific way. By experimenting carefully and observing its behavior, I discovered that it was possible to invoke a normal shell from within the restricted one.

The key insight was understanding how command parsing worked inside that environment.

---

## Commands Used (With Explanations)

Logging into the level:
    ssh bandit32@bandit.labs.overthewire.org -p 2220

The ssh command connects to a remote server.
- bandit32 is the username.
- -p 2220 specifies the port number.

Attempting basic commands:
    ls
    whoami

These commands normally list directory contents and display the current user.  
In the restricted shell, they did not behave normally.

Invoking a standard shell:
    $0

In many Unix-like systems, $0 refers to the currently running shell or script.  
By executing it in this environment, I was able to spawn a normal Bash shell.

Once inside a standard shell, normal commands worked again.

Navigating to the home directory:
    cd ~

The cd command changes directories.
The ~ symbol represents the user’s home directory.

Reading the password file:
    cat <filename>

The cat command prints the contents of a file to the terminal.

After escaping the restricted shell, retrieving the password became straightforward.

---

## Common Mistakes or Misunderstandings

- Treating the restricted shell like a normal Bash shell.
- Assuming commands are completely blocked rather than filtered.
- Not understanding how shells interpret variables like $0.
- Trying overly complex methods instead of observing behavior.

A key lesson here was to slow down and observe how the environment behaves before attempting advanced techniques.

---

## What This Level Teaches for Future Levels or Real-World Usage

This level reinforces:

- The importance of understanding shell behavior.
- How restricted environments attempt to limit users.
- How environment misconfigurations can lead to escape.
- Why defense-in-depth is necessary.

In real-world security:

- Restricted shells must be carefully configured.
- Input validation and command filtering must be strict.
- Small oversights can allow attackers to regain full shell access.

This level moves from Git-based challenges into shell-level thinking and exploitation awareness.

---

## Key Takeaways

Not all shells are equal.  
Restricted environments rely on proper configuration.  
Understanding how shells interpret commands can allow escape from limited systems.  
Careful observation is often more powerful than complex techniques.
