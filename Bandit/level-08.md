# Bandit Level 8

## Goal
find the password
The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

### sort command 
What it does
sort arranges lines of text in lexicographical (alphabetical) order by default.
This matters because uniq only works on adjacent lines.
If identical lines are scattered around, uniq will miss them unless you sort first.

### uniq command 
What it does
uniq filters out repeated adjacent lines.
Key idea:
uniq does not remove duplicates globally—only consecutive ones.
Common options
-c → count occurrences
-d→  show only duplicated lines
-u → show only unique lines (appearing once)

```bash
sort data.txt | uniq -u

```
very simple groups identiacl lines together then give us the only occurying 
