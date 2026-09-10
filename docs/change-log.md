# Homelab Change Log

A chronological record of changes, configuration decisions, problems,
solutions, and lessons learned while building the homelab.

---

## 2026-09-09 — GitHub Documentation Setup

### Change
Created the initial Git repository for the homelab and connected it to GitHub.

### Why
To begin version-controlling homelab documentation and infrastructure changes.

### Actions
- Created the `~/homelab` Git repository.
- Renamed the default branch to `main`.
- Created the initial `README.md`.
- Configured Git author information.
- Created an SSH key for GitHub authentication.
- Added the SSH key to GitHub.
- Changed the repository remote from HTTPS to SSH.
- Created a `.gitignore` to prevent sensitive and generated files from being tracked.
- Pushed the repository to GitHub.

### Result
The homelab repository is successfully hosted on GitHub and synchronized
using SSH authentication.

### What I Learned
- Git tracks changes to files in a repository.
- GitHub acts as a remote repository.
- SSH keys can authenticate Git operations without using a GitHub password.
- A `.gitignore` prevents specified files from being tracked by Git.
- `git commit` creates a local version-control checkpoint.
- `git push` publishes local commits to the remote repository.
- `git status` shows whether the local repository is synchronized with GitHub.
