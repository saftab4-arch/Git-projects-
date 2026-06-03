# Git Day 3 Project - Branching, Merging and Conflict Resolution

## Project Overview

This project was created as part of my Git learning journey to gain hands-on experience with branching, merging, merge conflicts, and GitHub collaboration workflows.

The project demonstrates how multiple developers can work on different features independently and how Git manages code integration.

---

## Skills Practiced

* Git repository initialization
* Creating and switching branches
* Branch isolation
* Fast-forward merges
* Merge commits
* Merge conflict detection
* Merge conflict resolution
* Local and remote repository synchronization
* GitHub integration
* Commit history visualization

---

## Project Structure

```text
git-day3-project/
│
├── README.md
└── app.txt
```

---

## Branches Created

### Main Branch

Production-ready branch.

### Feature Login

Added Login Module.

### Feature Dashboard

Added Dashboard Module.

### Feature Profile

Added Profile Module.

---

## Workflow

### Initial Setup

Created repository and committed initial files.

### Feature Development

Three feature branches were created:

* feature-login
* feature-dashboard
* feature-profile

Each branch modified the same line in app.txt to intentionally create merge conflicts.

### Merge Operations

#### Fast-Forward Merge

Merged feature-login into main using a Fast-Forward merge.

#### Merge Conflict #1

Merged feature-dashboard into main.

Conflict occurred because both branches modified the same line.

Conflict was manually resolved.

#### Merge Conflict #2

Merged feature-profile into main.

Another conflict occurred and was manually resolved.

### GitHub Collaboration Simulation

The repository was pushed to GitHub.

README.md was modified:

* Locally
* Directly on GitHub

A git pull operation created a merge conflict between local and remote changes.

The conflict was resolved manually and committed.

---

## Key Commands Used

```bash
git init
git add .
git commit -m "message"

git branch
git branch -a

git switch
git switch -c branch-name

git merge branch-name

git log --oneline
git log --oneline --graph --all

git remote add origin <repository-url>

git push -u origin main

git pull
```

---

## Concepts Learned

### Fast-Forward Merge

Occurs when the target branch has no new commits and Git simply moves the branch pointer forward.

### Merge Commit

Occurs when both branches contain unique commits and Git creates a new commit to combine histories.

### Merge Conflict

Occurs when multiple branches modify the same line of a file and Git cannot determine which version to keep.

### origin/main

Represents Git's local tracking reference to GitHub's main branch.

### git pull

Equivalent to:

```bash
git fetch
git merge
```

---

## Final Outcome

Successfully completed:

* Multiple branch workflow
* Local merge conflicts
* Remote GitHub merge conflicts
* Merge conflict resolution
* GitHub synchronization

This project simulates a real-world software development workflow using Git and GitHub.
