# 🧠 Git Mastery — Complete Cheatsheet
### Session 1: Basics + Session 2: Branching & Remote

A complete personal reference guide covering everything learned across both Git sessions.
All commands, flags, real examples, key concepts, and screenshots.

**GitHub:** [github.com/saftab4-arch](https://github.com/saftab4-arch)

---

## 📁 Screenshot Folder Structure

```
git-mastery/
├── session-1-basics/
│   └── screenshots/
├── session-2-branching/
│   └── screenshots/
│       ├── Screenshot_1_.jpg
│       ├── Screenshot_2_branches_created.jpg
│       ├── Screenshot_3_switch_branch_and_add_stuff.jpg
│       ├── Screenshot_4_switch_branch.jpg
│       ├── Screenshot_5_switch_to_main.jpg
│       ├── Screenshot_6_merge_all_3.jpg
│       ├── Screenshot_7_deleted_3_branch_0d.jpg
│       ├── Screenshot_8_github_created.jpg
│       ├── Screenshot_9_push_to_github.jpg
│       ├── Screenshot_10_git_pull_-u_origin_main.jpg
│       └── Screenshot_11_git_clone.jpg
└── MASTER-README.md
```

---

# 📘 SESSION 1 — Git Basics

---

## 📌 What is Git?

Git is a version control system that **tracks changes** to files over time.
Every change you make can be saved as a snapshot — and restored anytime.

```
Working Directory → Staging Area → Git History
    (edit file)       (git add)    (git commit)
```

---

## 🗂️ The 3 Zones of Git

| Zone | What it is |
|------|-----------|
| **Working Directory** | Where you create/edit files |
| **Staging Area** | Files waiting to be committed (git add) |
| **Git History** | Permanently saved snapshots (git commit) |

---

## ⚙️ Session 1 Commands

---

### 1. `git init`

Initializes a new Git repository in the current folder.
Creates a hidden `.git` folder that stores all history.

```bash
git init
```

> ⚠️ Everything Git knows lives inside `.git` — delete it and all history is gone.

---

### 2. `git add`

Stages files — moves them from Working Directory to Staging Area.
**Nothing gets tracked without this step first.**

```bash
git add filename.txt        # stage a specific file
git add hello.txt hello1.txt  # stage multiple files
git add .                   # stage ALL changes at once
```

**Key rule:**

| File state | Git can track? |
|-----------|---------------|
| Never git added | ❌ Git is completely blind |
| git added (staged) | ✅ Git sees it |
| git added + committed | ✅ Git tracks full history |

---

### 3. `git commit -m`

Saves a permanent snapshot of everything in the staging area.
Stamps your **name, email, timestamp, and message** on it forever.

```bash
git commit -m "your message here"
git commit -m "add login page"
git commit -m "fix NAT gateway routing bug"
```

**Good vs bad commit messages:**

```bash
git commit -m "add vpc peering config"    ✅ descriptive
git commit -m "fix bug"                   ⚠️  vague
git commit -m "testing"                   ❌ means nothing
git commit -m "asdfgh"                    ❌ worst 😂
```

> 💡 Commit message = label on a box. Future you will thank present you.

---

### 4. `git commit -am` (shortcut)

Skips `git add` for already tracked files — stages + commits in one command.

```bash
git commit -am "updated file content"
```

**Limitation:**

| Situation | `-am` works? |
|-----------|-------------|
| Modified existing file | ✅ Yes |
| Deleted existing file | ✅ Yes |
| Brand new file (never added) | ❌ Must `git add` first |

---

### 5. `git status`

Shows what has changed since the last commit — but **not yet committed**.

```bash
git status
```

**What the colors mean:**

| Color | Meaning |
|-------|---------|
| 🔴 Red `modified` | File changed, not staged yet |
| 🔴 Red `deleted` | File deleted, not committed yet |
| 🔴 Red `untracked` | New file never git added |
| 🟢 Green | Staged and ready to commit |

> ⚠️ `git status` shows WHAT changed — not WHO changed it. WHO is only recorded at commit time.

---

### 6. `git log`

Shows the full commit history with author, date, and message.

```bash
git log                     # full detailed history
git log --oneline           # short clean one-line view
git log --stat              # history + which files changed
git log filename.txt        # commits that touched a specific file
git log --all -- iqra.txt   # history of a file even after deletion
git log -p filename.txt     # full diff of every change to a file
```

**Example output of `git log --oneline`:**
```
395c65e  delete iqra.txt
dd791f3  add iqra.txt
82877f7  testing
```

> 💡 Always use `git log --stat` in real world — shows files, not just messages.

---

### 7. `git diff`

Shows what changed in a file **since the last commit** — before staging.

```bash
git diff                    # all uncommitted changes
git diff filename.txt       # changes in a specific file
git diff --cached           # changes that are staged but not committed
```

**Reading the output:**
```
-this is old line       ← red = removed
+this is new line       ← green = added
```

---

### 8. `git rm`

Deletes a file AND stages the deletion in one command.

```bash
git rm filename.txt
git commit -m "delete filename.txt"
```

**vs regular `rm`:**

| Command | What happens |
|---------|-------------|
| `rm filename.txt` | Deletes from filesystem only — Git doesn't know yet |
| `git rm filename.txt` | Deletes + stages deletion automatically |

> 💡 Always use `git rm` instead of `rm` when deleting tracked files.

---

### 9. `git show`

Shows exactly what changed in a specific commit.

```bash
git show HEAD           # latest commit details
git show 82877f7        # specific commit details
```

---

### 10. `git restore` (Modern Way)

Modern replacement for `git checkout` for file restoration.

```bash
# Undo changes to a file (not yet staged)
git restore filename.txt

# Unstage a file (undo git add)
git restore --staged filename.txt

# Restore from specific commit
git restore --source <commitID> filename.txt
```

**vs old way:**

| Old | Modern |
|-----|--------|
| `git checkout id -- file` | `git restore --source id file` |

---

### 11. `git checkout` (Restore - Old Way)

Time machine — goes back to a specific commit and restores a file.

```bash
git checkout <commitID> -- filename.txt
```

**Steps to restore a deleted file:**
```bash
# Step 1 - find the commit where file existed
git log --oneline

# Step 2 - restore it
git checkout dd791f3 -- iqra.txt

# Step 3 - commit the restore
git commit -am "restore iqra.txt"
```

> 💡 Nothing is ever truly gone as long as it was committed. Git remembers forever.

---

## 🔑 Key Concepts — Session 1

---

### Commit ID (Tracking Number)

```
Full ID:   dd791f3138ee2168f85957d3e09c6cf49cdc07a4
Short ID:  dd791f3    ← first 7 characters, works the same
```

---

### Who Did It?

```bash
# Set your identity (do this once)
git config --global user.name "Syed Aftab"
git config --global user.email "saftab4@wgu.edu"
```

Every commit shows:
```
Author: Syed Aftab <saftab4@wgu.edu>    ← WHO
Date:   Mon Jun 1 22:52:13 2026         ← WHEN
    updated file                         ← WHAT
```

> ⚠️ If someone changes a file but **never commits** — there is NO record of who did it.

---

### How Long Does Git Store Snapshots?

**Forever** — as long as `.git` folder exists.

| Action | History safe? |
|--------|-------------|
| Normal usage | ✅ Forever |
| Push to GitHub | ✅ Backed up remotely |
| `rm -rf .git` | ❌ All history gone |

> 💡 Golden rule: **If it's not committed and pushed — it doesn't exist.**

---

### The Loophole 🔓

If someone edits files, does `git add` but **never commits**:
- `git status` shows modified ✅
- WHO did it? ❌ Unknown

**Protection:** Commit frequently + push to GitHub always!

---

## 🧠 Session 1 Mental Models

```
git add      = put files in a box 📦
git commit   = seal the box + write a label 🏷️
git log      = see all your boxes 📋
git diff     = see what's changed since last sealed box 🔍
git restore  = open an old box and grab something 🕰️
git status   = what's messy right now 🗂️
```

---

## ✅ Session 1 Commands Mastered

| Command | ✅ |
|---------|---|
| `git init` | ✅ |
| `git add` | ✅ |
| `git commit -m` | ✅ |
| `git commit -am` | ✅ |
| `git status` | ✅ |
| `git log` | ✅ |
| `git log --oneline` | ✅ |
| `git log --stat` | ✅ |
| `git diff` | ✅ |
| `git diff --cached` | ✅ |
| `git show` | ✅ |
| `git rm` | ✅ |
| `git restore` | ✅ |
| `git checkout` (restore) | ✅ |
| `git config --global` | ✅ |

---

---

# 📗 SESSION 2 — Branching & Remote

---

## 📌 What is a Branch?

A branch is a **separate line of work** that runs independently from main.

```
main          → stable/production code 🔒
feature/login → developer A working on login
feature/api   → developer B working on API
bugfix/navbar → developer C fixing a bug
```

All 3 working at the same time **WITHOUT breaking each other!**

---

## 📌 main vs master

| Name | Status |
|------|--------|
| `master` | Old default name |
| `main` | New industry standard (GitHub default since 2020) ✅ |

Set it globally:
```bash
git config --global init.defaultBranch main
git branch -m main    # rename current branch to main
```

---

## ⚙️ Session 2 Commands

---

### 1. `git branch`

View, create, or delete branches.

```bash
git branch                  # list all branches (* = current)
git branch feature-1        # create new branch
git branch feature/login    # create with slash naming (real world)
git branch -d feature-1     # delete branch (after merging)
git branch -D feature-1     # force delete (even if not merged)
```

![Screenshot 1 - git init and first commit](session-2-branching/screenshots/Screenshot_1_.jpg)

![Screenshot 2 - branches created](session-2-branching/screenshots/Screenshot_2_branches_created.jpg)

**Output of `git branch`:**
```
  bugfix/navbar    ← branch exists
  feature-1        ← branch exists
  feature/api      ← branch exists
* main             ← * = you are HERE
```

---

### 2. `git switch`

Jump between branches — modern replacement for `git checkout`.

```bash
git switch feature-1        # switch to feature-1
git switch main             # switch back to main
git switch -c new-branch    # create AND switch in one command
```

![Screenshot 3 - switch branch and add stuff](session-2-branching/screenshots/Screenshot_3_switch_branch_and_add_stuff.jpg)

![Screenshot 4 - switch branch](session-2-branching/screenshots/Screenshot_4_switch_branch.jpg)

> 💡 The `*` in `git branch` always shows which branch you're currently on.

---

### 3. Working on a Branch

Each branch is completely isolated — files on one branch don't appear on others!

```bash
# Switch to branch
git switch feature/login

# Do your work
echo "this is login page" > login.txt
git add login.txt
git commit -m "add login page"

# Check log - only shows commits for THIS branch
git log --oneline
```

**Switch to main — files from other branches are GONE:**

```bash
git switch main
ls    # only shows main's files ← magic! 🔥
```

![Screenshot 5 - switch to main](session-2-branching/screenshots/Screenshot_5_switch_to_main.jpg)

---

### 4. `git merge`

Brings work from a branch INTO your current branch.

```bash
# Rule: stay on the branch you want to merge INTO
git switch main

git merge feature/login      # merge login into main
git merge feature/dashboard  # merge dashboard into main
git merge bugfix/header      # merge header fix into main
```

![Screenshot 6 - merge all 3](session-2-branching/screenshots/Screenshot_6_merge_all_3.jpg)

**Types of merges:**

| Type | When it happens |
|------|----------------|
| Fast-forward ⚡ | Simple, no conflicts — main just catches up |
| Ort/Recursive 🔀 | More complex history, still no conflicts |
| Conflict ❗ | Two branches changed the same line — must fix manually |

> 💡 Think of it like: **You stand in the ocean (main) and pull the river (branch) into you.**

---

### 5. `git branch -d` (Cleanup)

Delete branches after merging — real world cleanup!

```bash
git branch -d feature/login
git branch -d feature/dashboard
git branch -d bugfix/header
git branch    # only * main remains ✅
```

![Screenshot 7 - deleted 3 branches](session-2-branching/screenshots/Screenshot_7_deleted_3_branch_0d.jpg)

---

### 6. `git remote add origin`

Connects your local repo to GitHub.

```bash
git remote add origin https://github.com/saftab4-arch/git-practice2.git
```

| Part | Meaning |
|------|---------|
| `git remote` | manage connections to remote repos |
| `add` | add a new connection |
| `origin` | nickname for the GitHub URL (industry standard) |
| `<url>` | your GitHub repo address |

![Screenshot 8 - github created](session-2-branching/screenshots/Screenshot_8_github_created.jpg)

---

### 7. `git push`

Sends your local commits UP to GitHub. 💻→☁️

```bash
git push -u origin main     # first time (sets upstream)
git push                    # after first time (shortcut)
git push origin main        # explicit push
git push origin main --force  # force overwrite (careful! ⚠️)
```

| Flag | Meaning |
|------|---------|
| `-u` | set default upstream (only needed once) |
| `origin` | send to GitHub |
| `main` | push the main branch |

![Screenshot 9 - push to github](session-2-branching/screenshots/Screenshot_9_push_to_github.jpg)

---

### 8. `git pull`

Downloads changes FROM GitHub to your local machine. ☁️→💻

```bash
git pull origin main    # download latest from GitHub
git pull                # shortcut after upstream is set
```

![Screenshot 10 - git pull](session-2-branching/screenshots/Screenshot_10_git_pull_-u_origin_main.jpg)

**When to use:**
- Teammate pushed new code → you pull to get it
- You edited something directly on GitHub → pull to local

---

### 9. `git clone`

Copy an entire repo from GitHub to your local machine. ☁️→💻

```bash
git clone https://github.com/saftab4-arch/git-practice2.git
git clone https://github.com/saftab4-arch/git-practice2.git my-folder-name
```

![Screenshot 11 - git clone](session-2-branching/screenshots/Screenshot_11_git_clone.jpg)

**pull vs clone:**

| Command | When to use |
|---------|-------------|
| `git clone` | First time — getting a repo you don't have yet |
| `git pull` | Already have the repo — just getting latest updates |

---

## 🔑 Key Concepts — Session 2

---

### The Real World Branch Flow

```bash
# 1. Create branch for your task
git branch feature/login
git switch feature/login

# 2. Do your work and commit
echo "login code" > login.txt
git add login.txt
git commit -m "add login page"

# 3. Switch to main and merge
git switch main
git merge feature/login

# 4. Push to GitHub
git push origin main

# 5. Delete the branch (cleanup)
git branch -d feature/login
```

---

### Personal Access Token (GitHub Auth)

GitHub requires a token instead of password for HTTPS pushes:

1. GitHub → Settings → Developer Settings
2. Personal Access Tokens → Tokens (classic)
3. Generate new token → check `repo` → copy it
4. Use as password when Git asks

> ⚠️ Token is shown only ONCE — save it immediately!

---

### Branch Naming Conventions

```
feature/login       ← new features
feature/dashboard   ← new features
bugfix/navbar       ← bug fixes
hotfix/crash        ← urgent fixes
release/v1.0        ← release branches
```

---

## 🧠 Session 2 Mental Models

```
git branch    = create a side road 🛤️
git switch    = drive to a different road 🚗
git merge     = connect side road back to main road 🛣️
git push      = upload to cloud ☁️ 💻→☁️
git pull      = download from cloud ☁️ ☁️→💻
git clone     = copy entire highway from cloud ☁️→💻
```

---

## ✅ Session 2 Commands Mastered

| Command | ✅ |
|---------|---|
| `git branch` | ✅ |
| `git branch name` | ✅ |
| `git branch -d name` | ✅ |
| `git switch name` | ✅ |
| `git switch -c name` | ✅ |
| `git merge name` | ✅ |
| `git remote add origin` | ✅ |
| `git push -u origin main` | ✅ |
| `git push` | ✅ |
| `git pull origin main` | ✅ |
| `git clone <url>` | ✅ |

---

---

# 🚀 MASTER CHEATSHEET — All Commands

```bash
# ═══════════════════════════════
# SESSION 1 — BASICS
# ═══════════════════════════════

git init                          # initialize repo
git add filename.txt              # stage specific file
git add .                         # stage everything
git commit -m "message"           # commit with label
git commit -am "message"          # stage + commit (tracked files only)
git status                        # what's changed not yet committed
git log                           # full history
git log --oneline                 # short history
git log --stat                    # history + files changed
git log -p filename.txt           # full diff history of file
git diff                          # all uncommitted changes
git diff filename.txt             # changes in specific file
git diff --cached                 # staged but not committed
git show HEAD                     # latest commit details
git show <commitID>               # specific commit details
git rm filename.txt               # delete + stage deletion
git restore filename.txt          # undo changes (not staged)
git restore --staged filename.txt # undo git add
git restore --source <id> file    # restore from commit (modern)
git checkout <id> -- file         # restore from commit (old)
git config --global user.name ""  # set your name
git config --global user.email "" # set your email

# ═══════════════════════════════
# SESSION 2 — BRANCHING & REMOTE
# ═══════════════════════════════

git branch                        # list all branches
git branch name                   # create branch
git branch -d name                # delete branch
git branch -m main                # rename to main
git switch name                   # switch to branch
git switch -c name                # create + switch
git merge name                    # merge into current branch
git remote add origin <url>       # connect to GitHub
git push -u origin main           # first push
git push                          # push (after upstream set)
git push origin main --force      # force push ⚠️
git pull origin main              # pull from GitHub
git pull                          # pull (after upstream set)
git clone <url>                   # clone repo
git clone <url> folder-name       # clone into specific folder
```

---

## 📌 Coming Up — Session 3

```
git rebase         → cleaner history than merge
git stash          → temporarily save work without committing
merge conflicts    → fixing when two branches change same line
git reset          → undo commits
git revert         → safely undo with new commit
```

---

## 👤 Author

**Syed Aftab**
[![GitHub](https://img.shields.io/badge/GitHub-saftab4--arch-181717?style=flat&logo=github)](https://github.com/saftab4-arch)

---

*Part of the [#90DaysOfDevOps](https://github.com/saftab4-arch) challenge*

`#Git` `#GitHub` `#DevOps` `#Linux` `#90DaysOfDevOps` `#VersionControl`
