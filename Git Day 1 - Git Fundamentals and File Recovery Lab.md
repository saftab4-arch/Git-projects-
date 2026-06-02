# Git Day 1 - Git Fundamentals and File Recovery Lab

## Project Overview

This lab was created to learn the core Git workflow used by developers and DevOps engineers.

The goal was to understand how Git tracks files, stores commit history, stages changes, and restores deleted files from previous commits.

By the end of this lab, I was able to:

* Initialize a Git repository
* Configure Git user information
* Track files using Git
* Create commits
* View commit history
* Delete files and recover them from previous commits
* Understand Git audit trails and version history

---

# Skills Practiced

* Git Repository Initialization
* Git Staging Area
* Git Commit Workflow
* Git History Review
* Git File Recovery
* Git Audit Trail Concepts

---

# Lab Environment

* Ubuntu Linux
* Git
* Docker Container Lab Environment

---

# Git Workflow Learned

```text
Working Directory
        ↓
git add
        ↓
Staging Area
        ↓
git commit
        ↓
Git Repository History
```

---

# Part 1 - Initialize Repository

Created a new project directory and initialized Git.

```bash
mkdir git-day1
cd git-day1

git init
```

Git created a hidden `.git` directory which stores all repository information, commit history, and configuration.

---

# Part 2 - Create and Track a File

Created a text file.

```bash
echo "Hello Git" > notes.txt
```

Checked repository status.

```bash
git status
```

Git reported the file as:

```text
Untracked
```

meaning Git could see the file but was not tracking it yet.

---

# Part 3 - Stage File

Added the file to the staging area.

```bash
git add notes.txt
```

Verified using:

```bash
git status
```

Git now reported:

```text
Changes to be committed
```

---

# Part 4 - Create First Commit

Created the first repository snapshot.

```bash
git commit -m "Initial commit"
```

This permanently saved the current version of the file into Git history.

---

# Part 5 - Review Commit History

Viewed repository history.

```bash
git log
```

Also used:

```bash
git log --oneline
```

to view a simplified commit history.

---

# Part 6 - Modify Existing File

Added additional content.

```bash
echo "Second line" >> notes.txt
```

Staged and committed the changes.

```bash
git add notes.txt

git commit -m "Added second line"
```

---

# Part 7 - Delete File

Simulated accidental file deletion.

```bash
rm notes.txt
```

Verified status.

```bash
git status
```

Git reported:

```text
deleted: notes.txt
```

---

# Part 8 - Commit Deletion

Created an audit trail by recording the deletion.

```bash
git add notes.txt

git commit -m "Deleted notes.txt"
```

Repository history now contained a deletion record.

---

# Part 9 - Restore Deleted File

Recovered the file from a previous commit.

```bash
git restore --source ceab446 notes.txt
```

Important lesson:

To restore a file, use a commit where the file exists.

Do NOT use the commit where the file was deleted.

---

# Part 10 - Commit Restoration

Created a restoration record in Git history.

```bash
git add notes.txt

git commit -m "Restored notes.txt"
```

This created a complete audit trail.

---

# Final Commit History

```text
Initial commit
↓
Added second line
↓
Deleted notes.txt
↓
Restored notes.txt
```

---

# Commands Learned

## Repository Commands

```bash
git init
git status
```

### Explanation

| Command    | Purpose                     |
| ---------- | --------------------------- |
| git init   | Create a new Git repository |
| git status | Display repository status   |

---

## Staging Commands

```bash
git add notes.txt
git add .
```

### Explanation

| Command           | Purpose                              |
| ----------------- | ------------------------------------ |
| git add notes.txt | Stage a specific file                |
| git add .         | Stage all files in current directory |

---

## Commit Commands

```bash
git commit -m "message"
```

### Flags

| Flag | Meaning        |
| ---- | -------------- |
| -m   | Commit message |

### Example

```bash
git commit -m "Added second line"
```

Creates a snapshot of staged changes.

---

## History Commands

```bash
git log
git log --oneline
```

### Flags

| Flag      | Meaning                |
| --------- | ---------------------- |
| --oneline | Compact history output |

---

## Restore Commands

```bash
git restore --source <commit-id> filename
```

### Flags

| Flag     | Meaning                                |
| -------- | -------------------------------------- |
| --source | Specify commit ID used for restoration |

### Example

```bash
git restore --source ceab446 notes.txt
```

Restores a file from a previous commit.

---

# Key Lessons Learned

* Git tracks snapshots, not individual files.
* Files must be staged before committing.
* Git commit history acts as an audit trail.
* Deleted files can be restored from previous commits.
* Restoration requires selecting a commit where the file existed.
* A commit where a file was deleted cannot be used to restore that file.
* Git enables safe recovery of accidentally deleted work.

---

# Outcome

Successfully completed a full Git lifecycle exercise:

```text
Create File
↓
Track File
↓
Commit Changes
↓
Modify File
↓
Commit Update
↓
Delete File
↓
Commit Deletion
↓
Restore File
↓
Commit Restoration
```

This lab provided hands-on experience with the fundamental Git workflow used in real-world DevOps and software engineering environments.
