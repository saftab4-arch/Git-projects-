# Git Assignment – Local Repository, GitHub, and SSH Authentication

## Overview

This project demonstrates the complete workflow of connecting a local Git repository to GitHub using SSH authentication.

The objective was to learn how to:

* Create a local Git repository
* Create a GitHub repository
* Generate SSH keys
* Add a public SSH key to GitHub
* Connect a local repository to a remote repository
* Push local commits to GitHub
* Pull remote changes from GitHub

---

## Technologies Used

* Git
* GitHub
* SSH
* Ubuntu Linux

---

## Step 1 – Create Local Repository

```bash
mkdir git-assignment
cd git-assignment

git init
```

Created a new local Git repository.

---

## Step 2 – Create GitHub Repository

Created a new repository on GitHub:

```text
git-assignment
```

The repository was created without a README or license to allow pushing an existing local repository.

---

## Step 3 – Generate SSH Keys

Generated a new SSH key pair:

```bash
ssh-keygen -t ed25519 -C "syed@gmail.com"
```

Explanation:

* `ssh-keygen` = SSH Key Generator
* `-t` = Key Type
* `ed25519` = Modern encryption algorithm
* `-C` = Comment/Label attached to the key

Generated files:

```text
~/.ssh/id_ed25519
~/.ssh/id_ed25519.pub
```

---

## Step 4 – Add Public Key To GitHub

Displayed the public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Copied the output and added it to:

```text
GitHub
→ Settings
→ SSH and GPG Keys
→ New SSH Key
```

---

## Step 5 – Verify SSH Authentication

Tested SSH connectivity:

```bash
ssh -T git@github.com
```

Successful output:

```text
Hi saftab4-arch! You've successfully authenticated,
but GitHub does not provide shell access.
```

This confirmed that GitHub recognized the SSH key and authentication was working.

---

## Step 6 – Add Remote Origin

Connected the local repository to GitHub:

```bash
git remote add origin git@github.com:saftab4-arch/git-assignment.git
```

Verified remote configuration:

```bash
git remote -v
```

---

## Step 7 – Push Local Repository

Created the initial commit:

```bash
git add .
git commit -m "Initial commit"
```

Pushed to GitHub:

```bash
git push -u origin main
```

---

## Step 8 – Pull Remote Changes

Modified the repository on GitHub and then synchronized the local repository:

```bash
git pull
```

This downloaded and merged remote changes into the local repository.

---

## Key Concepts Learned

### Git Repository Initialization

```bash
git init
```

Creates a new local Git repository.

### SSH Authentication

Uses a private/public key pair to securely authenticate with GitHub without entering a username and password.

### Remote Repository

A remote repository allows Git to synchronize code between local and cloud-based repositories.

### Push

```bash
git push
```

Uploads local commits to GitHub.

### Pull

```bash
git pull
```

Downloads and merges changes from GitHub.

---

## Skills Demonstrated

* Git Fundamentals
* GitHub Repository Management
* SSH Authentication
* Remote Repository Configuration
* Git Push and Pull Operations
* Linux Command Line Usage

---

## Outcome

Successfully created a local Git repository, connected it to GitHub using SSH authentication, pushed local commits to GitHub, and pulled remote changes back to the local system.
