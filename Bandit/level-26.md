# OverTheWire Bandit — Level 26 → Level 27
📘 Personal Learning Notes (Cybersecurity Student)

## Level Goal (In My Own Words)
The goal of this level is to escape from a **restricted login environment** and obtain an interactive shell. Logging in works, but the system immediately drops me into a limited program instead of a normal shell. To progress, I had to understand how that program works and how to break out of it safely.

This level is about *escaping confinement*, not authentication.

## Concepts This Level Is Testing
This level focuses on several important Linux fundamentals:
- SSH forced commands
- Restricted shells and limited environments
- Pager programs (like `less`)
- Terminal behavior and window size
- Program escape techniques
- Understanding how interactive programs spawn shells

It tests awareness, not brute force.

## Why These Concepts Matter in Real Systems or Security
In real systems, administrators often restrict users by:
- Forcing commands in SSH
- Limiting shells
- Allowing access only to specific programs

From a security perspective:
- Many restricted environments rely on tools that were not designed to be security sandboxes
- Pager programs and editors often allow shell execution
- Escaping a restricted shell is a common privilege escalation technique

Understanding this helps both defenders and attackers recognize weak containment strategies.

## Reasoning Process Used to Approach the Level
After logging in, I noticed something unusual: I did not get a normal shell prompt. Instead, a program started automatically and exited quickly. That suggested a **forced command**.

Repeating the login carefully showed that the program behaved like a pager. Pager programs often allow:
- Command execution
- Editor mode
- Shell escapes

The challenge was that the program exited too fast to interact with. That led me to think about **terminal size**. If the output does not fit on the screen, pagers stay open.

By resizing the terminal window to be very small before logging in, I forced the pager to remain active long enough to interact with it.

Once inside, I used built-in features of the program to escape into a shell.

## Commands Used (With Clear Explanations)

Resizing the terminal window:
This is done manually by shrinking the terminal window so the output cannot fit on one screen. This forces pager programs to remain open.

Logging in with SSH:
```bash
    ssh -i bandit26.sshkey bandit26@localhost
```
The ssh command connects to the remote system using key-based authentication. The -i flag specifies the private key file.

Interacting with the pager:
Inside the pager, editor-style commands are available. Some pagers allow spawning a shell directly from their command interface.

Launching a shell from within the program:
```bash
    /bin/sh
```
This starts a basic shell from inside the restricted program, giving interactive command access.

Switching to a full shell:
```bash
    exec /bin/bash
```
The exec command replaces the current shell with another one, giving a more complete environment.

Each step relies on understanding how interactive programs behave, not on exploiting bugs.

## Common Mistakes or Misunderstandings
- Assuming login failure when access actually succeeds
- Not recognizing the restricted environment
- Letting the program exit before interacting with it
- Forgetting that terminal size affects program behavior
- Treating pagers as harmless viewers

A common misunderstanding is thinking restriction equals security.

## What This Level Teaches for Future Levels or Real-World Usage
This level teaches:
- How forced commands work in SSH
- Why restricted shells are often weak
- How interactive programs can be abused unintentionally
- The importance of understanding tool features deeply
- How small environmental details can change system behavior

These lessons are directly applicable to real-world penetration testing and system hardening.

## Key Takeaways
Restrictions built on general-purpose tools are fragile. Understanding how programs really work allows escape from environments that look locked down. Observation and patience are more powerful than force.
