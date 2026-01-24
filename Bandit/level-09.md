# Bandit Level 9

## Goal
find the password
The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

### solution 
The strings command finds human-readable strings in files. Specifically, it prints sequences of printable characters. Its main use is for non-printable files like hex dumps or executables.

```bash
strings data.txt | grep ===
```
