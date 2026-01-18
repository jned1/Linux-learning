# Bandit Level 2

## Goal
To find the password stored at file named "--spaces in this file name--" 

## Note 
so in this problem we have the file name prefixed with hyphen and have spaces so the solution is simple 
1) before the hyphen(-) : ./ #just in the start of the name
2) before every space need to put backslash(\)

## Commands used
```bash
ssh bandit2@bandit.labs.overthewire.org -p 2220 #using the password u found last level
ls -al 
cat ./--spaces\ in\ this\ file\ name--
