# 🧠 Git Mastery — Complete Guide
### Session 1: Basics | Session 2: Branching & Remote | Session 3: Advanced

> A complete hands-on reference guide covering everything from `git init` to `git reflog`.
> Every command explained simply, with real examples practiced in the terminal.

**Author:** Syed Aftab
[![GitHub](https://img.shields.io/badge/GitHub-saftab4--arch-181717?style=flat&logo=github)](https://github.com/saftab4-arch)

---

## 📋 Progress Tracker

| Session | Topics Covered | Status |
|---------|---------------|--------|
| Session 1 | Git Basics — init, add, commit, status, log, diff, rm | ✅ Complete |
| Session 2 | Branching & Remote — branch, merge, push, pull, clone | ✅ Complete |
| Session 3 | Advanced — stash, reset, revert, rebase, cherry-pick, reflog | ✅ Complete |

---

# 📘 SESSION 1 — Git Basics

---

## 🤔 What is Git?

Git is a **version control system** — it tracks every change you make to your files over time.

Think of it like this: every time you save a snapshot of your work, Git remembers it. You can go back to any snapshot at any time.

```
Working Directory → Staging Area → Git History
   (edit files)      (git add)     (git commit)
```

---

## 🗂️ The 3 Zones of Git

| Zone | What it is | How to get there |
|------|-----------|-----------------|
| **Working Directory** | Where you create and edit files | Just edit! |
| **Staging Area** | Files waiting to be saved | `git add` |
| **Git History** | Permanently saved snapshots | `git commit` |

---

## ⚙️ Session 1 Commands

---

### 1. `git init`

**What it does:** Creates a brand new Git repository in your current folder.
It creates a hidden `.git` folder — this folder IS Git. Everything Git knows lives here.

```bash
git init
```

> ⚠️ Warning: If you delete the `.git` folder (`rm -rf .git`), ALL history is gone forever. Not even reflog can save you!

**Example:**
```bash
mkdir my-project
cd my-project
git init
# Output: Initialized empty Git repository in /home/my-project/.git/
```

---

### 2. `git status`

**What it does:** Shows you what's going on right now — which files are tracked, untracked, staged, or modified.

```bash
git status
```

**Output explained:**
```
On branch main                    ← which branch you're on
Untracked files:                  ← new files Git doesn't know about yet
    hello.txt                     ← red = not staged
Changes to be committed:          ← files ready to be committed
    new file: hello.txt           ← green = staged
```

---

### 3. `git add`

**What it does:** Moves files from Working Directory to Staging Area. Think of it as "marking" files you want to save.

```bash
git add filename.txt      # add one specific file
git add .                 # add ALL files in current folder
git add *.txt             # add all .txt files
```

> Nothing gets permanently saved without `git add` first!

**Example:**
```bash
echo "Hello World" > hello.txt
git add hello.txt
git status
# Output: Changes to be committed: new file: hello.txt (green!)
```

---

### 4. `git commit`

**What it does:** Permanently saves a snapshot of everything in the Staging Area. This is your "save point."

```bash
git commit -m "your message here"
```

> `-m` = message flag. Always write a clear message describing WHAT you did.

**Example:**
```bash
git commit -m "initial commit: add hello.txt"
# Output: [main abc1234] initial commit
#  1 file changed, 1 insertion(+)
```

**Good commit messages:**
```bash
git commit -m "feat: add login page"
git commit -m "fix: resolve payment bug"
git commit -m "docs: update README"
git commit -m "hotfix: fixed critical bug"
```

---

### 5. `git log`

**What it does:** Shows the history of all commits — like a timeline of your work.

```bash
git log             # full detailed log
git log --oneline   # short version (most useful!)
```

**Example output:**
```
f29422e (HEAD -> main) commit C   ← newest
4219180 commit B
c911d4c commit A
235b11a initial commit            ← oldest
```

**HEAD** = where you currently are in history.

---

### 6. `git diff`

**What it does:** Shows exactly what CHANGED in your files — line by line.

```bash
git diff              # changes NOT yet staged
git diff --staged     # changes that ARE staged
```

**Output:**
```
- Hello World         ← red = removed line
+ Hello Pakistan      ← green = added line
```

---

### 7. `git rm`

**What it does:** Removes a file from both your folder AND from Git tracking.

```bash
git rm filename.txt           # delete file + untrack
git rm --cached filename.txt  # keep file, just untrack
```

> `--cached` = remove from Git's memory but keep the actual file on disk.

---

### 8. `git restore`

**What it does:** Brings back a previous version of a file. Has 3 different uses:

```bash
# Use 1: Unstage a file (undo git add)
git restore --staged filename.txt

# Use 2: Discard changes (go back to last commit version)
git restore filename.txt

# Use 3: Get a file from a specific old commit
git restore --source abc1234 filename.txt
```

> ⚠️ `git restore filename.txt` permanently deletes unsaved changes!

**With dot (.) — affects ALL files:**
```bash
git restore --staged .   # unstage everything
git restore .            # discard all changes
```

---

### 9. `git clean`

**What it does:** Deletes untracked files (files Git has never seen before).

```bash
git clean -nd    # dry run — preview what would be deleted
git clean -fd    # actually delete untracked files and folders
```

> `-n` = dry run, `-f` = force, `-d` = include directories

---

# 📗 SESSION 2 — Branching & Remote

---

## 🌿 What is a Branch?

A branch is like a parallel universe for your code. You can work on a new feature without touching the main code.

```
main:    A → B → C
                  \
feature:           D → E → F
```

---

## 🌿 Branching Commands

### 1. `git branch`

**What it does:** Lists all branches, or creates a new one.

```bash
git branch                    # list all branches (* = current)
git branch feature/login      # create new branch
git branch -d feature/login   # delete branch (safe)
git branch -D feature/login   # force delete branch
```

> Deleting a branch only removes the LABEL — commits stay in history!

---

### 2. `git switch`

**What it does:** Moves you to a different branch.

```bash
git switch main               # go to main branch
git switch feature/login      # go to existing branch
git switch -c feature/login   # create AND switch in one command
```

---

### 3. `git merge`

**What it does:** Combines another branch's changes into your current branch. Creates a merge commit.

```bash
git switch main
git merge feature/login       # merge feature into main
```

**Result:**
```
main:    A → B → C ──────────── M (merge commit)
                  \            /
feature:           D → E → F /
```

---

### 4. `git remote add`

**What it does:** Connects your local repo to GitHub.

```bash
git remote add origin https://github.com/username/repo.git
```

> `origin` = nickname for the GitHub URL. Industry standard name.

---

### 5. `git push`

**What it does:** Sends your local commits UP to GitHub. 💻 → ☁️

```bash
git push -u origin main     # first time push (sets upstream)
git push                    # after first time (shortcut)
git push origin main        # explicit push
git push origin main --force  # force overwrite ⚠️ dangerous!
```

> `-u` = set default upstream. Only needed once.

---

### 6. `git pull`

**What it does:** Downloads latest changes FROM GitHub to your local machine. ☁️ → 💻

```bash
git pull origin main    # download latest
git pull                # shortcut after upstream is set
```

**When to use:**
- Teammate pushed new code → pull to get it
- You edited something on GitHub directly → pull to local

---

### 7. `git clone`

**What it does:** Copies an entire repo from GitHub to your local machine for the first time.

```bash
git clone https://github.com/username/repo.git
git clone https://github.com/username/repo.git my-folder
```

**pull vs clone:**
| Command | When to use |
|---------|-------------|
| `git clone` | First time — you don't have the repo yet |
| `git pull` | You already have it — just get latest updates |

---

### 8. Merge Conflicts 💥

**What is it?** When 2 branches edit the SAME file on the SAME line — Git can't decide which to keep.

**Conflict rule:**
| Same File? | Same Line? | Result |
|------------|------------|--------|
| ❌ Different | ✅ Same | ✅ No Conflict |
| ✅ Same | ❌ Different | ✅ No Conflict |
| ✅ Same | ✅ Same | 💥 CONFLICT! |

**What a conflict looks like inside the file:**
```
<<<<<<< HEAD
Hello Pakistan        ← your version (current branch)
=======
Hello America         ← their version (merging branch)
>>>>>>> feature/conflict
```

**How to resolve:**
```bash
# Step 1: Open the file, decide what to keep
echo "Hello Pakistan and America" > conflict.txt

# Step 2: Stage the resolved file
git add conflict.txt

# Step 3: Commit
git commit -m "resolve: merge conflict in conflict.txt"
```

---

# 📙 SESSION 3 — Advanced Git

---

### 1. `git stash`

**What it does:** Temporarily saves your unfinished work so you can switch branches without committing.

**Real scenario:** You're halfway through a feature when your boss says "urgent bug fix needed on main!"

```bash
git stash           # save work (tracked files only)
git stash -u        # save work INCLUDING untracked files
```

> ⚠️ Untracked files (never `git add`ed) are NOT stashed by default! Use `-u` or `git add` first.

**Full stash commands:**
```bash
git stash                        # save current work
git stash -u                     # save including untracked
git stash push -m "my message"   # save with a name
git stash list                   # see all stashes
git stash pop                    # apply latest + delete from stash
git stash apply                  # apply latest but KEEP in stash
git stash apply stash@{1}        # apply specific stash
git stash drop stash@{0}         # delete specific stash
git stash clear                  # delete ALL stashes
```

**stash pop vs stash apply:**
| Command | Applies stash? | Keeps in stash list? |
|---------|---------------|---------------------|
| `stash pop` | ✅ Yes | ❌ No (deleted) |
| `stash apply` | ✅ Yes | ✅ Yes (kept) |

**Full workflow example:**
```bash
# Working on feature...
git switch -c feature/payment
echo "payment code" > payment.txt
git add payment.txt

# Urgent fix needed!
git stash                    # save work
git switch main
echo "hotfix" > hotfix.txt
git add hotfix.txt
git commit -m "hotfix: critical bug"

# Back to feature
git switch feature/payment
git stash pop                # get work back!
```

---

### 2. `git reset`

**What it does:** Moves HEAD backwards in history. Can undo commits in 3 different ways.

```
Before: A → B → C → D (HEAD)
After reset HEAD~1: A → B → C (HEAD)
```

**3 modes:**

```bash
git reset --soft HEAD~1     # undo commit, keep changes STAGED
git reset --mixed HEAD~1    # undo commit, keep changes UNSTAGED (default)
git reset --hard HEAD~1     # undo commit, DELETE changes ⚠️
```

| Mode | Commits | Staged Area | Files on Disk |
|------|---------|-------------|---------------|
| `--soft` | ❌ Gone | ✅ Safe | ✅ Safe |
| `--mixed` | ❌ Gone | ❌ Cleared | ✅ Safe |
| `--hard` | ❌ Gone | ❌ Cleared | ❌ DELETED |

> `HEAD~1` = one commit back. `HEAD~3` = three commits back. Or use a specific commit ID.

**When to use each:**
```
--soft   → "I committed too early, let me add more changes first"
--mixed  → "I want to redo my staging completely"
--hard   → "Delete everything, I want to start fresh" ⚠️
```

> ⚠️ Never use `reset` on commits already pushed to GitHub — use `revert` instead!

---

### 3. `git revert`

**What it does:** Creates a NEW commit that undoes a previous commit. History is kept safe.

```
Before: A → B → C → D
After:  A → B → C → D → D'(revert)
                         ↑
                    D is undone but still in history!
```

```bash
git revert HEAD         # undo latest commit
git revert abc1234      # undo specific commit
```

**reset vs revert:**
| | `git reset` | `git revert` |
|--|-------------|--------------|
| History | Deletes commit ❌ | Keeps commit ✅ |
| Safe after push? | ❌ Never | ✅ Always |
| Creates new commit? | ❌ No | ✅ Yes |
| Use when | Local only | Already pushed |

> **Golden Rule:** If code is already on GitHub → ALWAYS use `revert`!

---

### 4. `git rebase`

**What it does:** Moves your branch commits on top of another branch. Creates a clean linear history — no merge commit.

```
BEFORE rebase:
main:     A → B → C (urgent fix)
                ↑
feature:        D → E (navbar)

AFTER rebase:
main:     A → B → C → D' → E'
                             ↑
                   feature commits moved on top!
```

```bash
git switch feature/navbar
git rebase main             # put feature commits on top of main
```

**merge vs rebase:**
| | Merge | Rebase |
|--|-------|--------|
| Extra commit | ✅ Merge commit | ❌ No extra commit |
| History | Branchy 🌿 | Linear ➡️ |
| Safe | ✅ Always | ⚠️ Never on pushed branches |

> ⚠️ Never rebase a branch that has been pushed to GitHub — it rewrites history and breaks teammates' work!

---

### 5. `git cherry-pick` 🍒

**What it does:** Takes ONE specific commit from any branch and applies it to your current branch. You choose exactly what you want!

```
feature: fix1 → work2 → fix3
                  ❌      
main gets: fix1 + fix3 only (work2 skipped!)
```

```bash
git switch main
git cherry-pick abc1234     # pick one specific commit
git cherry-pick abc1 def2   # pick multiple commits
```

**Real world use case:**
```
Feature branch has 10 commits.
Only 2 of them are bug fixes you need in main NOW.
Don't merge the whole branch — cherry-pick just those 2!
```

---

### 6. `git log` Advanced

**What it does:** Shows commit history with different formats and filters.

```bash
git log --oneline                          # short one-line format
git log --oneline --graph --all            # visual branch graph
git log --oneline -3                       # last 3 commits only
git log --oneline -- README.md             # history of one file
git log --oneline --format="%h %ad %s" --date=short  # with dates
```

**Graph output example:**
```
* ce9a6f9 (HEAD → main) latest commit
* 636a12c fix: important bugfix
| * be39aea (feature/payment) feature commit
| * d5b44ec another feature commit
|/
* 235b11a initial commit
```

The `|` and `/` lines show branching visually!

---

### 7. `git tag`

**What it does:** Marks a specific commit with a version label — like a milestone bookmark.

```bash
git tag v1.0                           # lightweight tag (just a label)
git tag -a v1.0 -m "First release"    # annotated tag (with message) ✅ recommended
git tag -a v0.1 abc1234 -m "message"  # tag an old commit
git tag                                # list all tags
git log --oneline --decorate           # see tags in log
git push origin v1.0                   # push tag to GitHub
git push origin --tags                 # push ALL tags to GitHub
```

**Output in log:**
```
ce9a6f9 (HEAD → main, tag: v1.0) latest release
c911d4c (tag: v0.1) older version
```

---

### 8. `.gitignore`

**What it does:** Tells Git to completely ignore certain files — they won't be tracked or pushed to GitHub.

**Why it matters:**
```
.env files contain API keys and passwords → NEVER push to GitHub!
node_modules/ is huge and regeneratable → waste of space!
*.log files are temporary → no need to track!
```

```bash
# Create .gitignore
echo ".env" >> .gitignore
echo "*.log" >> .gitignore
echo "node_modules/" >> .gitignore
echo ".DS_Store" >> .gitignore

# Commit it
git add .gitignore
git commit -m "add .gitignore"
```

**Pattern examples:**
```
.env          → ignores exactly ".env" file
*.log         → ignores ANY file ending in .log
node_modules/ → ignores entire folder
secrets.txt   → ignores exactly "secrets.txt"
```

> The `.gitignore` file itself IS tracked — so teammates also know what's ignored!

---

### 9. `git reflog` 🔮

**What it does:** Shows EVERYTHING that ever happened — commits, resets, checkouts, merges, rebases. Your ultimate safety net!

```bash
git reflog
```

**Output:**
```
3298159 HEAD@{0}: commit: important: final piece
39e15d0 HEAD@{1}: reset: moving to HEAD~1
b7f65c0 HEAD@{2}: commit: important: added critical feature
```

**git log vs git reflog:**
| | `git log` | `git reflog` |
|--|-----------|--------------|
| Shows | Committed history only | EVERYTHING |
| After reset --hard | Commits gone | Still visible! |
| Recovery possible? | ❌ No | ✅ Yes! |

**Recovery after accidental reset --hard:**
```bash
# Step 1: Find the lost commit
git reflog
# Find the commit ID before the reset

# Step 2: Go back to it
git reset --hard <commit-id>

# Everything is back! 🎉
```

> ⚠️ reflog only works if `.git` folder exists! If you did `rm -rf .git` — nothing can save you!

---

# 🎯 Interview Questions & Answers

---

### Q1: What is the difference between `git merge` and `git rebase`?

**Answer:**

Both merge and rebase integrate changes from one branch into another, but they do it differently.

`git merge` creates a new "merge commit" that joins two branches together. The history shows the branching clearly — you can see exactly when branches diverged and merged.

`git rebase` takes your commits and replays them on top of another branch. The result is a perfectly linear history with no extra merge commit.

I use **merge** for team collaboration because it preserves the full history and is always safe. I use **rebase** when I want a clean linear history — usually before opening a Pull Request. But I never rebase a branch that's already been pushed to GitHub, because it rewrites history and breaks my teammates' work.

---

### Q2: How do you resolve a merge conflict?

**Answer:**

When I run `git merge` and a conflict happens, Git marks the conflicting file like this:

```
<<<<<<< HEAD
My version of the code
=======
Their version of the code
>>>>>>> feature/branch
```

My process is:
1. Run `git status` to identify which files have conflicts
2. Open each conflicted file
3. Review both versions, discuss with teammate if needed
4. Keep the correct version and delete all the `<<<<<<<`, `=======`, `>>>>>>>` markers
5. Run `git add` on the resolved file
6. Run `git commit` to complete the merge

---

### Q3: What is the difference between `git reset` and `git revert`?

**Answer:**

Both undo changes, but in completely different ways.

`git reset` actually removes commits from history. It's like they never happened. This is dangerous if the commits were already pushed to GitHub because it breaks the history for everyone on the team.

`git revert` creates a brand new commit that undoes the changes from a previous commit. The original commit stays in history — it's just neutralized by the new revert commit. This is always safe to use, even after pushing.

My rule is simple: if the commit is only local and not pushed yet, I might use reset. But if it's already on GitHub, I always use revert.

---

### Q4: What is `.gitignore` and why is it important?

**Answer:**

`.gitignore` is a file that tells Git which files to completely ignore — they won't be tracked or pushed to GitHub.

It's critically important for two reasons: security and efficiency.

For security — `.env` files contain API keys, database passwords, and secrets. If these get pushed to GitHub, anyone can see them and your accounts can be compromised.

For efficiency — `node_modules/` can contain thousands of files and hundreds of megabytes. It can be regenerated with `npm install` anytime, so there's no reason to push it.

Common things I always put in `.gitignore`:
```
.env              # secrets
node_modules/     # dependencies
*.log             # log files
.DS_Store         # Mac OS system file
```

---

### Q5: What branch strategy do you follow?

**Answer:**

I follow Git Flow:

```
main      → production code, always stable, never commit directly
develop   → integration branch, all features merge here first
feature/* → one branch per feature (feature/login, feature/payment)
bugfix/*  → for bug fixes during development
hotfix/*  → urgent production fixes, branch from main directly
```

I never commit directly to `main`. Every change goes through a branch and a Pull Request with code review. I write descriptive commit messages like `feat: add payment gateway` or `fix: resolve login timeout`. This keeps the team's work organized and makes rollbacks easy if something breaks in production.

---

# 📊 Complete Command Cheat Sheet

```bash
# ═══════════════════════════════════
# SESSION 1 — BASICS
# ═══════════════════════════════════
git init                          # create new repo
git status                        # what's going on?
git add filename.txt              # stage one file
git add .                         # stage all files
git commit -m "message"           # save snapshot
git log --oneline                 # short history
git diff                          # what changed?
git rm filename.txt               # delete + untrack file
git restore --staged filename.txt # unstage file
git restore filename.txt          # discard changes ⚠️
git restore --source ID file      # get old version
git clean -nd                     # preview untracked files
git clean -fd                     # delete untracked files

# ═══════════════════════════════════
# SESSION 2 — BRANCHING & REMOTE
# ═══════════════════════════════════
git branch                        # list branches
git branch feature/name           # create branch
git branch -d feature/name        # delete branch
git switch feature/name           # go to branch
git switch -c feature/name        # create + go to branch
git merge feature/name            # merge into current branch
git remote add origin <url>       # connect to GitHub
git push -u origin main           # first push
git push                          # push after first time
git pull origin main              # get latest from GitHub
git clone <url>                   # copy repo locally

# ═══════════════════════════════════
# SESSION 3 — ADVANCED
# ═══════════════════════════════════
git stash                         # save unfinished work
git stash -u                      # save including untracked
git stash push -m "message"       # save with name
git stash list                    # see all stashes
git stash pop                     # apply + delete stash
git stash apply                   # apply but keep stash
git stash drop stash@{0}          # delete specific stash
git stash clear                   # delete all stashes

git reset --soft HEAD~1           # undo commit, keep staged
git reset --mixed HEAD~1          # undo commit, unstage all
git reset --hard HEAD~1           # undo commit + delete files ⚠️

git revert HEAD                   # undo last commit safely
git revert abc1234                # undo specific commit

git rebase main                   # rebase onto main
git rebase -i HEAD~3              # interactive rebase

git cherry-pick abc1234           # pick one commit
git cherry-pick abc1 def2         # pick multiple commits

git log --oneline                 # short log
git log --oneline --graph --all   # visual graph
git log --oneline -3              # last 3 commits
git log --oneline -- file.txt     # file history

git tag v1.0                      # create tag
git tag -a v1.0 -m "message"      # annotated tag
git tag                           # list tags
git push origin --tags            # push tags to GitHub

git reflog                        # see ALL history (recovery tool)
git reset --hard <reflog-id>      # recover lost commits
```

---

*Built with hands-on terminal practice across 3 sessions. Every command tested and documented.*
*github.com/saftab4-arch*
