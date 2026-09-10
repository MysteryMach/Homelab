# Homelab Architecture

This document describes the current and planned architecture of the homelab.

---

## Physical Hardware

### Lenovo ThinkCentre M720q

The ThinkCentre M720q is the primary homelab server.

Hardware:

- Intel Core i5-8400T
- 64 GB RAM
- Samsung 990 EVO Plus 1 TB NVMe
- WD 2 TB storage drive

The Samsung NVMe is used for Proxmox and virtual machine/service storage.

The WD 2 TB drive is used for media and download storage.

---

## Virtualization

### Proxmox VE

Proxmox VE is installed directly on the ThinkCentre and provides the
virtualization layer for the homelab.

Current management address:

- Proxmox: `192.168.86.25`
- Gateway: `192.168.86.1`

Proxmox currently hosts the `services01` Debian VM.

---

## Current Virtual Machine

### services01

`services01` is a Debian 13 virtual machine running Docker-based services.

Address:

- `192.168.86.27`

Current services:

- Docker
- Portainer
- Homarr
- Pi-hole
- Jellyfin

The VM provides the current application/service layer of the homelab.

---

## Storage Architecture

The WD 2 TB drive is physically connected to the ThinkCentre.

The storage path is:

```text
WD 2 TB Drive
      │
      ▼
   Proxmox
      │
      │ disk passthrough
      ▼
   services01
      │
      ▼
 /dev/sdb
      │
      ▼
 /mnt/my-passport
