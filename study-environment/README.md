# Study Environment

This directory documents the computing environment used to support my OSSU Computer Science studies.

The goal is reproducibility: record the classes of hardware, operating systems, software, virtualization technologies, removable-media laboratory and home-lab capabilities that support practical learning.

> **Public Repository Rule:** This documentation intentionally contains no private home-network details, IP addresses, hostnames tied to the physical home, credentials, secrets, serial numbers, public IP addresses, VPN details, or other information that could expose the private infrastructure.

## Environment Overview

```text
                    CS Study Environment
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
     Laptop            Desktop           Portable Lab
   Windows 11 Pro       Ubuntu             Ventoy USB
        │                  │                  │
   VirtualBox           Linux Tools      Multiple OS Images
   Hyper-V              Compilers        Kali / Ubuntu / ...
   WSL                  Debuggers
        │                  │
        └──────────────────┼──────────────────┘
                           │
                      Home Lab
                           │
                     Proxmox VE
                           │
                 VMs / Containers / Services
```

## Components

| Component | Role |
|---|---|
| Windows 11 Pro laptop | Primary mobile study and development workstation |
| Ubuntu desktop | Dedicated Linux development and course workstation |
| Ventoy USB | Portable operating-system and recovery/practice laboratory |
| VirtualBox | Desktop virtualization and isolated experiments |
| Hyper-V | Windows virtualization and systems experiments |
| WSL | Linux tooling integrated with Windows |
| Home Server Lab | Persistent virtualization, services and systems practice |
| Proxmox VE | Server virtualization platform |

## Study Integration

| Study Area | Practical Environment |
|---|---|
| Programming | Windows + Ubuntu |
| Algorithms | Python / C / C++ development environments |
| Computer Architecture | Linux + virtual machines |
| Operating Systems | Ubuntu + virtual machines + Proxmox |
| Networking | Linux networking tools + isolated lab environments |
| Databases | Linux databases in local/virtual environments |
| Distributed Systems | Multiple virtual machines and containers |
| Security | Kali Linux + isolated practice environments |
| Software Engineering | Git, GitHub, editors, testing and build tools |
| Machine Learning | Python scientific/ML environment |
| AI Systems | Linux + virtualization + GPU/CPU experimentation where available |
| Systems Administration | Linux + Proxmox + virtual machines/containers |

## Documentation Principles

1. Document what is actually installed or configured.
2. Separate **installed**, **configured**, **tested** and **actively used**.
3. Keep credentials and secrets outside the repository.
4. Do not publish private infrastructure details.
5. Prefer configuration explanations and reproducible procedures over screenshots.
6. Record why a tool is used and which course/research activity it supports.
7. Keep server names lowercase, for example `pve-main`.

## Sections

- [Windows 11 Pro Laptop](01-laptop-windows/README.md)
- [Ventoy Portable Laboratory](02-ventoy-lab/README.md)
- [Ubuntu Desktop](03-desktop-ubuntu/README.md)
- [Home Server Laboratory](04-home-server-lab/README.md)
- [Environment Changelog](CHANGELOG.md)
