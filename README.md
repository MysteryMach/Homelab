Kevin’s HomeLab

A hands-on homelab project for learning Linux, virtualization, networking, storage, self-hosted applications, automation, and cloud infrastructure.

This project is also being used as a practical portfolio to document infrastructure design, troubleshooting, and ongoing learning.

⸻

Current Hardware

* Lenovo ThinkCentre M720q
    * Intel Core i5-8400T
    * 64 GB RAM
    * Samsung 990 EVO Plus 1 TB NVMe
    * WD 2 TB external storage

⸻

Current Infrastructure

Proxmox

Proxmox VE is used as the virtualization platform for the homelab.

Current network:

* Proxmox host: 192.168.86.25
* Gateway: 192.168.86.1

Proxmox currently hosts the following services:

Host	Type	Purpose
services01	VM	Infrastructure services
arr01	LXC	Media management
media01	VM	Media server

⸻

services01

Debian 13 VM used for infrastructure and management services.

Current services include:

* Docker
* Portainer
* Homarr
* Pi-hole

⸻

arr01

Unprivileged LXC container dedicated to media management.

Current services:

* Prowlarr
* Sonarr
* Radarr

The container has access to the homelab media/download storage.

⸻

media01

Debian 13 VM dedicated to media services.

Current services:

* Jellyfin
* ErsatzTV

Jellyfin provides the primary media library interface.

ErsatzTV is being used to create scheduled/live-style television channels from the media library.

⸻

Storage

The current media storage is a WD 2 TB external drive.

Current media organization includes:

* Movies
* TV
* Music
* Downloads
* Other

The storage architecture is expected to change as the homelab expands.

Planned Storage Expansion

Future plans include:

* TerraMaster NAS
* Dedicated backup storage
* Reworking the WD 2 TB drive as a backup/secondary storage device

⸻

Remote Access

Current Goal

Build secure remote access to the homelab so that services can be managed from outside the home network.

Planned access includes:

* Personal phone
* Remote computer
* Jellyfin
* ErsatzTV
* Homelab administration

WireGuard is planned as the VPN solution.

⸻

Current Project Status

Completed

* Proxmox VE deployment
* 64 GB RAM upgrade
* NVMe storage configuration
* WD 2 TB storage integration
* services01 infrastructure VM
* arr01 LXC
* Prowlarr deployment
* Sonarr deployment
* Radarr deployment
* media01 VM
* Jellyfin deployment
* ErsatzTV deployment
* Jellyfin/ErsatzTV media integration

In Progress

* Secure remote access
* WireGuard deployment
* Remote Jellyfin testing
* Remote ErsatzTV testing
* Remote administration from phone/computer

Future

* TerraMaster NAS
* Backup architecture
* Repurpose WD 2 TB drive for backup
* Improve monitoring
* Infrastructure automation
* Expand cloud/DevOps components

⸻

Learning Goals

* Linux administration
* Proxmox virtualization
* LXC containers
* Docker
* Networking
* Storage administration
* Self-hosted applications
* Infrastructure documentation
* Git and GitHub
* Automation
* CI/CD
* Cloud infrastructure concepts
* Troubleshooting

⸻

About

This is an ongoing hands-on homelab project focused on building practical IT infrastructure skills through experimentation, troubleshooting, documentation, and incremental improvements.