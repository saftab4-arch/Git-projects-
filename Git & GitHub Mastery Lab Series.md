# Git & GitHub Mastery Lab Series (Days 22–26)

## Project Overview

This repository documents a structured Git and GitHub learning journey focused on developing practical, job-ready skills for Cloud Engineering, DevOps, and Linux Administration roles.

The labs progressed from Git fundamentals to advanced GitHub workflows, including branch management, merge conflict resolution, SSH authentication, GitHub integration, Pull Requests, and GitHub CLI administration from a Linux environment.

All exercises were performed in a hands-on lab environment with real repositories, real GitHub integration, and real-world workflows that closely mirror professional software development and DevOps teams.

---

# Learning Objectives

By completing this lab series, the following objectives were achieved:

* Understand Git architecture and version control concepts
* Track file and code changes using commits
* View and analyze repository history
* Restore files and recover from mistakes
* Create and manage branches
* Merge branches safely
* Resolve merge conflicts
* Connect local repositories to GitHub
* Configure SSH authentication
* Manage remote repositories
* Create and manage Pull Requests
* Use GitHub CLI from Linux
* Understand GitHub workflow automation concepts
* Follow professional feature branch development workflows

---

# Environment

| Component               | Details          |
| ----------------------- | ---------------- |
| Operating System        | Ubuntu Linux     |
| Development Environment | Docker Container |
| Version Control System  | Git 2.53.0       |
| GitHub CLI              | 2.46.0           |
| Authentication Method   | SSH              |
| Repository Platform     | GitHub           |

---

# Day 22 – Git Fundamentals

## Topics Covered

### Repository Initialization

Created Git repositories from scratch:

```bash
git init
```

### Tracking Repository Status

Verified repository state:

```bash
git status
```

### Adding Files to Staging

```bash
git add file.txt
git add .
```

### Creating Commits

```bash
git commit -m "Initial commit"
```

### Viewing Commit History

```bash
git log
git log --oneline
```

## Skills Learned

* Git repository structure
* Working directory
* Staging area
* Commit lifecycle
* Version tracking fundamentals

---

# Day 23 – File Recovery and History Management

## Topics Covered

### Restoring Files

Restore uncommitted changes:

```bash
git restore filename
```

### Unstaging Files

```bash
git restore --staged filename
```

### Reviewing Changes

```bash
git diff
```

### Viewing Commit Details

```bash
git show
```

## Skills Learned

* Recovering from mistakes
* File restoration workflows
* Commit inspection
* Change tracking

---

# Day 24 – Branching and Merging

## Topics Covered

### Creating Branches

Modern Git workflow:

```bash
git switch -c feature-branch
```

Legacy equivalent:

```bash
git checkout -b feature-branch
```

### Viewing Branches

```bash
git branch
```

### Switching Branches

```bash
git switch main
```

### Merging Branches

```bash
git merge feature-branch
```

## Skills Learned

* Branch isolation
* Feature development workflow
* Safe code integration
* Parallel development concepts

---

# Day 25 – Merge Conflict Resolution and GitHub Integration

## Topics Covered

### Merge Conflict Resolution

Identified conflicts:

```bash
git status
```

Resolved conflicting files manually.

Completed merge:

```bash
git add .
git commit
```

### Remote Repository Management

Added GitHub repository:

```bash
git remote add origin <repository>
```

Verified remote configuration:

```bash
git remote -v
```

### SSH Authentication

Generated SSH key pair:

```bash
ssh-keygen -t ed25519
```

Viewed public key:

```bash
cat ~/.ssh/id_ed25519.pub
```

Tested GitHub connectivity:

```bash
ssh -T git@github.com
```

### Push Operations

```bash
git push -u origin main
```

## Skills Learned

* Conflict resolution workflow
* SSH authentication
* GitHub integration
* Remote repository management
* Secure Git operations

---

# Day 26 – GitHub CLI Administration

## Overview

This lab focused on managing GitHub directly from the Linux terminal using GitHub CLI.

The workflow simulated real DevOps and Cloud Engineering environments where engineers frequently work from Linux systems, cloud instances, containers, and remote servers.

---

## GitHub CLI Authentication

### Login

```bash
gh auth login
```

### Verify Authentication

```bash
gh auth status
```

## Repository Management

### Create Repository

```bash
gh repo create
```

### View Repository

```bash
gh repo view
```

## Issue Management

### List Issues

```bash
gh issue list
```

### Create Issue

```bash
gh issue create
```

### View Issue

```bash
gh issue view 1
```

Docker/Linux-friendly alternative:

```bash
gh issue view 1 --json url
```

---

## Feature Branch Workflow

### Create Feature Branch

```bash
git switch -c feature-readme
```

### Stage Changes

```bash
git add README.md
```

### Commit Changes

```bash
git commit -m "Add GitHub CLI lab documentation"
```

### Push Branch

```bash
git push -u origin feature-readme
```

---

## Pull Request Workflow

### Create Pull Request

```bash
gh pr create
```

### View Pull Requests

```bash
gh pr list
```

### View Pull Request

```bash
gh pr view 2
```

Docker/Linux-friendly alternative:

```bash
gh pr view 2 --json title,state,url,headRefName,baseRefName
```

### Merge Pull Request

```bash
gh pr merge 2
```

### Merge Strategies Learned

#### Merge Commit

Preserves complete branch history.

#### Rebase and Merge

Creates linear history.

#### Squash and Merge

Combines all commits into a single clean commit.

Selected merge method:

```text
Squash and Merge
```

---

## GitHub Actions Visibility

### View Workflow Runs

```bash
gh run list
```

Purpose:

* View CI/CD pipeline runs
* Monitor workflow execution
* Troubleshoot automation failures

---

# Real-World Workflow Practiced

```text
Issue Created
        ↓
Feature Branch Created
        ↓
Code Changes
        ↓
Commit
        ↓
Push
        ↓
Pull Request
        ↓
Code Review
        ↓
Merge
        ↓
Branch Deletion
```

This workflow mirrors the development process used by modern software engineering, DevOps, and cloud teams.

---

# Key Git Commands Mastered

```bash
git init
git status
git add
git commit
git log
git log --oneline
git diff
git show
git restore
git restore --staged
git switch
git branch
git merge
git remote add
git remote -v
git push
git pull
```

---

# Key GitHub Commands Mastered

```bash
gh auth login
gh auth status

gh repo create
gh repo view

gh issue create
gh issue list
gh issue view

gh pr create
gh pr list
gh pr view
gh pr merge

gh run list
```

---

# Skills Demonstrated

### Git

* Repository Management
* Commit Management
* Change Tracking
* Branching
* Merging
* Conflict Resolution
* File Recovery

### GitHub

* Repository Administration
* SSH Authentication
* Remote Management
* Pull Request Workflow
* Issue Tracking
* GitHub CLI Usage

### DevOps Practices

* Feature Branch Development
* Change Review Process
* Source Control Best Practices
* Linux-Based Development Workflow
* GitHub Actions Awareness
* Terminal-Based Repository Management

---

# Outcome

By completing this Git & GitHub Mastery Lab Series, practical experience was gained in source control, collaboration workflows, GitHub administration, and modern development practices used across Cloud Engineering, DevOps, Site Reliability Engineering (SRE), and Software Engineering teams.

The skills practiced throughout these labs form the foundation for future work involving:

* AWS
* Docker
* Kubernetes
* Terraform
* CI/CD Pipelines
* Infrastructure as Code (IaC)
* Cloud Automation
* DevOps Engineering
