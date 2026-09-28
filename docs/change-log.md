# Homelab Change Log

A chronological record of changes, configuration decisions, problems,
solutions, and lessons learned while building the homelab.


---
2026-09-27 — n8n Monitoring & Proxmox Network Incident Follow-Up
Change

Completed the first version of the homelab monitoring workflow using n8n and documented a recurring Proxmox network failure for future investigation.

Why

The goal of the monitoring system is to detect service failures before they become larger problems and provide notification through Telegram.

A separate concern was identified during recent work: the Proxmox host has experienced more than one network failure in which the ThinkCentre remained powered on but became unreachable. Because n8n runs inside the Proxmox environment, it cannot independently recover the host if Proxmox or its network becomes unavailable.

Actions
Built an n8n monitoring workflow using an existing five-minute schedule trigger.
Added HTTP health checks for:
Caddy
Jellyfin
Sonarr
Radarr
Prowlarr
Proxmox
Added Telegram notifications for failed service checks.
Added Proxmox storage monitoring through the Proxmox API.
Created a dedicated Proxmox API token for n8n monitoring.
Granted the monitoring token the PVEAuditor role.
Added monitoring for both local and local-lvm storage.
Added an 80% storage-utilization warning threshold.
Combined both storage pools into a single warning message rather than generating separate alerts.
Tested the storage-warning path using a temporary 1% threshold.
Restored the production storage-warning threshold to 80%.
Connected the storage monitoring into the existing five-minute monitoring workflow.
Executed the complete workflow manually and verified that the monitoring chain reached the storage check successfully.
Confirmed that the current storage levels remain below the warning threshold.
Current Storage State

At the time of testing:

local-lvm — 3% used, approximately 767 GB available.
local — 7% used, approximately 83 GB available.
Proxmox Network Incident

During recent homelab work, the Proxmox web interface became unreachable while the ThinkCentre remained powered on.

Observed behavior:

Proxmox web access stopped responding.
The local Proxmox console remained accessible.
vmbr0 remained UP and retained the Proxmox IP address.
The physical network interface was not functioning normally.
Attempts to reach the network gateway failed.
A physical reboot of the ThinkCentre restored network connectivity and Proxmox access.
After the reboot, the homelab services became reachable again.

This incident resembles the earlier NIC failure documented during September 2026, where the physical interface experienced a hardware/driver hang and required a physical reset.

What Was Noticed

The repeated behavior suggests that the Proxmox network failure may be related to a recurring hardware, driver, firmware, power-management, or network configuration issue.

However, the root cause has not been established.

The physical reboot restored functionality, but it should be considered a recovery action rather than a corrective fix.

Reproduction / Further Investigation

This issue should be reproduced and investigated during a future maintenance session.

When the next failure occurs, collect evidence before rebooting whenever possible, including:

Proxmox network interface state.
vmbr0 state and configuration.
Gateway connectivity.
ARP behavior.
NIC transmit/receive counters.
Kernel and dmesg output.
Network-driver messages.
Proxmox service status.
Relevant system logs.

Compare the evidence against the previous NIC failure to determine whether the same failure signature is occurring.

Potential areas for corrective investigation include:

NIC hardware.
NIC driver.
Proxmox networking configuration.
ThinkCentre BIOS/firmware.
NIC power-management settings.
Bridge configuration.
Physical network connection.
Other host-level causes.
Future Recovery Architecture

The current n8n monitoring system operates inside the Proxmox environment. Therefore, it cannot independently recover the ThinkCentre if the Proxmox host or its network becomes unavailable.

A future Raspberry Pi 5 watchdog is planned to operate independently of Proxmox.

The intended architecture is:

Raspberry Pi 5
      |
      | external health monitoring
      v
Proxmox / ThinkCentre
      |
      v
services01 / n8n
      |
      v
Homelab services

The Pi should eventually be capable of confirming a genuine Proxmox failure and initiating a controlled recovery action.

The recovery system should not reboot the ThinkCentre after a single failed check. It should use multiple checks, failure confirmation, logging, and a controlled recovery process.

The physical method for allowing the Raspberry Pi to control or signal the ThinkCentre has not yet been determined.

Result

The homelab now has a functioning first-stage monitoring system capable of detecting service availability and Proxmox storage utilization and notifying the user through Telegram.

The recurring Proxmox network failure remains an open investigation and has been intentionally documented for future reproduction, analysis, and corrective action rather than being treated as resolved.

What I Learned
n8n can monitor services through HTTP health checks.
A monitoring workflow can branch on service health and send notifications only when a failure occurs.
Proxmox exposes useful infrastructure information through its API.
API tokens can provide monitoring access without using a password.
Multiple storage pools can be processed into a single monitoring result.
Monitoring from inside the infrastructure has an important limitation: it cannot independently recover the infrastructure hosting the monitoring system.
A true infrastructure watchdog needs to operate outside the environment it is responsible for recovering.
A successful reboot is not necessarily a root-cause fix and should be documented separately from corrective action.
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

```text
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
```

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
