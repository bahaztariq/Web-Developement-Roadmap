# 🔀 Git & GitHub

## Summary

This document covers Git (distributed version control system) and GitHub (web-based hosting service). Topics include Git basics (staging, committing, history), branching and merging strategies, rebasing, stashing, undoing changes, remote repository management, GitHub collaboration features (forking, pull requests), GitHub Actions for CI/CD, and best practices for commit messages and branching workflows.

## Sommaire

- [1. Introduction](#1-introduction)
  - [Definition](#definition)
  - [Git Workflow Overview](#git-workflow-overview)
  - [Centralized vs Distributed VCS](#centralized-vs-distributed-vcs)
  - [Git vs GitHub](#git-vs-github)
  - [Installing Git](#installing-git)
  - [Basic Configuration](#basic-configuration)
- [2. Git Basics](#2-git-basics)
  - [Definition](#definition)
  - [The Three-Tree Architecture](#the-three-tree-architecture)
  - [Git Commands Reference](#git-commands-reference)
  - [Initializing a Repository](#initializing-a-repository)
  - [Checking Status](#checking-status)
  - [Staging Files](#staging-files)
  - [Committing Changes](#committing-changes)
  - [Viewing History](#viewing-history)
  - [Viewing Changes](#viewing-changes)
  - [Removing and Moving Files](#removing-and-moving-files)
- [3. .gitignore](#3-gitignore)
  - [Definition](#definition)
  - [Why Use .gitignore](#why-use-gitignore)
  - [Creating .gitignore](#creating-gitignore)
  - [Pattern Syntax](#pattern-syntax)
  - [Common .gitignore Patterns](#common-gitignore-patterns)
  - [Global Gitignore](#global-gitignore)
  - [.gitkeep](#gitkeep)
- [4. Branching](#4-branching)
  - [Definition](#definition)
  - [Branch Architecture](#branch-architecture)
  - [Creating and Switching Branches](#creating-and-switching-branches)
  - [Deleting Branches](#deleting-branches)
  - [Renaming Branches](#renaming-branches)
  - [Branch Naming Conventions](#branch-naming-conventions)
- [5. Merging](#5-merging)
  - [Definition](#definition)
  - [Merge Types Comparison](#merge-types-comparison)
  - [Performing a Merge](#performing-a-merge)
  - [Merge Conflicts](#merge-conflicts)
  - [Viewing Merge History](#viewing-merge-history)
- [6. Rebasing](#6-rebasing)
  - [Definition](#definition)
  - [Rebase vs Merge: Visual Comparison](#rebase-vs-merge-visual-comparison)
  - [Performing a Rebase](#performing-a-rebase)
  - [Interactive Rebase](#interactive-rebase)
  - [Handling Rebase Conflicts](#handling-rebase-conflicts)
  - [Golden Rule of Rebase](#golden-rule-of-rebase)
- [7. Stashing](#7-stashing)
  - [Definition](#definition)
  - [Stash Workflow Architecture](#stash-workflow-architecture)
  - [Stashing Specific Changes](#stashing-specific-changes)
  - [Creating a Branch from Stash](#creating-a-branch-from-stash)
  - [Stash Workflow Example](#stash-workflow-example)
- [8. Undoing Changes](#8-undoing-changes)
  - [Definition](#definition)
  - [Undo Commands at Different Stages](#undo-commands-at-different-stages)
  - [Reset Modes Comparison](#reset-modes-comparison)
  - [Visual Summary Table](#visual-summary-table)
  - [Discarding Working Changes](#discarding-working-changes)
  - [Reset Command (modifies history)](#reset-command-modifies-history)
  - [Revert (safe for shared history)](#revert-safe-for-shared-history)
  - [Reflog (safety net)](#reflog-safety-net)
  - [Cleaning Untracked Files](#cleaning-untracked-files)
  - [Choosing the Right Tool](#choosing-the-right-tool)
- [9. Remote Repositories](#9-remote-repositories)
  - [Definition](#definition)
  - [Remote Repository Sync Architecture](#remote-repository-sync-architecture)
  - [Fetch vs Pull vs Push](#fetch-vs-pull-vs-push)
  - [Pushing Changes](#pushing-changes)
  - [Pulling Changes](#pulling-changes)
  - [Fetching Changes](#fetching-changes)
  - [Cloning Repositories](#cloning-repositories)
  - [SSH vs HTTPS](#ssh-vs-https)
  - [Tracking Branches](#tracking-branches)
- [10. GitHub Collaboration](#10-github-collaboration)
  - [Definition](#definition)
  - [GitHub Pull Request Workflow](#github-pull-request-workflow)
  - [Forking](#forking)
  - [Pull Requests (PRs)](#pull-requests-prs)
- [Summary](#summary)
- [Changes](#changes)
- [Testing](#testing)
- [Related Issues](#related-issues)
  - [Code Reviews](#code-reviews)
  - [Issues](#issues)
- [Description](#description)
- [Steps to Reproduce](#steps-to-reproduce)
- [Expected Behavior](#expected-behavior)
- [Actual Behavior](#actual-behavior)
- [Screenshots](#screenshots)
- [Environment](#environment)
  - [Branch Protection Rules](#branch-protection-rules)
- [11. GitHub Features](#11-github-features)
  - [Definition](#definition)
  - [README.md](#readmemd)
- [Features](#features)
- [Installation](#installation)
- [Usage](#usage)
- [API Documentation](#api-documentation)
- [Contributing](#contributing)
- [License](#license)
  - [GitHub Pages](#github-pages)
  - [GitHub Actions (Basics)](#github-actions-basics)
  - [Releases](#releases)
- [12. Best Practices](#12-best-practices)
  - [Definition](#definition)
  - [Commit Message Guidelines](#commit-message-guidelines)
  - [General Best Practices](#general-best-practices)
  - [Git Flow vs GitHub Flow](#git-flow-vs-github-flow)
  - [Additional Tools](#additional-tools)
- [Quick Reference](#quick-reference)



> Version control and collaboration tools for professional software development.

---

## 1. Introduction

### Definition
Version control tracks changes to files over time, allowing you to recall specific versions later. Git is a distributed version control system; GitHub is a web-based hosting service for Git repositories.

### Git Workflow Overview

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         GIT WORKFLOW OVERVIEW                           │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                         │
│   Working Directory     Staging Area (Index)      Repository            │
│   ┌──────────────┐      ┌──────────────┐          ┌──────────────┐     │
│   │              │      │              │          │              │     │
│   │  Modify      │      │  git add     │          │  git commit  │     │
│   │  files       │──────│  (Stage      │──────────│  (Save to    │     │
│   │              │      │  changes)    │          │  history)    │     │
│   │  untracked   │      │              │          │              │     │
│   │  modified    │      │  staged      │          │  committed   │     │
│   │              │      │  changes     │          │  snapshot    │     │
│   └──────────────┘      └──────────────┘          └──────────────┘     │
│          │                     │                         │              │
│          │ <────────────────── │                         │              │
│          │  git restore        │                         │              │
│          │  --staged           │                         │              │
│          │                     │                         │              │
│          │ <─────────────────────────────────────────────               │
│          │  git checkout / git restore                                    │
│          │  (discard changes)                                           │
│                                                                         │
└─────────────────────────────────────────────────────────────────────────┘
```

### Centralized vs Distributed VCS

**Definition:** In a **Centralized VCS** (like SVN), a single server holds the full version history; users check out only the latest version. In a **Distributed VCS** (like Git), every user has a full copy of the repository (including history) locally, allowing offline work and robust branching/merging.

```
Centralized Version Control System (CVCS)
═══════════════════════════════════════════════════════════════════════

    ┌──────────────────────────────────────────────────────────┐
    │                    Central Server                        │
    │              (Single Point of Failure)                   │
    │                   ┌──────────┐                           │
    │                   │  SVN DB  │                           │
    │                   │  (Full   │                           │
    │                   │ History) │                           │
    │                   └────┬─────┘                           │
    └────────────────────────┬─────────────────────────────────┘
                             │
            ┌────────────────┼────────────────┐
            │                │                │
            ▼                ▼                ▼
     ┌──────────┐      ┌──────────┐      ┌──────────┐
     │  User A  │      │  User B  │      │  User C  │
     │  (Working│      │  (Working│      │  (Working│
     │  Copy)   │      │  Copy)   │      │  Copy)   │
     └──────────┘      └──────────┘      └──────────┘

   Pros: Simple permissions, centralized control
   Cons: Requires network connection, single point of failure


Distributed Version Control System (DVCS) - Git
═══════════════════════════════════════════════════════════════════════

   ┌──────────┐                              ┌──────────┐
   │  User A  │◄────────────────────────────►│  User B  │
   │(Full Repo│      (peer-to-peer)          │(Full Repo│
   │  History)│                              │  History)│
   └────┬─────┘                              └────┬─────┘
        │                                         │
        │                                         │
        │         ┌──────────────┐                │
        └────────►│  Remote      │◄───────────────┘
                  │ Repository   │
                  │ (GitHub,     │
                  │  GitLab,     │
                  │  etc.)       │
                  └──────┬───────┘
                         │
        ┌────────────────┼────────────────┐
        │                │                │
        ▼                ▼                ▼
   ┌──────────┐     ┌──────────┐     ┌──────────┐
   │  User C  │     │  User D  │     │  User E  │
   │(Full Repo│     │(Full Repo│     │(Full Repo│
   │  History)│     │  History)│     │  History)│
   └──────────┘     └──────────┘     └──────────┘

   Pros: Works offline, complete backup, faster operations
   Cons: Larger repository size, steeper learning curve
```

### Git vs GitHub

**Definition:** **Git** is the local version control software that tracks changes on your machine. **GitHub** is a cloud-based hosting service for Git repositories, adding collaboration features like Pull Requests, Issues, and remote backup. You use Git *without* GitHub, but GitHub requires Git.

```
┌─────────────────────────────────────────────────────────────────┐
│  Git                                                            │
│  - Software running locally                                     │
│  - Tracks file changes                                          │
│  - Works offline                                                │
│  - Commands: git init, git commit, git branch                   │
└─────────────────────────────────────────────────────────────────┘
                              │
                              │ (push/pull)
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│  GitHub                                                         │
│  - Web-based hosting service                                    │
│  - Remote repository storage                                    │
│  - Collaboration features (PRs, Issues, Actions)                │
│  - Web interface: github.com                                    │
└─────────────────────────────────────────────────────────────────┘
```

### Installing Git

**Definition:** Installing Git sets up the necessary command-line tools (and sometimes GUI clients) on your operating system. It allows you to run `git` commands in your terminal. Installation methods vary by OS (Homebrew for macOS, installer for Windows, package manager for Linux).

```bash
# macOS (using Homebrew)
brew install git

# Windows
# Download from: https://git-scm.com/download/win
# Or use winget: winget install --id Git.Git

# Linux (Debian/Ubuntu)
sudo apt update && sudo apt install git

# Linux (Fedora)
sudo dnf install git

# Verify installation
git --version
```

### Basic Configuration

```bash
# Set your name and email (required for commits)
git config --global user.name "Your Name"
git config --global user.email "you@example.com"

# Set default branch name to 'main'
git config --global init.defaultBranch main

# Set default text editor (VS Code)
git config --global core.editor "code --wait"

# Enable colored output
git config --global color.ui auto

# View all configurations
git config --list

# View a specific config value
git config user.name
```

**Configuration Levels:**
- `--system` - All users on the machine
- `--global` - Current user (stored in `~/.gitconfig`)
- `--local` - Current repository (stored in `.git/config`)

---

## 2. Git Basics

### Definition
Git is a distributed version control system that tracks file changes through three distinct areas. The working directory contains your current files, the staging area (index) holds changes prepared for commit, and the repository stores committed snapshots in a directed acyclic graph (DAG) of commits.

### The Three-Tree Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      GIT THREE-TREE ARCHITECTURE                            │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│                                                                 HEAD        │
│                                                                   │         │
│                                                                   ▼         │
│   Working Directory        Staging Area           Local Repository          │
│   (Working Tree)           (Index)                (HEAD)                    │
│   ┌──────────────┐         ┌──────────────┐       ┌──────────────┐         │
│   │              │  git add │              │ git   │              │         │
│   │   Modified   │─────────►│   Staged     │commit │   Committed  │         │
│   │   Files      │          │   Changes    │──────►│   History    │         │
│   │              │          │              │       │              │         │
│   │ file.txt     │          │ file.txt     │       │ file.txt     │         │
│   │ + new line   │          │ + new line   │       │ + new line   │         │
│   │              │          │              │       │              │         │
│   │ status:      │          │ status:      │       │ status:      │         │
│   │ modified     │          │ staged       │       │ committed    │         │
│   └──────┬───────┘          └──────┬───────┘       └──────┬───────┘         │
│          │                         │                     │                 │
│          │◄────────────────────────│                     │                 │
│          │  git restore --staged   │                     │                 │
│          │  (unstage changes)      │                     │                 │
│          │                                               │                 │
│          │◄──────────────────────────────────────────────│                 │
│          │  git checkout HEAD -- file.txt                │                 │
│          │  (discard all changes)                        │                 │
│          │                                               │                 │
│          │◄────────────────────────────────────────────────                 │
│          │  git restore .                              (discard all)       │
│                                                                             │
│   File Lifecycle in Git:                                                    │
│   ┌─────────┐   untracked   ┌─────────┐                                     │
│   │ Untracked│──────────────►│  Tracked│                                     │
│   │          │◄──────────────│         │                                     │
│   └──────────┘  git rm --cached                                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Git Commands Reference

| Command | Description | Use Case |
|---------|-------------|----------|
| `git init` | Initialize repository | Start tracking a new project |
| `git clone` | Clone repository | Download existing repo from remote |
| `git status` | Check status | See changed/staged files |
| `git add` | Stage files | Prepare changes for commit |
| `git commit` | Commit changes | Save snapshot of staged changes |
| `git push` | Push to remote | Upload local commits to server |
| `git pull` | Pull from remote | Download and merge remote changes |
| `git branch` | Manage branches | List, create, or delete branches |
| `git checkout` | Switch context | Switch branches or restore files |
| `git merge` | Merge branch | Combine history of two branches |
| `git log` | View history | Show commit logs |
| `git diff` | View changes | Show file differences |

### Initializing a Repository


**Definition:** `git init` creates a new, empty Git repository or reinitializes an existing one. It creates a hidden `.git` directory in the project root, which stores all version control metadata and object history. This turns a regular folder into a tracked Git project.

```bash
# Create a new Git repository
git init

# Output: Initialized empty Git repository in /path/.git/

# Initialize with a specific branch name
git init --initial-branch=main
```

### Checking Status

**Definition:** `git status` displays the state of the working directory and the staging area. It shows which files have been modified, which are staged for the next commit, and which are untracked. It is the most frequently used command to understand the current context.

```bash
# View the current state of your repository
git status

# Short status (compact format)
git status -s
# ?? file.txt    (untracked)
# A  file.txt    (added to staging)
# M  file.txt    (modified)
# D  file.txt    (deleted)
```

### Staging Files

**Definition:** Staging (using `git add`) prepares changes for a commit. It allows you to selectively choose which file modifications (or even specific lines) will be part of the next snapshot. This "Staging Area" (or Index) acts as a buffer between your working directory and the repository history.

```bash
# Stage a single file
git add filename.txt

# Stage all files in current directory
git add .

# Stage all changes (including deletions)
git add -A
git add --all

# Stage only modified and deleted files, not new files
git add -u

# Interactively stage changes
git add -p
```

### Committing Changes

**Definition:** A commit (`git commit`) captures a snapshot of the project's currently staged changes. Each commit has a unique ID (SHA-1 hash), a timestamp, an author, and a descriptive message. Commits form the permanent history of the project.

```bash
# Commit staged changes with a message
git commit -m "Add user authentication feature"

# Stage and commit all tracked files in one command
git commit -am "Fix login bug"

# Commit with a more detailed message
git commit -m "Add user authentication" -m "- Implemented JWT tokens
- Added password hashing
- Created login/logout endpoints"

# Amend the last commit (change message or add files)
git commit --amend -m "New commit message"
```

**Commit Message Best Practices:**
- Use imperative mood: "Add feature" not "Added feature"
- Keep the first line under 50 characters
- Add details after a blank line if needed
- Reference issues: "Fix login bug #123"

### Viewing History

**Definition:** `git log` shows the commit history of the repository. It lists commits in reverse chronological order, displaying the hash, author, date, and message. Various flags (like `--oneline`, `--graph`) help visualize branch structures and merge history.

```bash
# View commit history
git log

# Compact view (one line per commit)
git log --oneline

# Graph view with branches
git log --oneline --graph --all

# View last N commits
git log -5

# View commits with statistics
git log --stat

# View commits by author
git log --author="John Doe"

# View commits since a date
git log --since="1 week ago"

# Pretty format
git log --pretty=format:"%h - %an, %ar : %s"
```

### Viewing Changes

**Definition:** `git diff` shows the specific line-by-line changes between files. It can compare the working directory to the staging area (what you *haven't* staged yet), the staging area to the last commit, or the differences between any two commits or branches.

```bash
# Show unstaged changes (working directory vs staging)
git diff

# Show staged changes (staging vs last commit)
git diff --staged
git diff --cached

# Show changes for a specific file
git diff filename.txt

# Show changes between two commits
git diff commit1..commit2

# Show changes introduced by a specific commit
git show commit-hash
```

### Removing and Moving Files

**Definition:** `git rm` removes files from both the working directory and the index (staging them for deletion). `git mv` renames or moves files and automatically stages the change. Using these standard commands ensures Git tracks the operation correctly rather than seeing a separate "delete" and "new file".

```bash
# Remove file from working directory and stage deletion
git rm filename.txt

# Remove file from staging but keep in working directory
git rm --cached filename.txt

# Rename/move a file (preserves history)
git mv oldname.txt newname.txt
```

---

## 3. .gitignore

### Definition
The `.gitignore` file specifies patterns for files Git should ignore, preventing untracked files from being staged or committed. It acts as a filter to exclude temporary files, build artifacts, sensitive data (API keys, passwords), IDE configurations, and operating system files from version control, keeping the repository clean and secure.

### Why Use .gitignore

**Definition:** A `.gitignore` file tells Git which files or directories to intentionally ignore and exclude from version control. This is critical for preventing build artifacts, dependencies (`node_modules`), secrets (`.env`), and system files (`.DS_Store`) from polluting the repository.

```
WITHOUT .gitignore                    WITH .gitignore
═══════════════════                   ═══════════════

Repository:                           Repository:
┌──────────────────┐                  ┌──────────────────┐
│ my-project/      │                  │ my-project/      │
│ ├── src/         │                  │ ├── src/         │
│ ├── dist/        │  ❌ Cluttered    │ ├── dist/        │  (ignored)
│ ├── node_modules/│  ❌ Huge         │ ├── node_modules/│  (ignored)
│ ├── .env         │  ❌ Security risk│ ├── .env         │  (ignored)
│ ├── .DS_Store    │  ❌ OS files     │ ├── .DS_Store    │  (ignored)
│ ├── *.log        │  ❌ Temp files   │ ├── *.log        │  (ignored)
│ ├── .idea/       │  ❌ IDE config   │ ├── .idea/       │  (ignored)
│ └── .gitignore   │  ✅ Missing!     │ └── .gitignore   │  ✅ Clean!
└──────────────────┘                  └──────────────────┘

Size: ~500MB+                         Size: ~2MB
Commits: Full of noise                Commits: Focused on code
Security: Exposed secrets             Security: Protected
```

### Creating .gitignore

**Definition:** The `.gitignore` file is a plain text file placed in the repostory root (or subdirectories). Each line contains a pattern for files/directories to ignore. It affects untracked files only; files already tracked by Git are not ignored even if they match a pattern.

```bash
# Create a .gitignore file
touch .gitignore

# Edit it in your preferred editor
code .gitignore
```

### Pattern Syntax

```gitignore
# Comment - lines starting with # are ignored

# Ignore specific file
secret.txt

# Ignore all files with extension
*.log
*.tmp

# Ignore directory (trailing slash)
node_modules/
build/
dist/

# Ignore files in specific directories
temp/*.txt

# Ignore all .txt files anywhere
temp/**/*.txt

# Negation - don't ignore this file
!important.log

# Ignore files starting with dot
.*

# But track .gitignore itself
!.gitignore
```

### Common .gitignore Patterns

```gitignore
# Node.js
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
package-lock.json
.env
.env.local
.env.*.local

# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
env/
venv/
ENV/
*.egg-info/
dist/
build/

# macOS
.DS_Store
.AppleDouble
.LSOverride

# Windows
Thumbs.db
ehthumbs.db
Desktop.ini

# IDE
.vscode/
.idea/
*.swp
*.swo
*~

# Logs
logs/
*.log

# OS files
*.DS_Store
```

### Global Gitignore

**Definition:** A global `.gitignore` file applies ignore rules to *every* repository on your system. This is useful for user-specific OS files (like macOS `.DS_Store` or Windows `Thumbs.db`) or editor configuration files/folders (`.vscode/`, `.idea/`) that shouldn't be committed to any project.

```bash
# Create a global gitignore file
git config --global core.excludesfile ~/.gitignore_global

# Edit the global file
echo ".DS_Store" >> ~/.gitignore_global
echo "*.swp" >> ~/.gitignore_global
```

### .gitkeep

**Definition:** Git does not track empty directories. `.gitkeep` is a convention (not a Git feature) where an empty file (often named `.gitkeep`) is placed inside an empty directory to force Git to track the folder. Useful for ensuring directory structure exists in the repo even without content.

```bash
# Git doesn't track empty directories
# Create a .gitkeep file to track an otherwise empty folder
mkdir empty-folder
touch empty-folder/.gitkeep
```

---

## 4. Branching

### Definition
Branches are lightweight movable pointers to commits that enable parallel development. Unlike other VCSs, Git branches are simply references (40-byte files) pointing to a specific SHA-1 hash. This makes creating and switching branches nearly instantaneous, encouraging feature isolation and experimentation without risking the main codebase.

### Branch Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      GIT BRANCH POINTER MODEL                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│   Branches are just pointers to commits (lightweight ~40 bytes each)       │
│                                                                             │
│   .git/refs/heads/ contains:                                                │
│   - main: "abc1234..."  (40-char SHA-1 hash)                               │
│   - feature: "def5678..."                                                   │
│                                                                             │
│   Visual Representation:                                                    │
│                                                                             │
│   Commit History with Branch Pointers:                                      │
│                                                                             │
│        main ───────┐                                                        │
│                     ▼                                                       │
│   A──────B──────C──────F──────G  (main branch commits)                     │
│   │      │      │      │      │                                            │
│   └──────┴──────┼──────┴──────┘                                            │
│                 │                                                           │
│                 │  (branch created from C)                                  │
│                 ▼                                                           │
│                D──────E         (feature branch)                           │
│                        ▲                                                    │
│        feature ────────┘                                                    │
│                                                                             │
│   HEAD Pointer:                                                             │
│   ┌──────────────┐                                                          │
│   │ HEAD         │  Points to current branch                                │
│   │ ref: refs/   │  or directly to commit in "detached HEAD"                │
│   │ heads/main   │                                                          │
│   └──────────────┘                                                          │
│          │                                                                  │
│          ▼                                                                  │
│        main ──► C (abc1234)                                                 │
│                                                                             │
│   Creating a new branch:                                                    │
│   git branch feature  →  Creates new pointer at current commit              │
│   git checkout feature  →  Moves HEAD to point to "feature"                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Creating and Switching Branches

**Definition:** Branching allows you to diverge from the main line of development and verify/isolate changes without affecting the main codebase. `git branch` creates a new pointer to a commit. `git switch` (or `git checkout`) moves your HEAD pointer to that branch to start working on it.

```bash
# List all branches
git branch

# List all branches including remotes
git branch -a

# List branches with last commit
git branch -v

# Create a new branch
git branch feature-branch

# Create and switch to new branch
git checkout -b feature-branch

# Modern syntax (Git 2.23+)
git switch -c feature-branch

# Switch to existing branch
git checkout feature-branch
git switch feature-branch

# Switch to previous branch
git checkout -
git switch -
```

### Deleting Branches

**Definition:** `git branch -d` deletes a local branch. Git prevents deleting a branch if it contains unmerged changes (`-D` forces deletion). Pruning old feature branches keeps the repository clean and manageable.

```bash
# Delete a merged branch (safe)
git branch -d branch-name

# Force delete an unmerged branch ⚠️
git branch -D branch-name

# Delete remote branch
git push origin --delete branch-name
git push origin :branch-name
```

### Renaming Branches

**Definition:** `git branch -m` renames a branch. This is useful for correcting typos or updating branch names to follow a new convention. If you rename the current branch, you simply provide the new name.

```bash
# Rename current branch
git branch -m new-branch-name

# Rename another branch
git branch -m old-name new-name

# Rename local and remote branch
git branch -m old-name new-name
git push origin :old-name
git push -u origin new-name
```

### Branch Naming Conventions

```bash
# Feature branches
feature/user-authentication
feature/add-payment-gateway

# Bug fix branches
bugfix/login-error
bugfix/memory-leak

# Hotfix branches (urgent production fixes)
hotfix/security-patch
hotfix/critical-bug

# Release branches
release/v1.0.0
release/2024-01

# Personal/developer branches
username/feature-name
```

**Best Practices:**
- Use lowercase with hyphens (kebab-case)
- Include ticket numbers: `feature/JIRA-123-login`
- Keep names descriptive but concise
- Delete branches after merging

---

## 5. Merging

### Definition
Merging combines changes from one branch into another, integrating divergent work histories. Git performs merges by comparing the tips of branches and finding their common ancestor (merge base), then applying changes to produce a unified result. There are two primary merge strategies: fast-forward (simple pointer movement) and three-way merge (creating a merge commit).

### Merge Types Comparison

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        MERGE TYPES COMPARISON                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  FAST-FORWARD MERGE (Linear History)                                       │
│  ═══════════════════════════════════                                       │
│                                                                             │
│  Before Merge:                                                              │
│                                                                             │
│  main:      A────────B────────C                                            │
│                             ↑                                              │
│                            HEAD                                            │
│                                                                             │
│  feature:                    D────────E                                    │
│                                       ↑                                    │
│                                   (no new commits                          │
│                                    on main since                           │
│                                    branch created)                         │
│                                                                             │
│  Command: git checkout main && git merge feature                           │
│                                                                             │
│  After Merge:                                                               │
│                                                                             │
│  main:      A────────B────────C────────D────────E                          │
│                                                 ↑                          │
│                                                HEAD                        │
│                                                                             │
│  Result: main pointer simply moved forward to E (no merge commit)          │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  THREE-WAY MERGE (Divergent History)                                       │
│  ═══════════════════════════════════                                       │
│                                                                             │
│  Before Merge:                                                              │
│                                                                             │
│  main:      A────────B────────C────────F                                   │
│                                    ↑                                       │
│                                   HEAD                                     │
│                                  /                                         │
│                                 / (common ancestor)                        │
│                                /                                           │
│  feature:                    D────────E                                    │
│                                                                             │
│  Merge Base: Commit C (most recent common ancestor)                        │
│                                                                             │
│  Command: git checkout main && git merge feature                           │
│                                                                             │
│  After Merge:                                                               │
│                                                                             │
│  main:      A────────B────────C────────F────────M                          │
│                                    ↑             │                         │
│                                    └─────────────┘                         │
│                                              /                             │
│                                             /                              │
│  feature:                    D────────E────┘                               │
│                                                                             │
│  Result: New merge commit M with TWO parents (F and E)                     │
│          M contains combined changes from both branches                    │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  NO-FAST-FORWARD MERGE (--no-ff)                                           │
│  ═══════════════════════════════════                                       │
│                                                                             │
│  Even with fast-forward possible, force a merge commit:                    │
│                                                                             │
│  Before:           main: A──B──C                                           │
│                          feature:  D──E                                    │
│                                                                             │
│  After:            main: A──B──C──M  (M has two parents)                  │
│                                  │                                         │
│                                  └──────┐                                  │
│                                         ▼                                  │
│                          feature:    D──E                                  │
│                                                                             │
│  Use: git merge --no-ff feature                                            │
│  Benefits: Preserves feature branch history, clearer audit trail           │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Performing a Merge

**Definition:** Merging takes the independent lines of development from two branches and integrates them into a single branch. `git merge` adds the changes from the source branch to the current branch. A "merge commit" is created to tie the histories together (unless it's a fast-forward merge).

```bash
# Switch to the target branch (the one receiving changes)
git checkout main

# Merge feature branch into main
git merge feature-branch

# Merge with a custom message
git merge feature-branch -m "Merge feature: user auth"

# Create a merge commit even for fast-forward
git merge --no-ff feature-branch
```

### Merge Conflicts

**Definition:** A merge conflict occurs when Git cannot automatically resolve differences in code between two commits (e.g., the same line was changed differently in both branches). Git pauses the merge process and marks the conflicted files, requiring manual intervention to choose the correct version.

Conflicts occur when the same line in a file was modified differently in both branches.

```
<<<<<<< HEAD
This is the version in your current branch (main)
=======
This is the version in the branch you're merging (feature)
>>>>>>> feature-branch
```

**Resolving Conflicts:**

```bash
# When merge conflicts occur
git status  # Shows conflicted files

# Edit files to resolve conflicts manually
# Remove conflict markers (<<<<<<<, =======, >>>>>>>)

# Stage resolved files
git add filename.txt

# Complete the merge
git commit

# Or abort the merge
git merge --abort
```

**Using VS Code:**
- Click "Accept Current Change" (your branch)
- Click "Accept Incoming Change" (merging branch)
- Click "Accept Both Changes"
- Click "Compare Changes" to review

### Viewing Merge History

**Definition:** Viewing merge history helps visualize how branches have diverged and reintegrated. The `--graph` flag in `git log` draws a text-based representation of the commit history on the left side of the output, clearly showing merge points and branch structures.

```bash
# Show merge commits
git log --merges

# Show no-merges only
git log --no-merges

# Graph view with branches
git log --oneline --graph --all
```

---

## 6. Rebasing

### Definition
Rebasing moves or combines a sequence of commits to a new base commit, rewriting history to create a linear commit sequence. Unlike merging which creates a merge commit, rebasing re-applies commits on top of another base, creating new commits with different hashes (D', E' instead of D, E). This produces a cleaner, linear history but modifies commit identities.

### Rebase vs Merge: Visual Comparison

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    REBASE VS MERGE: COMPLETE COMPARISON                     │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ORIGINAL STATE: Both branches diverged from commit C                       │
│  ═══════════════════════════════════════════════════════                    │
│                                                                             │
│  main:      A────────B────────C────────F                                   │
│                             ↑                                              │
│                           (origin)                                         │
│                            /                                               │
│                           /                                                │
│  feature:                D────────E                                        │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  MERGE APPROACH: Preserves Complete History                                │
│  ═══════════════════════════════════════════════════════                    │
│                                                                             │
│  Result:      A───B───C───F───M  (M = merge commit)                        │
│                         ↑     │                                            │
│                        origin └────────┐                                   │
│                                        │                                   │
│                                        └──► D───E (feature preserved)      │
│                                                                             │
│  Pros:                                                                     │
│  ✓ Non-destructive, original commits intact                                │
│  ✓ Complete historical context preserved                                   │
│  ✓ Shows when parallel development occurred                                │
│  ✓ Safe for shared/public branches                                         │
│                                                                             │
│  Cons:                                                                     │
│  ✗ History becomes complex with many merges                                │
│  ✗ "Diamond" patterns make history harder to read                          │
│                                                                             │
│  Command: git checkout main && git merge feature                           │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  REBASE APPROACH: Linear History                                           │
│  ═══════════════════════════════════════════════════════                    │
│                                                                             │
│  Step 1: Rebase feature onto main                                          │
│  ┌────────────────────────────────────────────────────────────┐            │
│  │ git checkout feature                                       │            │
│  │ git rebase main                                            │            │
│  └────────────────────────────────────────────────────────────┘            │
│                                                                             │
│  What Happens:                                                             │
│  1. Temporarily save feature commits (D, E)                                │
│  2. Reset feature to point at main (commit F)                              │
│  3. Re-apply commits on top of F with NEW hashes                           │
│                                                                             │
│  After Rebase:                                                             │
│                                                                             │
│  main:       A───B───C───F                                                 │
│                                ↑                                           │
│  feature:                     D'───E'  (D', E' are NEW commits)            │
│                                                                             │
│  Step 2: Fast-forward merge                                                │
│  ┌────────────────────────────────────────────────────────────┐            │
│  │ git checkout main                                          │            │
│  │ git merge feature                                          │            │
│  └────────────────────────────────────────────────────────────┘            │
│                                                                             │
│  Final Result: A───B───C───F───D'───E'  (Perfectly linear!)                │
│                                                                             │
│  Pros:                                                                     │
│  ✓ Clean, linear history - easy to follow                                  │
│  ✓ No merge commits cluttering the log                                     │
│  ✓ Ideal for local cleanup before sharing                                  │
│                                                                             │
│  Cons:                                                                     │
│  ✗ Rewrites history - changes commit SHAs                                  │
│  ✗ DANGEROUS if commits already pushed to shared branch                    │
│  ✗ Requires force push if already published                                │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  ⚠️  GOLDEN RULE: Never rebase commits that exist outside your repo!       │
│                                                                             │
│  Safe:  git checkout my-local-feature && git rebase main                   │
│                                                                             │
│  DANGEROUS (don't do this!):                                               │
│  git checkout main                                                         │
│  git rebase origin/main  ← main is shared!                                 │
│  git push --force        ← Don't force push shared branches!               │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Performing a Rebase

**Definition:** Rebasing (`git rebase`) rewrites the commit history by moving the entire feature branch to begin on the tip of the main branch. This creates a linear history by re-applying commits one by one, eliminating the need for a merge commit.

```bash
# Switch to feature branch
git checkout feature-branch

# Rebase feature onto main
git rebase main

# This replays feature's commits on top of main
```

### Interactive Rebase

**Definition:** Interactive rebase (`git rebase -i`) is a powerful tool for cleaning up commit history before merging. It allows you to squash (combine), fixup, reorder, edit, or drop commits within a branch, ensuring the history is clean and follows logical steps.

```bash
# Rebase last 3 commits interactively
git rebase -i HEAD~3

# Rebase onto main interactively
git rebase -i main
```

**Interactive Commands:**

```
pick     - Use commit as-is
reword   - Use commit but edit message
edit     - Use commit but stop for amending
squash   - Combine with previous commit (keep both messages)
fixup    - Combine with previous commit (discard this message)
drop     - Remove commit
```

**Example Interactive Rebase:**

```bash
# Start interactive rebase
git rebase -i HEAD~4

# Editor opens with:
pick abc1234 First commit
pick def5678 Second commit
pick ghi9012 Third commit
pick jkl3456 Fourth commit

# Change to:
pick abc1234 First commit
squash def5678 Second commit
reword ghi9012 Third commit
fixup jkl3456 Fourth commit
```

### Handling Rebase Conflicts

**Definition:** Like merging, rebasing can encounter conflicts. Because rebasing replays commits one by one, you may have to resolve conflicts multiple times (once for each commit that conflicts). After resolving, you use `git rebase --continue` to proceed to the next commit.

```bash
# If conflicts occur during rebase
git status

# Resolve conflicts in files
# Stage resolved files
git add filename.txt

# Continue rebase
git rebase --continue

# Skip current commit
git rebase --skip

# Abort rebase and restore original state
git rebase --abort
```

### Golden Rule of Rebase

**Definition:** The Golden Rule states: **Never rebase public history.** Do not rebase commits that you have already pushed to a shared remote repository (like `main`), because rebasing rewrites commit hashes. This forces everyone else to fix their history, causing chaos for the team.

⚠️ **Never rebase commits that have been pushed to a public/shared branch.**

```bash
# Safe: Rebase your local feature branch
git checkout feature-branch
git rebase main

# Dangerous: Rebase after pushing
git push origin feature-branch
git rebase main  # DON'T DO THIS!
git push --force  # This rewrites shared history!
```

**When to Use Rebase:**
- Cleaning up local commits before pushing
- Keeping feature branch up to date with main
- Creating a linear history

**When to Use Merge:**
- Integrating completed features into main
- When working with shared branches
- When you want to preserve context

---

## 7. Stashing

### Definition
Stashing temporarily saves uncommitted changes (both staged and unstaged) onto a stack without creating a commit. This allows you to quickly switch contexts, pull updates, or switch branches without losing work-in-progress. Stashes are stored in `.git/refs/stash` and can be reapplied later to continue where you left off.

### Stash Workflow Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        STASH WORKFLOW DIAGRAM                               │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  SCENARIO: Working on feature, need to quickly switch to main for hotfix   │
│                                                                             │
│  Step 1: You have uncommitted work                                         │
│  ┌────────────────────────────────────────────────────────────┐            │
│  │ Working Directory:                                         │            │
│  │   M file1.txt (modified)                                   │            │
│  │   A file2.txt (added, staged)                              │            │
│  │   ?? file3.txt (untracked)                                 │            │
│  │                                                            │            │
│  │ Current Branch: feature-branch                             │            │
│  └────────────────────────────────────────────────────────────┘            │
│                                                                             │
│  Step 2: Stash your changes                                                │
│  ┌────────────────────────────────────────────────────────────┐            │
│  │ $ git stash push -m "WIP: login form validation"           │            │
│  │                                                            │            │
│  │ Changes stored to: stash@{0}                               │            │
│  │ Working directory is now clean!                            │            │
│  └────────────────────────────────────────────────────────────┘            │
│                                                                             │
│  Step 3: Stash is stored in stack                                          │
│  ┌────────────────────────────────────────────────────────────┐            │
│  │ Stash Stack (.git/refs/stash):                             │            │
│  │                                                            │            │
│  │ TOP → stash@{0}                                            │            │
│  │       Commit: abc1234 "WIP: login form validation"         │            │
│  │       ├─ file1.txt (changes)                               │            │
│  │       ├─ file2.txt (changes)                               │            │
│  │       └─ index state (staging info)                        │            │
│  │                                                            │            │
│  │       stash@{1}  (older stash)                             │            │
│  │       Commit: def5678 "WIP: database schema"               │            │
│  └────────────────────────────────────────────────────────────┘            │
│                                                                             │
│  Step 4: Switch branches and fix hotfix                                    │
│  ┌────────────────────────────────────────────────────────────┐            │
│  │ $ git checkout main                                        │            │
│  │ # fix urgent bug...                                        │            │
│  │ $ git commit -am "Hotfix: critical security issue"         │            │
│  └────────────────────────────────────────────────────────────┘            │
│                                                                             │
│  Step 5: Return and restore your work                                      │
│  ┌────────────────────────────────────────────────────────────┐            │
│  │ $ git checkout feature-branch                              │            │
│  │ $ git stash pop           # Apply and remove from stack    │            │
│  │                                                            │            │
│  │ OR: $ git stash apply     # Apply but keep in stack        │            │
│  └────────────────────────────────────────────────────────────┘            │
│                                                                             │
│  Complete Workflow Summary:                                                 │
│  ┌────────────────────────────────────────────────────────────┐            │
│  │                                                            │            │
│  │  [Working] ──git stash──► [Stash Stack] ──git stash pop──► │            │
│  │      │                         │                  │        │            │
│  │      │                    ┌────┴────┐             │        │            │
│  │      │                    ▼         ▼             │        │            │
│  │      │               stash@{0}   stash@{1}        │        │            │
│  │      │                    │         │             │        │            │
│  │      │                    └────┬────┘             │        │            │
│  │      │                         │                  │        │            │
│  │      │◄────────git stash apply─┘                  │        │            │
│  │      │                                            │        │            │
│  │      └────────────────────────────────────────────┘        │            │
│  │                          (apply)                           │            │
│  │                                                            │            │
│  └────────────────────────────────────────────────────────────┘            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

```bash
# Stash current changes
git stash

# Stash with a descriptive message
git stash push -m "Work in progress: login form"

# List all stashes
git stash list
# Output:
# stash@{0}: On feature-branch: Work in progress: login form
# stash@{1}: WIP on main: abc1234 Previous commit

# Apply most recent stash and remove it
git stash pop

# Apply most recent stash but keep it
git stash apply

# Apply specific stash
git stash apply stash@{1}

# Drop (delete) most recent stash
git stash drop

# Drop specific stash
git stash drop stash@{1}

# Clear all stashes ⚠️
git stash clear
```

### Stashing Specific Changes

**Definition:** By default, `git stash` saves all uncommitted changes. You can stash specific files or hunks using `git stash push -p` (interactive) or passing filenames, allowing you to selectively save unfinished work while ignoring other changes.

```bash
# Stash only staged changes
git stash --staged

# Stash including untracked files
git stash -u
git stash --include-untracked

# Stash including ignored files
git stash -a
git stash --all

# Stash specific files
git stash push -m "partial stash" file1.txt file2.txt
```

### Creating a Branch from Stash

**Definition:** If a stash has been sitting for a while and conflicts with the current branch, you can apply it to a fresh branch using `git stash branch`. This avoids conflicts and allows you to work on the stashed changes in isolation.

```bash
# Create new branch from stash and apply it
git stash branch new-branch-name stash@{0}
```

### Stash Workflow Example

```bash
# You're working on a feature...
echo "new code" >> feature.txt

# Boss asks you to fix urgent bug on main
git stash -m "Feature work in progress"
git checkout main

# Fix the bug...
git commit -am "Fix urgent bug"

# Go back to feature work
git checkout feature-branch
git stash pop

# Continue working...
```

---

## 8. Undoing Changes

### Definition
Git provides multiple mechanisms to undo changes at different stages of the workflow. Understanding the distinction between unstaging (removing from index), discarding (removing from working directory), and resetting (modifying history) is crucial. Choose the appropriate method based on whether changes are local only or shared with others.

### Undo Commands at Different Stages

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    UNDO OPERATIONS REFERENCE GUIDE                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  WORKING DIRECTORY ◄── STAGING AREA ◄── LOCAL REPO ◄── REMOTE REPO        │
│                                                                             │
│  ┌────────────────────────────────────────────────────────────────────┐    │
│  │ Scenario 1: File is modified but NOT staged (red in git status)    │    │
│  └────────────────────────────────────────────────────────────────────┘    │
│                                                                             │
│  Discard changes:  git restore file.txt                                     │
│  Keep changes:     git add file.txt  (stage them)                          │
│                                                                             │
│  ┌────────────────────────────────────────────────────────────────────┐    │
│  │ Scenario 2: File is staged but NOT committed (green in status)     │    │
│  └────────────────────────────────────────────────────────────────────┘    │
│                                                                             │
│  Unstage only:     git restore --staged file.txt                           │
│  (keeps working changes)                                                    │
│                                                                             │
│  Discard all:      git restore --staged file.txt && git restore file.txt   │
│                                                                             │
│  ┌────────────────────────────────────────────────────────────────────┐    │
│  │ Scenario 3: Committed locally but NOT pushed to remote             │    │
│  └────────────────────────────────────────────────────────────────────┘    │
│                                                                             │
│  Amend last commit:  git commit --amend -m "new message"                   │
│  Undo last commit:   git reset --soft HEAD~1   (keeps changes staged)      │
│  Undo and unstage:   git reset --mixed HEAD~1  (keeps changes, unstaged)   │
│  Undo and discard:   git reset --hard HEAD~1   (DESTRUCTIVE!)              │
│                                                                             │
│  ┌────────────────────────────────────────────────────────────────────┐    │
│  │ Scenario 4: Already pushed to remote (shared history)              │    │
│  └────────────────────────────────────────────────────────────────────┘    │
│                                                                             │
│  Create reversal commit:  git revert HEAD                                  │
│  (safest - doesn't rewrite history)                                         │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Reset Modes Comparison

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      GIT RESET MODES VISUALIZED                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  STARTING STATE (before reset):                                            │
│                                                                             │
│  Working Dir:     file.txt contains "Line 1\nLine 2\nLine 3"                │
│  Staging Area:    file.txt staged (green)                                  │
│  Commit History:  HEAD ──► A ──► B (current)                              │
│  (B is most recent commit)                                                  │
│                                                                             │
│  Execute: git reset HEAD~1  (remove last commit)                           │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  1. SOFT RESET (--soft)                                                     │
│  ══════════════════════                                                     │
│                                                                             │
│  Before:  [Working]◄────[Staging: B's changes]◄────[HEAD ──► B]            │
│                                                                             │
│  Command: git reset --soft HEAD~1                                          │
│                                                                             │
│  After:   [Working]◄────[Staging: B's changes]◄────[HEAD ──► A]            │
│                          ▲                                                  │
│                          │                                                  │
│                     Changes preserved in staging!                          │
│                                                                             │
│  Result: Commit B removed from history, but changes remain staged.         │
│          Ready to re-commit with new message.                              │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  2. MIXED RESET (--mixed, default)                                          │
│  ═══════════════════════════════════                                        │
│                                                                             │
│  Before:  [Working]◄────[Staging: B's changes]◄────[HEAD ──► B]            │
│                                                                             │
│  Command: git reset --mixed HEAD~1  (or just git reset HEAD~1)             │
│                                                                             │
│  After:   [Working: B's changes]◄────[Staging: empty]◄────[HEAD ──► A]     │
│                  ▲                                                          │
│                  │                                                          │
│             Changes preserved but unstaged!                                │
│                                                                             │
│  Result: Commit B removed, changes remain in working directory but         │
│          unstaged (red in git status).                                     │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  3. HARD RESET (--hard) ⚠️ DANGEROUS!                                       │
│  ═══════════════════════════════════                                        │
│                                                                             │
│  Before:  [Working]◄────[Staging: B's changes]◄────[HEAD ──► B]            │
│                                                                             │
│  Command: git reset --hard HEAD~1                                          │
│                                                                             │
│  After:   [Working: empty]◄────[Staging: empty]◄────[HEAD ──► A]           │
│                                                                             │
│  Result: Commit B AND all changes COMPLETELY DELETED!                      │
│                                                                             │
│  ⚠️  WARNING: This destroys work permanently! Use with extreme caution!     │
│                                                                             │
│  Recovery (if within reflog window):                                        │
│  git reflog  # Find commit B's hash                                         │
│  git reset --hard <commit-B-hash>                                          │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Visual Summary Table

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     WHEN TO USE EACH COMMAND                                │
├────────────────────────┬────────────────────────────────────────────────────┤
│ Command                │ Use Case                                           │
├────────────────────────┼────────────────────────────────────────────────────┤
│ git restore file       │ Discard unstaged changes in a file                 │
│ git restore --staged   │ Unstage a file (keep working changes)              │
│ git commit --amend     │ Fix last commit message or add files               │
│ git reset --soft       │ Undo commit, keep changes staged                   │
│ git reset --mixed      │ Undo commit, unstage changes (default)             │
│ git reset --hard       │ Undo commit, delete all changes (DESTRUCTIVE)      │
│ git revert             │ Undo a commit by creating a new reversal commit    │
│ git reflog             │ Recover lost commits or undo bad resets            │
└────────────────────────┴────────────────────────────────────────────────────┘

Decision Flow:
              ┌─────────────────────────────────────┐
              │  Need to undo something?            │
              └──────────────┬──────────────────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
        ┌─────────┐   ┌──────────┐   ┌───────────┐
        │ Unstage │   │ Discard  │   │  Modify   │
        │ changes │   │ changes  │   │  History  │
        └────┬────┘   └────┬─────┘   └─────┬─────┘
             │             │               │
             ▼             ▼               ▼
      ┌────────────┐ ┌──────────┐ ┌──────────────┐
      │git restore │ │git restore│ │Already       │
      │--staged    │ │file      │ │pushed?        │
      └────────────┘ └──────────┘ └──────┬───────┘
                                         │
                              ┌──────────┴──────────┐
                              ▼                     ▼
                        ┌──────────┐           ┌──────────┐
                        │   YES    │           │    NO    │
                        └────┬─────┘           └────┬─────┘
                             │                      │
                             ▼                      ▼
                      ┌────────────┐        ┌────────────┐
                      │git revert  │        │git reset   │
                      │(safe)      │        │--soft/--hard│
                      └────────────┘        └────────────┘
```

```bash
# Unstage a file (keep changes in working directory)
git restore --staged filename.txt

# Older syntax
git reset HEAD filename.txt

# Unstage all files
git restore --staged .
```

### Discarding Working Changes

**Definition:** Discarding changes reverts files in your working directory to their last committed state. This is destructive and cannot be undone. Use `git restore <file>` (modern) or `git checkout -- <file>` (legacy) to discard changes.

```bash
# Discard changes in a file (⚠️ destructive)
git restore filename.txt

# Older syntax
git checkout -- filename.txt

# Discard all changes in working directory ⚠️
git restore .
```

### Reset Command (modifies history)

**Definition:** `git reset` moves the HEAD pointer to a specific commit. Depending on the mode (`--soft`, `--mixed`, `--hard`), it can also modify the Staging Index and Working Directory. It is essentially a "time travel" command that can rewrite local history.

```bash
# Soft reset - undo commit, keep staged
git reset --soft HEAD~1

# Mixed reset (default) - undo commit, keep unstaged
git reset --mixed HEAD~1
git reset HEAD~1

# Hard reset - undo commit and discard all changes ⚠️
git reset --hard HEAD~1
```

**Reset Comparison:**

```
Before: Working → Staging → Commit A → Commit B

Soft reset (--soft HEAD~1):
Working → Staging → Commit A
(changes from B are staged)

Mixed reset (--mixed HEAD~1):
Working → Staging → Commit A
(changes from B are unstaged)

Hard reset (--hard HEAD~1):
(changes from B are gone!)
```

### Revert (safe for shared history)

**Definition:** `git revert` creates a *new* commit that undoes the changes introduced by a specific previous commit. Unlike `reset`, it does not rewrite history, making it safe for undoing mistakes in shared/public branches.

```bash
# Create new commit that undoes a previous commit
git revert commit-hash

# Revert without creating commit
git revert --no-commit commit-hash

# Revert multiple commits
git revert commit-hash1..commit-hash2

# Revert a merge commit (specify parent)
git revert -m 1 merge-commit-hash
```

### Reflog (safety net)

**Definition:** The `git reflog` records updates to the tip of branches and other references (HEAD). It allows you to recover "lost" commits (e.g., after a hard reset or deleted branch) that are no longer referenced by any branch but still exist in the local object database.

```bash
# View all Git operations (including lost commits)
git reflog

# Output:
# abc1234 HEAD@{0}: commit: Add feature
# def5678 HEAD@{1}: checkout: moving from main to feature
# ghi9012 HEAD@{2}: commit: Fix bug

# Recover a lost commit
git reset --hard HEAD@{2}
git reset --hard abc1234
```

### Cleaning Untracked Files

**Definition:** `git clean` removes untracked files from the working directory. This is useful for removing build artifacts or temporary files that aren't ignored. It is essentially a "delete" command for untracked files.

```bash
# Show what would be deleted (dry run)
git clean -n
git clean --dry-run

# Delete untracked files ⚠️
git clean -f

# Delete untracked files and directories ⚠️
git clean -fd

# Delete ignored files too ⚠️
git clean -fdx
```

### Choosing the Right Tool

| Situation | Command | History Modified? |
|-----------|---------|-------------------|
| Unstage a file | `git restore --staged` | No |
| Discard working changes | `git restore` | No |
| Amend last commit | `git commit --amend` | Yes |
| Undo local commits | `git reset` | Yes |
| Undo shared commits | `git revert` | No (adds new commit) |
| Recover lost commits | `git reflog` | No |

---

## 9. Remote Repositories

### Definition
Remote repositories are versions of your project hosted on servers (GitHub, GitLab, Bitbucket) or internal networks. They enable collaboration by acting as a central hub where developers push their local commits and pull others' changes. Each remote is a reference (stored in `.git/config`) pointing to a URL, allowing synchronization between distributed local repositories.

### Remote Repository Sync Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    REMOTE REPOSITORY SYNC WORKFLOW                          │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│                              REMOTE SERVER                                  │
│                         (GitHub/GitLab/etc.)                               │
│                         ┌─────────────────────┐                            │
│                         │  origin/main        │                            │
│                         │  origin/feature-x   │                            │
│                         │  origin/feature-y   │                            │
│                         └─────────────────────┘                            │
│                                  ▲                                          │
│                                  │                                          │
│                    ┌─────────────┴─────────────┐                           │
│                    │                             │                           │
│          ┌─────────┴──────────┐      ┌──────────┴──────────┐               │
│          │                    │      │                     │               │
│          │     FETCH          │      │      PUSH           │               │
│          │  (download only)   │      │   (upload commits)  │               │
│          │                    │      │                     │               │
│          └─────────┬──────────┘      └──────────┬──────────┘               │
│                    │                             │                           │
│          ┌─────────┴──────────┐      ┌──────────┴──────────┐               │
│          │  origin/main       │      │  origin/main        │               │
│          │  (remote tracking) │      │  (updated)          │               │
│          └─────────┬──────────┘      └─────────────────────┘               │
│                    │                                                        │
│          ┌─────────┴──────────┐                                            │
│          │   git merge        │                                            │
│          │   or git rebase    │                                            │
│          └─────────┬──────────┘                                            │
│                    │                                                        │
│                    ▼                                                        │
│          ┌────────────────────┐                                            │
│          │    main (local)    │                                            │
│          │  ┌──────────────┐  │                                            │
│          │  │ Working Dir  │  │                                            │
│          │  │ Staging Area │  │                                            │
│          │  │   Commits    │  │                                            │
│          │  └──────────────┘  │                                            │
│          └────────────────────┘                                            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Fetch vs Pull vs Push

**Definition:** `git push` uploads your local commits to a remote repository. `git fetch` downloads new commits from the remote but does not merge them. `git pull` is a combination command that performs a `fetch` followed immediately by a `merge` (or rebase if configured), updating your current branch.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    FETCH / PULL / PUSH COMPARISON                           │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  FETCH - Download without merging                                           │
│  ════════════════════════════════════                                       │
│                                                                             │
│  Remote:  A───B───C───D                                                     │
│                    ▲                                                        │
│                origin/main                                                  │
│                                                                             │
│  Local:   A───B───C                                                         │
│                    ▲                                                        │
│                   main                                                      │
│                                                                             │
│  Command: git fetch origin                                                  │
│                                                                             │
│  Result:  A───B───C───D  (origin/main updated, main unchanged)             │
│                    │                                                        │
│                   main                                                      │
│                                                                             │
│  Use when: You want to see remote changes before merging                   │
│  View with: git log HEAD..origin/main --oneline                            │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  PULL = FETCH + MERGE                                                       │
│  ═══════════════════════════════════                                        │
│                                                                             │
│  Remote:  A───B───C───D                                                     │
│                                                                             │
│  Local:   A───B───C                                                         │
│                                                                             │
│  Command: git pull origin main                                              │
│                                                                             │
│  Result:  A───B───C───D  (same as: git fetch && git merge origin/main)     │
│                       │                                                     │
│                      main                                                   │
│                                                                             │
│  OR with rebase:                                                            │
│  Command: git pull --rebase origin main                                     │
│                                                                             │
│  Result:  A───B───C───D───E'  (your commits replayed on top of D)          │
│                                                                             │
│  Use when: You want to incorporate remote changes immediately               │
│                                                                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  PUSH - Upload local commits                                                │
│  ═══════════════════════════════════                                        │
│                                                                             │
│  Local:   A───B───C───D───E                                                 │
│                            ▲                                                │
│                           main                                              │
│                                                                             │
│  Remote:  A───B───C                                                         │
│                    ▲                                                        │
│                origin/main                                                  │
│                                                                             │
│  Command: git push origin main                                              │
│                                                                             │
│  Result:  A───B───C───D───E                                                 │
│                            │                                                │
│                     ┌──────┴──────┐                                         │
│                     ▼             ▼                                         │
│                   main      origin/main                                     │
│                                                                             │
│  Use when: Your local commits are ready to share                           │
│  ⚠️  Will fail if remote has diverged (requires pull first)                 │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

```bash
# List configured remotes
git remote -v

# Add a remote
git remote add origin https://github.com/user/repo.git

# Add another remote
git remote add upstream https://github.com/original/repo.git

# Rename a remote
git remote rename origin destination

# Remove a remote
git remote remove origin

# Change remote URL
git remote set-url origin https://github.com/user/new-repo.git

# Show remote details
git remote show origin
```

### Pushing Changes

**Definition:** `git push` sends your committed changes to a remote repository (like GitHub). It updates the remote references (branches/tags) to match your local ones. The first push of a new branch usually requires setting an upstream tracking reference (`-u`).

```bash
# Push current branch to origin
git push origin branch-name

# Push and set upstream (track the remote branch)
git push -u origin branch-name
git push --set-upstream origin branch-name

# Push all branches
git push --all origin

# Force push ⚠️ (use with caution)
git push --force
git push -f

# Safer force push (fails if remote has new commits)
git push --force-with-lease

# Delete remote branch
git push origin --delete branch-name
```

### Pulling Changes

**Definition:** `git pull` updates your current local working branch with all new commits from the corresponding remote branch. It is the standard way to "sync up" with your team's work. Since it involves a merge, it can result in merge conflicts.

```bash
# Fetch and merge changes from remote
git pull

# Equivalent to:
git fetch
git merge origin/branch-name

# Pull with rebase instead of merge
git pull --rebase

# Pull specific branch
git pull origin branch-name
```

### Fetching Changes

**Definition:** `git fetch` downloads objects and refs from another repository. It updates your *remote-tracking branches* (e.g., `origin/main`) but leaves your local work untouched. This allows you to review what others have done before deciding to integrate (merge/rebase) their changes.

```bash
# Download changes without merging
git fetch

# Fetch from specific remote
git fetch origin

# Fetch all remotes
git fetch --all

# Prune deleted remote branches
git fetch --prune
git fetch -p

# View fetched changes without merging
git log HEAD..origin/main --oneline
```

### Cloning Repositories

**Definition:** `git clone` copies an entire existing repository (including project files, history, and branches) from a remote server to your local machine. It automatically sets up a remote connection called `origin` pointing back to the cloned URL.

```bash
# Clone a repository
git clone https://github.com/user/repo.git

# Clone with custom directory name
git clone https://github.com/user/repo.git my-folder

# Clone only the latest commit (shallow clone)
git clone --depth 1 https://github.com/user/repo.git

# Clone a specific branch
git clone -b branch-name https://github.com/user/repo.git

# Clone with submodules
git clone --recurse-submodules https://github.com/user/repo.git
```

### SSH vs HTTPS

**Definition:** **HTTPS** uses your GitHub username/password (or Personal Access Token) and is easier to set up but requires authentication more often (unless cached). **SSH** uses public/private key pairs for authentication without passwords, offering a more secure and convenient workflow for frequent contributors.

**HTTPS:**
```bash
# URL format
https://github.com/username/repository.git

# Pros: Simple, works everywhere
# Cons: Must enter credentials or use credential helper
```

**SSH:**
```bash
# URL format
git@github.com:username/repository.git

# Setup (one-time)
ssh-keygen -t ed25519 -C "your@email.com"
cat ~/.ssh/id_ed25519.pub
# Add key to GitHub: Settings → SSH and GPG keys

# Test connection
ssh -T git@github.com

# Pros: No password prompts, more secure
# Cons: Requires initial setup
```

### Tracking Branches

**Definition:** A tracking branch (or upstream branch) is a local branch that is legally linked to a remote branch. When you `push` or `pull` without arguments, Git uses this link to know which remote branch to interact with.

```bash
# Set upstream for current branch
git branch --set-upstream-to=origin/main main

# Check which branch you're tracking
git branch -vv

# Track a remote branch
git checkout --track origin/feature-branch

# Short form (automatically tracks)
git checkout feature-branch
```

---

## 10. GitHub Collaboration

### Definition
GitHub extends Git's distributed model with web-based collaboration tools. Forking creates a personal copy of a repository, pull requests (PRs) propose changes for review, and code reviews enable quality control through peer examination. These features enable open-source contribution workflows and team collaboration with protected branches, automated checks, and structured approval processes.

### GitHub Pull Request Workflow

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                    GITHUB PULL REQUEST WORKFLOW                             │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  SCENARIO: Contributing to an open-source project                           │
│                                                                             │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ 1. FORK (on GitHub web interface)                                   │   │
│  │                                                                     │   │
│  │   Original Repo          Your Fork                                  │   │
│  │   ┌───────────┐         ┌───────────┐                              │   │
│  │   │facebook/  │         │yourname/  │                              │   │
│  │   │react      │  Fork   │react      │                              │   │
│  │   │(read-only)│────────►│(read/write)│                              │   │
│  │   └───────────┘         └───────────┘                              │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                              │                                              │
│                              ▼                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ 2. CLONE your fork locally                                          │   │
│  │                                                                     │   │
│  │   $ git clone https://github.com/yourname/react.git                │   │
│  │   $ cd react                                                        │   │
│  │   $ git remote add upstream https://github.com/facebook/react.git  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                              │                                              │
│                              ▼                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ 3. CREATE FEATURE BRANCH                                            │   │
│  │                                                                     │   │
│  │   $ git checkout -b fix-typo-in-docs                                │   │
│  │   # Make your changes                                               │   │
│  │   $ git commit -am "Fix typo in installation docs"                  │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                              │                                              │
│                              ▼                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ 4. PUSH to your fork                                                │   │
│  │                                                                     │   │
│  │   $ git push -u origin fix-typo-in-docs                             │   │
│  │                                                                     │   │
│  │   Your Fork:                                                        │   │
│  │   main: A───B───C                                                   │   │
│  │                  \                                                  │   │
│  │   fix-typo:       D───E  ◄── pushed!                               │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                              │                                              │
│                              ▼                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ 5. CREATE PULL REQUEST (on GitHub)                                  │   │
│  │                                                                     │   │
│  │   GitHub shows: "Compare & pull request" button                     │   │
│  │                                                                     │   │
│  │   Base: facebook/react main  ◄── compare ──►  head: yourname/fix   │   │
│  │                                                                     │   │
│  │   [Create Pull Request]                                             │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                              │                                              │
│                              ▼                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ 6. CODE REVIEW PROCESS                                              │   │
│  │                                                                     │   │
│  │   Reviewers:                                                        │   │
│  │   ┌─────────────┐  ┌─────────────┐  ┌─────────────┐                │   │
│  │   │  Reviewer 1 │  │  Reviewer 2 │  │  Reviewer 3 │                │   │
│  │   │   ✅ Approve │  │   💬 Comment│  │   ❌ Request │                │   │
│  │   │             │  │             │  │    Changes  │                │   │
│  │   └─────────────┘  └─────────────┘  └─────────────┘                │   │
│  │          │                │                │                        │   │
│  │          └────────────────┼────────────────┘                        │   │
│  │                           ▼                                         │   │
│  │                    Author makes changes                             │   │
│  │                    $ git commit --amend                             │   │
│  │                    $ git push --force-with-lease                    │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                              │                                              │
│                              ▼                                              │
│  ┌─────────────────────────────────────────────────────────────────────┐   │
│  │ 7. MERGE PULL REQUEST                                               │   │
│  │                                                                     │   │
│  │   Options:                                                          │   │
│  │   ┌────────────────┐ ┌────────────────┐ ┌────────────────┐         │   │
│  │   │ Create merge   │ │ Squash & merge │ │ Rebase & merge │         │   │
│  │   │ commit         │ │ (1 commit)     │ │ (linear)       │         │   │
│  │   └────────────────┘ └────────────────┘ └────────────────┘         │   │
│  │                                                                     │   │
│  │   After merge:                                                      │   │
│  │   Original Repo main: A───B───C───F───G───M (your changes!)        │   │
│  │                              \        /                             │   │
│  │                               D───E──┘                              │   │
│  │                                                                     │   │
│  │   [Delete branch] [Revert]                                          │   │
│  └─────────────────────────────────────────────────────────────────────┘   │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Forking

**Definition:** A **Fork** is a copy of a repository that sits in your own GitHub account. It allows you to freely change a project without affecting the original. Forks are the primary way to contribute to open-source projects where you don't have direct write access to the main repository.

```bash
# Fork a repository on GitHub (web interface)
# 1. Go to repository page
# 2. Click "Fork" button
# 3. Clone your fork locally

git clone https://github.com/YOUR-USERNAME/repo.git
cd repo

# Add original repository as upstream
git remote add upstream https://github.com/ORIGINAL/repo.git

# Sync your fork
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

### Pull Requests (PRs)

**Definition:** A **Pull Request** defines a request to merge changes from your branch (or fork) into the base branch of the original repository. It allows maintainers to review, discuss, and request changes to your code before it becomes part of the project proper.

**Creating a PR:**
1. Push your branch to your fork/origin
2. Go to repository on GitHub
3. Click "Compare & pull request"
4. Add title and description
5. Select reviewers
6. Click "Create pull request"

```bash
# Push your feature branch
git push -u origin feature-branch

# GitHub will show a URL to create PR
# Or create PR via CLI (GitHub CLI)
gh pr create
```

**PR Description Template:**
```markdown
## Summary
Brief description of changes

## Changes
- Added user authentication
- Fixed login redirect bug
- Updated documentation

## Testing
- [ ] Unit tests pass
- [ ] Manual testing completed
- [ ] Edge cases handled

## Related Issues
Fixes #123
Closes #456
Related to #789
```

### Code Reviews

**Definition:** Code review is the process where other developers examine proposed code changes in a Pull Request. They check for bugs, design issues, readability, and adherence to style guides. GitHub provides a UI to comment on specific lines of code and "Approve" or "Request Changes".

**As a Reviewer:**
- Check the "Files changed" tab
- Click on a line to add a comment
- Use "Add suggestion" to propose changes
- Submit review: Comment / Approve / Request changes

**As an Author:**
- Address feedback with new commits
- Reply to comments
- Re-request review when ready
- Squash commits if requested

### Issues

**Definition:** GitHub Issues track ideas, feedback, tasks, or bugs. They act as a project management tool integrated directly with the repository. Issues can be assigned to users, labeled, and linked to Pull Requests (e.g., closing an issue when a PR is merged).

```markdown
Creating a Good Issue:

Title: Clear and concise description

Body:
## Description
What is the issue?

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. See error

## Expected Behavior
What should happen?

## Actual Behavior
What actually happens?

## Screenshots
If applicable

## Environment
- OS: [e.g., macOS 14]
- Browser: [e.g., Chrome 120]
- Version: [e.g., 1.2.3]
```

**Closing Issues with Commits/PRs:**
```bash
# Keywords that close issues:
# Fixes, Closes, Resolves, Fixed, Close, Resolve

git commit -m "Fixes #123 - Add authentication"
git commit -m "Closes #456, resolves #789"
```

### Branch Protection Rules

**Definition:** Branch protection rules allow repository admins to enforce workflows on critical branches (like `main`). Rules can require passing tests (CI), a minimum number of PR approvals, or prevent force pushes, ensuring the stability of the production codebase.

Configure in GitHub: Settings → Branches → Add rule

**Common Protections:**
- Require pull request reviews before merging
- Require status checks to pass
- Require branches to be up to date
- Include administrators
- Restrict pushes that create files larger than 100MB

---

## 11. GitHub Features

### Definition
GitHub provides platform-specific features that enhance the Git workflow: READMEs for project documentation, GitHub Pages for static site hosting, Actions for CI/CD automation, Releases for version management, and project management tools like Issues, Projects, and Wikis. These features transform GitHub from a simple hosting service into a complete DevOps platform.

### README.md

**Definition:** The `README.md` is the front page of your repository. It is a Markdown file displayed automatically on GitHub that should explain what the project is, how to install it, how to use it, and how to contribute. A good README is essential for any public project.

```markdown
# Project Name

> Short project description

## Features
- Feature 1
- Feature 2
- Feature 3

## Installation

```bash
git clone https://github.com/user/repo.git
cd repo
npm install
```

## Usage

```javascript
import { myFunction } from 'my-library';

myFunction();
```

## API Documentation
See [API.md](API.md)

## Contributing
See [CONTRIBUTING.md](CONTRIBUTING.md)

## License
[MIT](LICENSE)
```

### GitHub Pages

**Definition:** GitHub Pages is a static site hosting service that takes HTML, CSS, and JavaScript files directly from a repository and publishes a website. It is free and ideal for hosting documentation, portfolios, or project demos.

```bash
# Enable in repository settings
# Settings → Pages → Source → Select branch

# Deploy from branch:
# - main branch (root or /docs folder)
# - gh-pages branch

# Access site at:
# https://username.github.io/repository-name/
```

### GitHub Actions (Basics)

**Definition:** GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. You define workflows in YAML files (e.g., "run tests on every push") that execute on GitHub's servers.

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Setup Node.js
      uses: actions/setup-node@v3
      with:
        node-version: '18'
    
    - name: Install dependencies
      run: npm ci
    
    - name: Run tests
      run: npm test
    
    - name: Build
      run: npm run build
```

**Common Workflows:**
- Continuous Integration (run tests on PR)
- Continuous Deployment (deploy on merge)
- Automated releases (create release on tag)
- Dependency updates (Dependabot)

### Releases

**Definition:** GitHub Releases bundle project history (tags) into downloadable artifacts (like binaries or source code zips). They allow you to version your software (v1.0, v2.0) and provide release notes describing what changed in that version.

```bash
# Create a tag locally
git tag -a v1.0.0 -m "Release version 1.0.0"

# Push tag to remote
git push origin v1.0.0
git push origin --tags

# Delete a tag
git tag -d v1.0.0
git push origin --delete v1.0.0
```

**Semantic Versioning:**
- `MAJOR.MINOR.PATCH`
- `v1.0.0` - Initial release
- `v1.1.0` - New features, backward compatible
- `v1.1.1` - Bug fixes
- `v2.0.0` - Breaking changes

---

## 12. Best Practices

### Definition
Git best practices are conventions and workflows that ensure clean history, effective collaboration, and maintainable repositories. These include commit message standards, branch management strategies, and collaboration patterns that scale from solo development to enterprise teams.

### Commit Message Guidelines

```bash
# Good commit messages
git commit -m "Add user authentication"
git commit -m "Fix login redirect bug"
git commit -m "Update README with API docs"
git commit -m "Refactor database connection"

# Bad commit messages
git commit -m "fix"                    # Too vague
git commit -m "updated stuff"          # Not descriptive
git commit -m "Fixed bug"              # Past tense (use imperative)
git commit -m "asdf"                   # Meaningless
```

**Structure:**
```
<type>: <subject>

<body>

<footer>
```

**Types:**
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation
- `style:` - Formatting
- `refactor:` - Code restructuring
- `test:` - Tests
- `chore:` - Maintenance

### General Best Practices

1. **Commit Often**
   - Small, focused commits
   - Easier to review and revert
   - Better history

2. **Use Feature Branches**
   ```bash
   git checkout -b feature/login-page
   # Work on feature
   git push -u origin feature/login-page
   # Create PR
   ```

3. **Keep Main Stable**
   - Only merge tested code
   - Use CI/CD to verify
   - Never force push to main

4. **Pull Before Push**
   ```bash
   git pull origin main
   # Resolve any conflicts
   git push origin feature-branch
   ```

5. **Write Meaningful Commit Messages**
   - Explain "why" not just "what"
   - Reference issues when applicable

6. **Review Code Before Merging**
   - Use pull requests
   - Require approvals
   - Run automated tests

### Git Flow vs GitHub Flow

**Git Flow (Complex Projects with Releases):**
```
┌─────────────────────────────────────────────────────────────────────────────┐
│                         GIT FLOW WORKFLOW                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  Designed for: Projects with scheduled releases, multiple versions          │
│                                                                             │
│  Branch Structure:                                                          │
│  ════════════════════════════════════════════════                           │
│                                                                             │
│  main ─────────────────────────────────────────────────────────────────►    │
│  (production)         v1.0         v1.1         v2.0                        │
│                                                                             │
│   \                                                                         │
│    \  release/v1.0 ─────────────┐  (release prep, bug fixes only)          │
│     \           \               │                                           │
│      \           merge ─────────┤                                           │
│       \                         │                                           │
│        develop ─────────────────┼──────────────────────────────────────►    │
│         (integration)           │     merge                                 │
│          │ \         \          │     /                                     │
│          │  feature/  feature/  │    /                                      │
│          │  login      payment  │   /                                       │
│          │     │          │     │  /                                        │
│          │     merge      merge─┘ /                                         │
│          │                        │                                         │
│          hotfix/                  │                                         │
│          security ────────────────┘  (emergency fixes to main)              │
│                                                                             │
│  Branch Types:                                                              │
│  ┌──────────────┬──────────────────────────────────────────────────────┐   │
│  │ main         │ Production releases only, tagged with versions      │   │
│  │ develop      │ Integration branch for features, always deployable  │   │
│  │ feature/*    │ New features branch from develop, merge back        │   │
│  │ release/*    │ Prepare release, bug fixes, branch from develop     │   │
│  │ hotfix/*     │ Emergency fixes, branch from main, merge to both    │   │
│  └──────────────┴──────────────────────────────────────────────────────┘   │
│                                                                             │
│  Workflow:                                                                  │
│  1. Create feature branch from develop                                      │
│  2. Develop and test feature                                                │
│  3. Merge feature back to develop via PR                                    │
│  4. When ready to release, create release branch                            │
│  5. Test and fix bugs on release branch                                     │
│  6. Merge release to main AND develop                                       │
│  7. Tag main with version number                                            │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**GitHub Flow (Simple, Continuous Deployment):**
```
┌─────────────────────────────────────────────────────────────────────────────┐
│                      GITHUB FLOW WORKFLOW                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│                                                                             │
│  Designed for: Web applications, continuous deployment, fast iteration      │
│                                                                             │
│  Branch Structure:                                                          │
│  ════════════════════════════════════════════════                           │
│                                                                             │
│  main ─────────────────────────────────────────────────────────────────►    │
│  (deployable)                                                               │
│                                                                             │
│   │                                                                         │
│   │  feature/user-auth ─────┐                                               │
│   │  (branch from main)     │                                               │
│   │       │                 │                                               │
│   │       │ commit          │                                               │
│   │       │ commit          │                                               │
│   │       │                 │                                               │
│   │       ▼                 │                                               │
│   │   Pull Request          │                                               │
│   │   (code review)         │                                               │
│   │       │                 │                                               │
│   │       │ approve         │                                               │
│   │       │ merge           │                                               │
│   │       ▼                 │                                               │
│   └───► main ───────────────┘  (auto-deploy)                                │
│                                                                             │
│   │                                                                         │
│   │  feature/dashboard ─────┐                                               │
│   │       │                 │                                               │
│   │       │ commit          │                                               │
│   │       ▼                 │                                               │
│   │   Pull Request          │                                               │
│   │       │                 │                                               │
│   │       │ approve         │                                               │
│   │       │ merge           │                                               │
│   │       ▼                 │                                               │
│   └───► main ───────────────┘  (auto-deploy)                                │
│                                                                             │
│  Rules:                                                                     │
│  ┌────────────────────────────────────────────────────────────────────┐    │
│  │ 1. main is always deployable                                       │    │
│  │ 2. Create feature branches from main                               │    │
│  │ 3. Use descriptive branch names                                    │    │
│  │ 4. Make small, focused pull requests                               │    │
│  │ 5. Require code review before merge                                │    │
│  │ 6. Run CI checks on every PR                                       │    │
│  │ 7. Deploy immediately after merge                                  │    │
│  │ 8. Monitor production after deployment                             │    │
│  └────────────────────────────────────────────────────────────────────┘    │
│                                                                             │
│  Workflow:                                                                  │
│  1. Pull latest main                                                        │
│  2. Create feature branch                                                   │
│  3. Make commits, push regularly                                            │
│  4. Open Pull Request when ready                                            │
│  5. Discuss and review code                                                 │
│  6. Deploy to staging for testing                                           │
│  7. Merge to main after approval                                            │
│  8. Deploy to production automatically                                      │
│                                                                             │
└─────────────────────────────────────────────────────────────────────────────┘
```

**Comparison Summary:**

```
┌──────────────────────┬──────────────────────┬──────────────────────┐
│ Feature              │ Git Flow             │ GitHub Flow          │
├──────────────────────┼──────────────────────┼──────────────────────┤
│ Branch Types         │ 5 (main, develop,    │ 2 (main, feature)    │
│                      │ feature, release,    │                      │
│                      │ hotfix)              │                      │
├──────────────────────┼──────────────────────┼──────────────────────┤
│ Release Cycle        │ Scheduled releases   │ Continuous deployment│
├──────────────────────┼──────────────────────┼──────────────────────┤
│ main Branch          │ Production only      │ Always deployable    │
├──────────────────────┼──────────────────────┼──────────────────────┤
│ Complexity           │ Higher               │ Lower                │
├──────────────────────┼──────────────────────┼──────────────────────┤
│ Best For             │ Desktop apps,        │ Web apps, SaaS,      │
│                      │ versioned software   │ microservices        │
├──────────────────────┼──────────────────────┼──────────────────────┤
│ Team Size            │ Large teams          │ Small to medium      │
├──────────────────────┼──────────────────────┼──────────────────────┤
│ CI/CD                │ Release-based        │ Continuous           │
└──────────────────────┴──────────────────────┴──────────────────────┘

When to Use:
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
• Git Flow:      Complex projects with scheduled releases
• GitHub Flow:   Continuous deployment, web applications  
• Trunk-based:   High-velocity teams, small commits, senior developers

### Additional Tools

```bash
# See who changed a line (blame)
git blame filename.txt

# Find which commit introduced a bug
git bisect start
git bisect bad
git bisect good v1.0
# Git checks out commits, you test and mark good/bad

git bisect reset

# Apply specific commit to current branch
git cherry-pick commit-hash

# View repository statistics
git shortlog -sn
```

---

## Quick Reference

| Task | Command |
|------|---------|
| Initialize repo | `git init` |
| Clone repo | `git clone <url>` |
| Check status | `git status` |
| Stage file | `git add <file>` |
| Stage all | `git add .` |
| Commit | `git commit -m "msg"` |
| Push | `git push` |
| Pull | `git pull` |
| Create branch | `git checkout -b <name>` |
| Switch branch | `git checkout <name>` |
| Merge branch | `git merge <name>` |
| View log | `git log --oneline` |
| View diff | `git diff` |
| Stash | `git stash` |
| Unstash | `git stash pop` |

---

*Documentation created following the roadmap structure. Practice these commands regularly to build muscle memory.*
