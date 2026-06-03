# 🔀 Git Mastery — Local vs GitHub Conflict Resolution

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)

> A real-world Git project simulating what happens when two developers edit the same file —
> one locally, one directly on GitHub — and how to resolve the conflict like a pro.

**Author:** Syed Aftab | [github.com/saftab4-arch](https://github.com/saftab4-arch)

---

## 🎯 What This Project Demonstrates

- What happens when local and remote histories **diverge**
- Why `git push` gets **rejected**
- How to resolve a **merge conflict** step by step
- The difference between `git pull` with and without conflicts
- Real-world **conflict resolution** using nano editor

---

## 🧠 The Concept — Why Does This Happen?

When two people (or you on two machines) edit the **same file on the same lines**, Git cannot decide which version to keep automatically.

```
GitHub:  A → B → C → D   ← teammate committed here
Local:   A → B → C → E   ← you committed here
                  ↑
         Both branched from C in different directions!

Git says: "I don't know which to keep — YOU decide!" 💥
```

This is one of the most common real-world Git scenarios — especially in team environments.

---

## 📋 Project Steps — Full Walkthrough

---

### Step 1: Create Repo on GitHub with README

Created a new GitHub repository `git-mastery` with the **"Add a README file"** option checked.

This means GitHub already has one commit — the initial README.

```
GitHub state:
889e4d2 — Initial commit (README.md created on GitHub)
```

---

### Step 2: Edit README Directly on GitHub

Edited `README.md` directly on GitHub (simulating a teammate making changes):

```markdown
# Git Mastery

## This README was written on GitHub
- Session 1: Git Basics
- Session 2: Branching and Remote
- Session 3: Advanced Git

## Author
Syed Aftab - github.com/saftab4-arch
```

Committed directly to main on GitHub.

```
GitHub state:
b76dee5 — Update README.md  ← teammate's commit
889e4d2 — Initial commit
```

---

### Step 3: Clone Repo Locally

```bash
git clone https://github.com/saftab4-arch/git-mastery.git
cd git-mastery
cat README.md    # verify GitHub version is here
```

At this point local and GitHub are in sync:
```
Local:  A → B (same as GitHub) ✅
```

---

### Step 4: Edit README Locally (Without Pulling First)

Edited `README.md` locally — added different content:

```bash
nano README.md
# Added: "## Local Change - This line was added locally by me"
git add README.md
git commit -m "local: added my changes"
```

Now the histories have **diverged**:
```
GitHub:  A → B → C → D   (teammate added GitHub Change section)
Local:   A → B → C → E   (we added Local Change section)
```

---

### Step 5: Try to Push — REJECTED! 💥

```bash
git push
```

**Output:**
```
! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/saftab4-arch/git-mastery.git'
hint: Updates were rejected because the remote contains work that you
hint: do not have locally. Use 'git pull' before pushing again.
```

**Why rejected?**
```
Git protects you from overwriting teammates' work.
GitHub has commit D that you don't have locally.
You cannot push E on top of C when D already exists on GitHub.
You must first PULL D, combine it with E, then push.
```

---

### Step 6: Pull — Conflict Appears! 💥

```bash
git pull origin main
```

**Output:**
```
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

Git tried to auto-merge but couldn't — both versions changed the same lines.

**What the conflict looks like inside README.md:**
```
<<<<<<< HEAD
## Local Change
This line was added locally by me
=======
## GitHub Change
This line was added directly on GitHub by teammate
>>>>>>> fc7dec89b26903e179c6700d66f21e0380d1f774
```

**Conflict markers explained:**
```
<<<<<<< HEAD        = YOUR version (local)
=======             = DIVIDER between versions
>>>>>>> abc123...   = THEIR version (GitHub/remote)
```

---

### Step 7: Resolve the Conflict

Opened the file in nano and manually resolved:

```bash
nano README.md
```

**Action taken:** Removed all 3 conflict markers and kept BOTH versions:

```markdown
## Local Change
This line was added locally by me

## GitHub Change
This line was added directly on GitHub by teammate
```

**3 things to always do when resolving:**
1. Delete `<<<<<<< HEAD`
2. Delete `=======`
3. Delete `>>>>>>> abc123...`
4. Keep whichever content you want (one, both, or neither)

---

### Step 8: Stage, Commit and Push

```bash
# Stage the resolved file
git add README.md

# Commit the resolution
git commit -m "resolve: merged local and GitHub README conflict"

# Now push successfully!
git push origin main
```

**Output:**
```
To https://github.com/saftab4-arch/git-mastery.git
   fc7dec8..1692056  main -> main  ✅
```

**Final history:**
```
1692056 (HEAD → main) resolve: merged local and GitHub README conflict
fc7dec8 docs: GitHub Change added by teammate
f486681 local: added my changes
b76dee5 Update README.md
889e4d2 Initial commit
```

---

## 📊 Key Takeaways

### When Does Push Get Rejected?

```
ACCEPTED ✅ — Your local is AHEAD of GitHub:
GitHub:  A → B
Local:   A → B → C  ← you're ahead, fast forward push works!

REJECTED ❌ — Histories have DIVERGED:
GitHub:  A → B → C → D  ← someone else pushed
Local:   A → B → C → E  ← you committed locally
         Must pull first, resolve, then push!
```

### Conflict Rule

| Same File? | Same Line? | Result |
|-----------|-----------|--------|
| ❌ Different files | ✅ Same line | ✅ No Conflict |
| ✅ Same file | ❌ Different lines | ✅ Auto-merged |
| ✅ Same file | ✅ Same line | 💥 CONFLICT |

### Golden Rules

```
1. Always git pull before starting work each day
2. Never edit files directly on GitHub if others are working locally
3. Conflicts are NORMAL — don't panic, just resolve the markers
4. git status always shows which files have conflicts
5. After resolving: git add → git commit → git push
```

---

## 🛠️ Commands Used in This Project

```bash
git clone <url>                   # Copy repo locally
git status                        # Check current state
git add README.md                 # Stage file
git commit -m "message"           # Save snapshot
git push                          # Send to GitHub
git pull origin main              # Get GitHub changes
git log --oneline                 # See history
nano README.md                    # Edit file in terminal
```

---

## 🔗 Related

- Full Git Mastery Guide (Session 1–3): [GIT-MASTERY-COMPLETE.md](./GIT-MASTERY-COMPLETE.md)
- GitHub Profile: [github.com/saftab4-arch](https://github.com/saftab4-arch)

---

*This project is part of my DevOps portfolio — hands-on Git practice with real conflict resolution.*
*Every step was actually executed in the terminal, not just documented.*
