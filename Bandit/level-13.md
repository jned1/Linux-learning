## Bandit Level 13
### Goal
Login to the next level without using a password.
The password for the next level is not typed manually.
Instead, access is granted using an SSH private key provided in the home directory.

### Key concept

SSH key-based authentication
Instead of password authentication, SSH can authenticate a user using a private key.
If the private key matches a public key stored on the server, access is granted automatically.
This is how most real servers are accessed in production environments

#### Important details

The private key file is readable only by the owner
SSH refuses to use keys with insecure permissions
The -i flag is used to specify an identity (private key) file
Incorrect permissions will cause SSH to reject the key.
Solution I used
```bash
ssh -i sshkey.private bandit14@localhost -p 2220
```

If permissions were incorrect:
```bash
chmod 600 sshkey.private
```
### What you learned

SSH does not always rely on passwords
Private key permissions are critical for security
The -i flag allows manual key selection
This mirrors real-world server authentication

### Why this level matters

Password-based SSH is discouraged on real systems.
Key-based authentication is:
more secure
resistant to brute force attacks
standard practice in DevOps and cybersecurity