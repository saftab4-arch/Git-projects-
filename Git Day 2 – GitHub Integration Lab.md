# Git Day 2 – GitHub Integration Lab

## Project Overview

This lab focused on connecting a local Git repository to GitHub and understanding how local and remote repositories communicate.

The objective was to learn how to upload local commits to GitHub, retrieve changes from GitHub, and understand the relationship between local branches and remote tracking branches.

---

# Skills Practiced

* GitHub Repository Creation
* Git Remote Management
* Git Push Operations
* Git Pull Operations
* Remote Tracking Branches
* Local vs Remote Repositories
* GitHub Synchronization

---

# Lab Environment

* Ubuntu Linux
* Git
* GitHub

---

# Learning Objectives

Understand:

```text
Local Repository
        ↓
Git Push
        ↓
GitHub Repository
```

and

```text
GitHub Repository
        ↓
Git Pull
        ↓
Local Repository
```

---

# Part 1 – Create Local Repository

Created a new lab directory.

```bash
mkdir git-day2
cd git-day2
```

Initialized Git.

```bash
git init
```

Verified the repository.

```bash
ls -la
```

Observed:

```text
.git
```

The hidden `.git` directory stores repository metadata, commit history, branches, and Git configuration.

---

# Part 2 – Create README File

Created a README file.

```bash
echo "Git Day 2 - GitHub Integration" > README.md
```

Verified contents.

```bash
cat README.md
```

---

# Part 3 – Check Repository Status

Verified repository status.

```bash
git status
```

Observed:

```text
Untracked files:
README.md
```

Meaning Git could see the file but was not yet tracking it.

---

# Part 4 – Stage File

Added README.md to the staging area.

```bash
git add README.md
```

Verified status.

```bash
git status
```

Observed:

```text
Changes to be committed
```

Meaning the file was staged and ready for a commit.

---

# Part 5 – Create First Commit

Created the initial repository snapshot.

```bash
git commit -m "Initial commit"
```

Verified history.

```bash
git log --oneline
```

Observed:

```text
Commit-ID Initial commit
```

---

# Part 6 – Verify Remote Repositories

Checked whether the repository was connected to GitHub.

```bash
git remote -v
```

Observed:

```text
(no output)
```

Meaning no remote repository was configured.

---

# Part 7 – Connect Repository to GitHub

Connected local Git repository to GitHub.

```bash
git remote add origin https://github.com/USERNAME/git-day2-lab.git
```

Verified connection.

```bash
git remote -v
```

Observed:

```text
origin URL (fetch)
origin URL (push)
```

---

# Understanding Fetch and Push

```text
Fetch
GitHub → Local Repository
```

Downloads information from GitHub.

```text
Push
Local Repository → GitHub
```

Uploads commits to GitHub.

---

# Part 8 – Push Repository to GitHub

Uploaded local commits.

```bash
git push -u origin main
```

Explanation:

```text
git push
↓
Upload commits

-u
↓
Set upstream tracking

origin
↓
Remote repository

main
↓
Branch being pushed
```

---

# Upstream Tracking

After using:

```bash
git push -u origin main
```

Git remembers:

```text
Local Branch
main

tracks

Remote Branch
origin/main
```

Future pushes can use:

```bash
git push
```

without specifying the remote and branch every time.

---

# Part 9 – Modify File Directly on GitHub

Edited README.md using the GitHub web interface.

Added:

```text
Added from GitHub web interface
```

Committed the change directly on GitHub.

---

# Part 10 – Pull Changes From GitHub

Downloaded the new GitHub commit.

```bash
git pull origin main
```

Observed:

```text
Fast-forward
```

Meaning Git was able to update the local repository without conflicts.

Verified:

```bash
cat README.md
```

Output:

```text
Git Day 2 - GitHub Integration

Added from GitHub web interface
```

---

# Part 11 – View Updated Commit History

Viewed repository history.

```bash
git log --oneline
```

Observed:

```text
Update README.md
Initial commit
```

---

# Understanding HEAD

Observed:

```text
HEAD -> main
```

Meaning:

```text
Current Branch
↓
main
```

HEAD points to the current branch and current commit.

---

# Understanding origin/main

Observed:

```text
origin/main
```

Meaning:

```text
Remote Tracking Branch
```

Represents the current state of the main branch on GitHub.

---

# Commands Learned

## Remote Management

```bash
git remote -v
git remote add origin URL
git remote remove origin
```

---

## Uploading Changes

```bash
git push
git push -u origin main
```

---

## Downloading Changes

```bash
git pull
git pull origin main
```

---

## Viewing History

```bash
git log
git log --oneline
```

---

# Key Lessons Learned

* Git repositories can exist locally without GitHub.
* GitHub repositories are considered remote repositories.
* `git remote -v` displays configured remote repositories.
* `origin` is a nickname for a remote repository.
* `main` is the primary branch.
* `git push` uploads commits to GitHub.
* `git pull` downloads and merges changes from GitHub.
* `HEAD` represents the current branch and commit.
* `origin/main` represents GitHub's version of the main branch.
* Local and remote repositories can remain synchronized through push and pull operations.

---

# Outcome

Successfully completed a full GitHub integration workflow:

```text
Create Repository
↓
Create Commit
↓
Connect GitHub
↓
Push Changes
↓
Modify File on GitHub
↓
Pull Changes
↓
Verify Synchronization
```

This lab provided hands-on experience with the Git and GitHub workflow used by DevOps Engineers, Cloud Engineers, Site Reliability Engineers (SREs), and Software Developers.
