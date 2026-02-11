# OverTheWire Bandit — Level 30 → Level 31
📘 Personal Learning Notes (Cybersecurity Student)

## Level Goal (In My Own Words)

The goal of this level was to retrieve hidden information from a Git repository, but not from normal commits or branches. Instead, the secret was stored inside a Git tag.

At first, I expected another branch trick like the previous level. Instead, this level introduced a different Git object type that I had not fully explored before.

This level taught me that Git stores more than just files and branches.

---

## Concepts This Level Is Testing

This level focuses on:

- Git tags
- Understanding Git object types (commits, branches, tags)
- Inspecting repository metadata
- Exploring beyond visible file structures

Tags in Git are references that point to specific commits. They are often used to mark releases or important milestones.

---

## Why These Concepts Matter in Real Systems or Security

In real-world development:

- Tags are used to mark production releases.
- Sensitive information may accidentally be embedded in tag messages.
- Attackers inspect all Git object types, not just files.
- Metadata can reveal secrets even if the working directory looks clean.

Security audits require understanding the full structure of a repository, including its hidden layers.

Git is essentially a database of objects. If I only inspect files, I am ignoring part of the database.

---

## Reasoning Process

After cloning the repository, I checked the files and branches. Nothing unusual appeared.

Since previous levels involved Git internals, I asked myself:

- What other Git structures exist besides commits and branches?
- Is there any metadata I have not inspected?

That led me to explore tags.

---

## Commands Used (With Explanations)

Cloning the repository:
    git clone <repository_url>

This downloads the repository along with its full history and metadata.

Entering the repository directory:
    cd <repository_name>

This moves into the repository folder.

Listing available tags:
    git tag

The git tag command lists all tags in the repository.  
Tags are labels attached to specific commits.

Inspecting a tag:
    git show <tag_name>

The git show command displays detailed information about a Git object.  
When used on a tag, it shows:
- The tag message (if it exists)
- The commit it points to
- Any additional metadata

This is where the hidden information was revealed.

---

## Common Mistakes or Misunderstandings

- Ignoring tags entirely.
- Assuming tags are just version labels with no useful data.
- Only checking branches and commits.
- Not understanding that Git stores structured object types.

A common beginner assumption is that only files matter. In reality, metadata can be just as important.

---

## What This Level Teaches for Future Levels or Real-World Usage

This level reinforces:

- Git contains multiple object types.
- Tags can store messages and metadata.
- Security analysis requires full repository enumeration.
- Secrets can hide in non-obvious places.

In penetration testing, reviewing tags is standard practice when auditing repositories for exposed secrets.

Understanding Git internals moves me from basic usage toward security-aware usage.

---

## Key Takeaways

Git is more than files and branches.  
Tags are Git objects that can store meaningful data.  
Thorough inspection of repository metadata is essential in cybersecurity.
