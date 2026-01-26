# Bandit Level 10

## Goal
find the password
The password for the next level is stored in the file data.txt, which contains base64 encoded data.
### solution 
Base64 is a binary-to-text encoding scheme. It can often be recognised by equal signs at the end of the data. However, this is not always the case. Linux has a command called base64 that allows for encoding and decoding in Base64. For decoding, we need to use the flag -d.

```bash
base64 -d data.txt
```
