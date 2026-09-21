Homelab Architecture

Overview

This homelab is built around a Lenovo ThinkCentre M720q running Proxmox VE.

The goal of the project is to gain hands-on experience with virtualization, Linux administration, networking, storage, self-hosted applications, and infrastructure management.

⸻

Physical Hardware

Lenovo ThinkCentre M720q

* Intel Core i5-8400T
* 64 GB RAM
* Samsung 990 EVO Plus 1 TB NVMe
* WD 2 TB external storage

⸻

Virtualization

Proxmox VE

The ThinkCentre runs Proxmox VE as the primary virtualization platform.

Proxmox currently hosts:

* services01 — Infrastructure VM
* arr01 — Media management LXC
* media01 — Media server VM

⸻

Network

Current Network

* LAN: 192.168.86.0/24
* Gateway: 192.168.86.1
* Proxmox host: 192.168.86.x

Internal IP addresses may change as the network configuration develops.

⸻

services01

services01 is a Debian 13 VM used for infrastructure and management services.

Current Services

* Docker
* Portainer
* Pi-hole

Additional infrastructure services may be added as the homelab develops.

⸻

arr01

arr01 is an unprivileged LXC container dedicated to media management.

Current Services

* Prowlarr
* Sonarr
* Radarr

The container has access to the media storage required by these services.

⸻

media01

media01 is a dedicated Debian 13 VM for media playback and television-style services.

Current Services

* Jellyfin
* ErsatzTV

Jellyfin provides the primary media library interface.

ErsatzTV is used to create scheduled television-style channels using the media library.

⸻

Storage

WD 2 TB External Drive

The WD 2 TB drive is currently being used as the primary media storage device.

Current storage includes:

* Movies
* TV
* Music
* Downloads
* Other

The storage architecture is expected to change as the homelab expands.

⸻

Remote Access

Remote access is currently a planned project.

The goal is to securely access the homelab from outside the home network for:

* Homelab administration
* Phone access
* Remote computer access
* Jellyfin
* ErsatzTV

Planned Technology

* WireGuard

⸻

Future Infrastructure

Planned future improvements include:

* TerraMaster NAS
* Dedicated backup storage
* Repurpose the WD 2 TB drive as backup storage
* Improved monitoring
* Infrastructure automation
* Additional Linux and cloud infrastructure projects

⸻

Architecture Summary

The current environment is organized by function:

* pve1 — Proxmox virtualization host
* services01 — Infrastructure services
* arr01 — Media management
* media01 — Media playback and television services
* WD 2 TB — Current media storage

This separation allows individual services to be developed, maintained, and expanded without placing the entire homelab on a single system.