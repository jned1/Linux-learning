# 13-symbolic-links-and-hard-links.md

# Symbolic Links and Hard Links

## Introduction

In Linux, links are filesystem objects that reference existing files. Instead of duplicating file content, links provide alternative access paths to the same data.

Links exist to improve storage efficiency, maintain compatibility, simplify file management, and provide flexible referencing within the filesystem.

Understanding link behavior is essential for system administration and cybersecurity analysis, as improper handling can introduce security risks.

---

# Inodes (High-Level Overview)

## Define Inode

An inode (index node) is a data structure used by Linux filesystems to store metadata about a file.

An inode contains:
- File permissions
- Ownership
- Timestamps
- File size
- Pointers to data blocks

It does not store the filename. Filenames are stored in directory entries that reference inodes.

---

## How Files Are Associated with Inodes

When a file is created:
- The filesystem assigns it an inode.
- A directory entry maps the filename to that inode.

Multiple filenames can reference the same inode.

---

## Why Inodes Matter for Understanding Links

Hard links directly reference the same inode as the original file. Symbolic links reference a file path instead of an inode. This distinction explains their behavior during file modification and deletion.

---

# Hard Links

## Definition

A hard link is an additional directory entry that points to the same inode as an existing file.

## How They Work

When a hard link is created:
- No new inode is generated.
- Both filenames reference the same inode.
- File data exists only once on disk.

Changes made through one name are reflected in the other because both reference the same inode.

---

## Relationship to Inodes

Hard links share:
- The same inode number
- The same data blocks
- The same metadata

The file is only removed from disk when all hard links to that inode are deleted.

---

## Limitations

- Hard links must exist within the same filesystem.
- Hard links cannot be created for directories (to prevent filesystem loops).

---

## Example Creation Using ln

    ln original.txt hardlink.txt

This creates a second filename pointing to the same inode as `original.txt`.

---

# Symbolic Links (Soft Links)

## Definition

A symbolic link (soft link) is a special file that contains a reference to another file's path.

## How They Work

A symbolic link stores the pathname of the target file. When accessed, the system follows the stored path to locate the target.

Unlike hard links, symbolic links have their own inode.

---

## Difference from Hard Links

- Symbolic links reference a path, not an inode.
- They can span across different filesystems.
- They can link to directories.

---

## Behavior if Original File Is Deleted

If the original file is deleted:
- A hard link remains functional as long as at least one link to the inode exists.
- A symbolic link becomes broken (dangling) because the referenced path no longer exists.

---

## Example Creation Using ln -s

    ln -s original.txt symlink.txt

This creates a symbolic link named `symlink.txt` pointing to `original.txt`.

---

# Key Differences Between Hard and Symbolic Links

## Inode Behavior

- Hard links share the same inode as the original file.
- Symbolic links have their own inode and reference a file path.

---

## Cross-Filesystem Support

- Hard links cannot cross filesystem boundaries.
- Symbolic links can reference files on different filesystems.

---

## Directory Linking

- Hard links cannot link directories.
- Symbolic links can link directories.

---

## Deletion Impact

- Deleting the original file does not remove data if a hard link exists.
- Deleting the original file causes symbolic links to become invalid.

---

# Security Implications

## Symbolic Link Attacks

Symbolic links may be exploited in race condition attacks, where an attacker replaces a legitimate file path with a link to a sensitive file. This can cause privileged programs to operate on unintended targets.

---

## Privilege Escalation Scenarios

If a privileged process writes to a predictable file path without proper validation, an attacker may create a symbolic link to redirect output to sensitive files, potentially leading to privilege escalation.

---

## Log File Redirection Risks

Improper handling of symbolic links in log directories may allow attackers to redirect logs or overwrite critical files.

---

## Importance During Forensic Analysis

During investigations, analysts must:
- Identify unexpected symbolic links
- Check inode numbers to confirm hard link relationships
- Detect broken links that may indicate tampering

Understanding link structures helps determine whether files are independently stored or simply alternate references.

---

# Summary

Hard links and symbolic links provide alternative methods of referencing files in Linux. Hard links reference the same inode and share file data, while symbolic links reference file paths and operate as independent special files.

Their differences in inode behavior, filesystem scope, and deletion impact have important security implications. Proper understanding of link mechanisms supports secure configuration, vulnerability assessment, and forensic analysis in Linux environments.