# 32-password-hashing-basics.md

# Password Hashing Basics

## Introduction

Passwords are not stored in plain text in Linux systems to prevent immediate compromise if credential storage files are accessed. Instead, passwords are transformed into hashed representations.

Hashing is the process of converting input data into a fixed-length string of characters using a mathematical function. The original input cannot be directly retrieved from the hash.

Password hashing is a critical security control. Even if password hashes are exposed, attackers must still perform computational work to recover the original passwords.

---

## What is a Cryptographic Hash Function?

### Definition

A cryptographic hash function is a mathematical algorithm that converts input data of arbitrary size into a fixed-length output string.

### One-Way Property

Hash functions are designed to be one-way, meaning it is computationally infeasible to reverse the hash to obtain the original input.

### Deterministic Output

The same input always produces the same hash output when processed by the same algorithm.

### Fixed-Length Output

Regardless of input size, the resulting hash has a consistent, fixed length defined by the algorithm.

---

## Hashing vs Encryption

### Key Differences

- Hashing is one-way and does not use a key.
- Encryption is reversible and requires a key for decryption.

### Why Hashing Is Used for Passwords Instead of Encryption

Passwords must be verified, not decrypted. During authentication, the system hashes the entered password and compares it to the stored hash. Since there is no need to retrieve the original password, hashing is more secure than encryption for this purpose.

---

## Password Hash Storage in Linux

### Location in /etc/shadow

Password hashes are stored in the `/etc/shadow` file, which is accessible only to privileged users.

### General Structure of a Hash Entry

A typical hash field in `/etc/shadow` follows this format:

    $id$salt$hashedvalue

### Algorithm Identifiers

Common identifiers include:

- `$1$` – MD5
- `$5$` – SHA-256
- `$6$` – SHA-512

The identifier specifies the hashing algorithm used.

### Example Hash Format

    $6$randomsalt$encryptedhashvalue

---

## Salting

### Definition of a Salt

A salt is a random value added to a password before hashing.

### Why Salts Prevent Rainbow Table Attacks

Without salts, identical passwords produce identical hashes. Attackers can use precomputed tables (rainbow tables) to reverse common hashes. A unique salt ensures that even identical passwords result in different hashes, rendering precomputed attacks ineffective.

### How Salt Is Stored in Linux Hash Format

The salt appears between the algorithm identifier and the final hash value:

    $6$saltvalue$hashedoutput

The salt is stored alongside the hash but does not weaken security because it only increases attack complexity.

---

## Common Hashing Algorithms in Linux

### MD5 (Historical)

MD5 was previously used for password hashing but is now considered weak due to collision vulnerabilities and fast computation speed.

### SHA-256

Provides stronger security than MD5 with longer output length and improved resistance to cryptographic attacks.

### SHA-512

Widely used in modern Linux systems. It offers longer hash output and stronger resistance to brute force and collision attacks.

Stronger algorithms are preferred because they increase computational cost for attackers attempting password cracking.

---

## Security Considerations

### Weak Passwords and Brute Force Attacks

Even strong hashing algorithms cannot protect weak passwords. Short or common passwords are vulnerable to brute force and dictionary attacks.

### Importance of Strong Password Policies

Enforcing minimum length, complexity requirements, and regular rotation reduces the likelihood of successful attacks.

### Protecting /etc/shadow

The `/etc/shadow` file must remain readable only by privileged users. Exposure of this file allows attackers to perform offline cracking attempts.

---

## Summary

Password hashing in Linux protects user credentials by storing one-way hashed values instead of plain text passwords. Cryptographic hash functions provide deterministic, fixed-length outputs and resist reversal. Salting enhances security by preventing precomputed attacks. Strong hashing algorithms, secure file permissions, and robust password policies are essential components of Linux authentication security.