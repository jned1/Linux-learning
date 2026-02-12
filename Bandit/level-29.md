# OverTheWire Bandit — Level 29 → Level 30
📘 Personal Learning Notes (Cybersecurity Student)

## Level Goal (In My Own Words)

The goal of this level was to retrieve information that was not available in the default branch of a Git repository. Instead of searching through files or commit history like the previous level, I had to explore different branches inside the repository.

In simple terms: the secret was hidden in another branch.

This level forced me to think beyond just “files” and start thinking in terms of Git structure.

---

## Concepts This Level Is Testing

This level focuses on:

- Git branches
- Understanding the difference between local and remote branches
- Switching between branches
- Exploring alternative development paths in a repository

It tests whether I understand that Git is not just a timeline (history), but also a tree with multiple parallel paths.

---

## Why These Concepts Matter in Real Systems or Security

In real-world development:

- Developers often create feature branches.
- Sensitive information may accidentally be committed in a test or development branch.
- Hidden branches can contain staging credentials or debugging data.
- Public repositories may expose non-main branches.

Attackers frequently enumerate branches to find secrets that are not visible in the main branch.

If I only inspect the default branch, I might miss critical data.

---

## Reasoning Process

After cloning the repository, I initially checked the visible files. Nothing useful appeared in the default branch.

From the previous level, I learned to think in terms of Git structure. This time I asked:

- Are there other branches?
- Is something hidden outside the current working branch?

So instead of focusing on file content, I started inspecting the repository structure.

---

## Commands Used (With Explanations)

Cloning the repository:
    git clone <repository_url>

This downloads the full Git repository, including all branches.

Entering the repository directory:
    cd <repository_name>

This moves into the project folder so Git commands can be executed.

Listing local branches:
    git branch

This shows branches available locally. At first, only the default branch is visible.

Listing all branches including remote:
    git branch -a

The -a flag stands for "all".  
This displays both local and remote branches. This was the key step that revealed additional branches.

Switching to another branch:
    git checkout <branch_name>

The git checkout command switches the working directory to another branch.  
After switching, the file contents change to match that branch’s state.

Viewing file contents:
    cat <filename>

The cat command prints file contents to the terminal.

Once I switched to the correct branch, the information I was looking for became visible.

---

## Common Mistakes or Misunderstandings

- Only checking the default branch.
- Not using git branch -a to see remote branches.
- Forgetting that cloning includes all branches.
- Confusing commit history with branch structure.
- Thinking Git is linear instead of branching.

A beginner mistake is assuming there is only one version of a project at a time.

---

## What This Level Teaches for Future Levels or Real-World Usage

This level reinforces:

- Git repositories can contain multiple parallel development paths.
- Sensitive information may exist in non-production branches.
- Enumeration is critical in cybersecurity.
- Always inspect the full attack surface.

In penetration testing or security auditing, checking only what is immediately visible is not enough.

Branches matter.

---

## Key Takeaways

Git is not just history — it is a multi-branch system.  
Secrets can hide in alternate branches, not just past commits.  
Enumeration and structured thinking are essential skills in cybersecurity.
