# Homelab Change Log

A chronological record of changes, configuration decisions, problems,
solutions, and lessons learned while building the homelab.

---
2026-09-21 — Media Infrastructure Expansion

Change

Expanded the homelab media infrastructure by separating media management and media playback services into dedicated systems.

Added

* Created arr01 as an LXC container for media management.
* Deployed Prowlarr.
* Deployed Sonarr.
* Deployed Radarr.
* Created media01 as a dedicated Debian 13 VM.
* Deployed Jellyfin on media01.
* Deployed ErsatzTV on media01.
* Connected the media services to the existing WD 2 TB storage.

Architecture Change

The media environment is now separated from the primary infrastructure services.

'''text
pve1
│
├── services01
│   ├── Docker
│   ├── Portainer
│   ├── Homarr
│   └── Pi-hole
│
├── arr01 (LXC)
│   ├── Prowlarr
│   ├── Sonarr
│   └── Radarr
│
└── media01 (VM)
    ├── Jellyfin
    └── ErsatzTV

Why

Separating the media services from the infrastructure services provides better isolation and makes the homelab easier to expand and maintain.

Result

The homelab now has dedicated infrastructure, media-management, and media-server environments.

Next Objective

Implement secure remote access so the homelab can be managed remotely and Jellyfin/ErsatzTV can be accessed from outside the home network.

Planned areas:

* WireGuard
* Phone access
* Remote computer access
* Jellyfin remote access
* ErsatzTV remote access
* Remote administration


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
