# Git Day 4 - Advanced Git Operations

## Overview

This lab focuses on advanced Git commands commonly used in collaborative development and DevOps environments.

Topics covered:

* Fetch vs Pull
* Git Rebase
* Git Stash
* Git Tags
* Git Restore
* Git Reset (Soft, Mixed, Hard)

---

## 1. Fetch vs Pull

### Git Fetch

Downloads updates from the remote repository without modifying the local branch.

```bash
git fetch
```

Use fetch when you want to inspect remote changes before integrating them.

### Git Pull

Downloads updates and updates the current branch.

```bash
git pull
```

Pull is essentially:

```bash
git fetch
git merge
```

---

## 2. Git Rebase

Rebase moves a feature branch on top of another branch.

```bash
git rebase main
```

Benefits:

* Cleaner commit history
* Fewer merge commits
* Easier project maintenance

Example workflow:

```bash
git switch feature
git rebase main
```

---

## 3. Git Stash

Temporarily saves unfinished work.

### Save Changes

```bash
git stash
```

### View Stashes

```bash
git stash list
```

### Restore Changes

```bash
git stash pop
```

Useful when switching tasks without creating incomplete commits.

---

## 4. Git Tags

Tags are used to mark release points.

### Create Tag

```bash
git tag v1.0
```

### View Tags

```bash
git tag
```

### Push Tags

```bash
git push origin v1.0
```

or

```bash
git push --tags
```

---

## 5. Git Restore

Discard uncommitted changes in a file.

```bash
git restore feature.txt
```

Restores the file to its last committed state.

---

## 6. Git Reset

### Soft Reset

Removes commit but keeps changes staged.

```bash
git reset --soft HEAD~1
```

Result:

* Commit removed
* Changes staged
* Files preserved

### Mixed Reset

Removes commit and unstages changes.

```bash
git reset --mixed HEAD~1
```

Result:

* Commit removed
* Changes unstaged
* Files preserved

### Hard Reset

Removes commit and restores tracked files.

```bash
git reset --hard HEAD~1
```

Result:

* Commit removed
* Staging cleared
* Tracked file changes removed

---

## Key Lessons Learned

* Fetch updates remote references only.
* Pull updates local files and branch history.
* Rebase creates a cleaner project history.
* Stash safely stores unfinished work.
* Tags mark release versions.
* Restore discards local modifications.
* Soft, Mixed, and Hard reset affect commits, staging, and files differently.

---

## Skills Practiced

* Remote repository synchronization
* Branch management
* Commit history manipulation
* Temporary work preservation
* Release versioning
* Recovery and rollback techniques

This lab provides practical Git skills commonly used by Linux, DevOps, and Cloud Engineers.
