# Git – Version Control System

## 1. Introduction

Git is a distributed version control system (VCS) that tracks changes made to files over time.

It allows developers to manage source code, collaborate with others, compare file versions, and restore previous changes.

**Main Uses:**
- Track changes in files.
- Manage project versions.
- Collaborate with other developers.
- Compare changes between commits.
- Restore previous versions of files.

## 2. Installation on Kali Linux

```bash
sudo apt update
sudo apt install git -y
```

Check the installed version:

```bash
git --version
```

## 3. Important Git Commands

### Repository Management

| Command | Purpose |
|---|---|
| `git init` | Initialize a new Git repository |
| `git status` | Check repository status |
| `git add filename` | Stage a specific file |
| `git add .` | Stage all changes in the current directory |
| `git commit -m "message"` | Save staged changes as a commit |
| `git clone URL` | Clone an existing repository |

### History & Investigation

| Command | Purpose |
|---|---|
| `git log` | View commit history |
| `git log -p` | View commit history with file changes |
| `git show` | Inspect a particular commit |
| `git diff` | Compare working changes |
| `git rev-list --all` | List commit IDs reachable from references |
| `git log --oneline --all --graph` | Visualize commit history |

### Branch Management

| Command | Purpose |
|---|---|
| `git branch` | List local branches |
| `git branch -a` | List local and remote-tracking branches |
| `git checkout branch-name` | Switch to another branch |
| `git switch branch-name` | Switch branches |
| `git merge branch-name` | Merge a branch into the current branch |

**Note:** `git checkout` can also restore files or switch to a previous commit, depending on the arguments.

## 4. Git in Cybersecurity

Git is useful in several cybersecurity areas.

### A. Digital Forensics

Git history can help investigators:

- Investigate previous file versions.
- Identify deleted or modified content.
- Understand when changes occurred.
- Examine suspicious code modifications.

### B. Secret Hunting

Developers sometimes accidentally commit sensitive information, such as:

- API keys.
- Passwords.
- Database credentials.
- Access tokens.
- Private configuration files.

These secrets may remain in Git history even after being deleted from the latest version.

### C. Security Auditing

Git can help security professionals:

- Investigate suspicious code changes.
- Identify when vulnerabilities were introduced.
- Track modifications to applications.
- Review changes between commits.

## 5. Useful Git Investigation Commands

### View All Commit History

```bash
git log --oneline --all --graph
```

### Inspect a Specific Commit

```bash
git show COMMIT_ID
```

### Compare Changes

```bash
git diff
```

### Search Git History for a Specific String

```bash
git log -S'API_KEY' --all -p
```

Searches commit history for changes involving the specified string.

**Important:** Git history inspection can reveal accidentally committed secrets. If a real credential is exposed, revoke or rotate it immediately. Deleting it from the latest commit alone is not sufficient.

## 6. Learning Resources

- [Official Git Website](https://git-scm.com/)
- [Git Documentation](https://git-scm.com/doc)
- [GitHub](https://github.com/)
- [TryHackMe](https://tryhackme.com/)

---

**Note:** Git is a version control system, not a dedicated security testing tool. However, its history and comparison features are valuable for security investigations and code auditing.
