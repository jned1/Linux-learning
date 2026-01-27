# Bandit Level 11

## Goal
find the password
The password stored in :
file name data.txt
all lowercase and uppercase letters are rotated by 13 positions (ROT13)
Base64 is a binary-to-text encoding scheme. It can often be recognised by equal signs at the end of the data. However, this is not always the case. Linux has a command called base64 that allows for encoding and decoding in Base64. For decoding, we need to use the flag -d.

## What is ROT13
ROT13 is a simple letter substitution cipher
each letter is replaced by the letter 13 positions after it

example:
A → N
N → A
a → n
n → a
numbers and symbols are not changed

## solutions i used
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

```
## what you learned
simple ciphers can be broken with basic tools
tr is useful for character substitution
pipelines make decoding easy