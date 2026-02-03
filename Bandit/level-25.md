# OverTheWire Bandit — Level 25 → Level 26
📘 Personal Learning Notes (Cybersecurity Student)

## Level Goal (In My Own Words)
The goal of this level is to log in to the next Bandit account using **SSH key-based authentication** instead of a password. Rather than finding a secret string inside a file, I needed to understand how private keys are used to authenticate securely and how to pass that key correctly to the SSH client.

This level marks a shift from password-based access to real-world authentication mechanisms.

## Concepts This Level Is Testing
This level focuses on several foundational Linux and security concepts:
- SSH (Secure Shell) for remote login
- Public key vs private key authentication
- File permissions on sensitive key material
- SSH client options and flags
- Understanding how authentication methods differ

It emphasizes that access control is not always about passwords.

## Why These Concepts Matter in Real Systems or Security
In real systems, password authentication is often disabled entirely in favor of SSH keys. This matters because:
- SSH keys are more resistant to brute-force attacks
- Private keys must be protected carefully
- Misconfigured permissions can cause authentication failures
- Many production servers rely exclusively on key-based access

From a security perspective, understanding SSH keys is mandatory for system administration, DevOps, and penetration testing.

## Reasoning Process Used to Approach the Level
The level description made it clear that a private SSH key was provided and that it should be used to access the next account. That immediately ruled out password-based login.

My reasoning process was:
- Identify the private key file provided
- Check its permissions to ensure SSH would accept it
- Use the SSH client with the correct flag to specify the key
- Connect to the remote service as the correct user

The challenge was not complexity, but correctness.

## Commands Used (With Clear Explanations)

Checking file permissions:
```bash
    ls -l bandit26.sshkey
```
The ls command lists files, and the -l flag shows detailed permissions. SSH requires private keys to be readable only by the owner.

Fixing key permissions:
```bash
    chmod 600 bandit26.sshkey
```
The chmod command changes file permissions. The 600 mode ensures that only the owner can read and write the key, which SSH enforces for security reasons.

Logging in using SSH with a private key:
```bash
    ssh -i bandit26.sshkey bandit26@localhost
```
The ssh command initiates a secure connection. The -i flag specifies the identity file (private key) to use for authentication instead of a password.

Each part ensures the SSH client trusts the key and the server accepts it.

## Common Mistakes or Misunderstandings
- Trying to log in with a password instead of a key
- Forgetting to restrict key file permissions
- Using the wrong username when connecting
- Assuming SSH keys work without proper flags
- Editing or moving the key file unnecessarily

A very common mistake is ignoring permission errors shown by SSH.

## What This Level Teaches for Future Levels or Real-World Usage
This level teaches:
- How key-based authentication works in practice
- Why private key protection is critical
- How SSH enforces security through file permissions
- How real servers are accessed securely without passwords

These skills are essential for managing servers, accessing cloud infrastructure, and understanding secure authentication systems.

## Key Takeaways
Passwords are not the only way in. SSH keys are a core part of real-world security, permissions matter as much as possession, and correct usage of tools is often more important than complex tricks.
