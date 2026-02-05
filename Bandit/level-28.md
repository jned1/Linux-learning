# OverTheWire Bandit — Level 28 → Level 29
📘 Personal Learning Notes (Cybersecurity Student)

## Level Goal (In My Own Words)
The goal of this level is to find information that is **not present in the current version of a project**, but still exists in its version control history. Instead of looking at files as they are now, I had to think about how files change over time and how old data can still be recovered.

This level taught me to look backward, not forward.

## Concepts This Level Is Testing
This level focuses on:
- Git version history
- Commit tracking
- Differences between file versions
- Understanding how deleted or modified data can persist
- Inspecting changes rather than static files

It highlights that data removal does not always mean data disappearance.

## Why These Concepts Matter in Real Systems or Security
In real-world security:
- Secrets are often accidentally committed and later removed
- Git repositories preserve history by design
- Attackers routinely inspect commit history for credentials
- Sensitive data can leak even if it is no longer visible

Understanding Git history is critical for code audits, incident response, and secure development practices.

## Reasoning Process Used to Approach the Level
After cloning the repository, I noticed that the visible files did not contain anything useful. That suggested the information might have existed before and was removed.

Instead of searching blindly, I shifted my thinking to:
- What changed in this project?
- What was removed or edited?
- Can I inspect earlier versions?

This led me to explore Git’s history features to compare file versions across commits.

## Commands Used (With Clear Explanations)

Cloning the repository:
    git clone <repository_url>
This downloads the entire repository, including all past commits.

Entering the repository directory:
    cd <repository_name>
This moves into the project directory so Git commands can be used.

Checking repository status:
    git status
This shows the current state of the working tree and confirms the repository is clean.

Viewing commit history:
    git log
This displays a list of commits, showing how the project changed over time.

Inspecting file differences:
    git diff <commit1> <commit2>
The git diff command compares two states of the repository and highlights what changed between them.

Reviewing earlier file versions:
    git show <commit>:<filename>
This shows the contents of a file as it existed in a specific commit.

Each of these commands helped reconstruct what was removed without guessing.

## Common Mistakes or Misunderstandings
- Only reading the current files and stopping there
- Assuming deleted data is gone forever
- Ignoring commit history
- Not understanding how Git tracks changes
- T
