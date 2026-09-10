# Kevin's HomeLab

A hands-on homelab project for learning Linux, virtualization, networking,
Docker, storage, automation, and cloud infrastructure.

## Current Hardware

- Lenovo ThinkCentre M720q
- Intel Core i5-8400T
- 64 GB RAM
- Samsung 990 EVO Plus 1 TB NVMe
- WD 2 TB storage drive

## Current Infrastructure

### Proxmox

Proxmox VE is used as the virtualization platform.

Current network:

- Proxmox: 192.168.86.25
- services01: 192.168.86.27
- Gateway: 192.168.86.1

### services01

Debian 13 VM running Docker services.

Current services:

- Docker
- Portainer
- Homarr
- Pi-hole
- Jellyfin

### Storage

The WD 2 TB drive is passed through from Proxmox to services01 and mounted
read-only at:

`/mnt/my-passport/`

Media is organized under:

`/mnt/my-passport/Media`

Current media directories:

- Movies
- TV

## Learning Goals

- Linux administration
- Proxmox virtualization
- Docker and containers
- Networking
- Storage administration
- Infrastructure documentation
- Git and GitHub
- Automation
- CI/CD
- Cloud infrastructure concepts
