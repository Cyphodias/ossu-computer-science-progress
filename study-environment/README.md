# study environment

This directory documents the computing environment used to support my OSSU Computer Science studies.

The goal is reproducibility: record the classes of hardware, operating systems, software, virtualization technologies, removable-media laboratory and home-lab capabilities that support practical learning.

> **Public-repository rule:** this documentation intentionally contains no private home-network details, IP addresses, hostnames tied to the physical home, credentials, secrets, serial numbers, public IP addresses, VPN details, or other information that could expose the private infrastructure.

## environment overview

```text
                    cs study environment
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
     laptop            desktop           portable lab
   windows 11 pro       ubuntu             ventoy usb
        │                  │                  │
   virtualbox           linux tools      multiple os images
   hyper-v              compilers        kali / ubuntu / ...
   wsl                  debuggers
        │                  │
        └──────────────────┼──────────────────┘
                           │
                      home lab
                           │
                     proxmox ve
                           │
                 vms / containers / services
```

## components

| component | role |
|---|---|
| windows 11 pro laptop | primary mobile study and development workstation |
| ubuntu desktop | dedicated linux development and course workstation |
| ventoy usb | portable operating-system and recovery/practice laboratory |
| virtualbox | desktop virtualization and isolated experiments |
| hyper-v | windows virtualization and systems experiments |
| wsl | linux tooling integrated with windows |
| home server lab | persistent virtualization, services and systems practice |
| proxmox ve | server virtualization platform |

## study integration

| study area | practical environment |
|---|---|
| programming | windows + ubuntu |
| algorithms | python / c / c++ development environments |
| computer architecture | linux + virtual machines |
| operating systems | ubuntu + virtual machines + proxmox |
| networking | linux networking tools + isolated lab environments |
| databases | linux databases in local/virtual environments |
| distributed systems | multiple virtual machines and containers |
| security | kali linux + isolated practice environments |
| software engineering | git, github, editors, testing and build tools |
| machine learning | python scientific/ml environment |
| ai systems | linux + virtualization + gpu/cpu experimentation where available |
| systems administration | linux + proxmox + virtual machines/containers |

## documentation principles

1. Document what is actually installed or configured.
2. Separate **installed**, **configured**, **tested** and **actively used**.
3. Keep credentials and secrets outside the repository.
4. Do not publish private infrastructure details.
5. Prefer configuration explanations and reproducible procedures over screenshots.
6. Record why a tool is used and which course/research activity it supports.
7. Keep server names lowercase, for example `pve-main`.

## sections

- [windows 11 pro laptop](01-laptop-windows/README.md)
- [ventoy portable laboratory](02-ventoy-lab/README.md)
- [ubuntu desktop](03-desktop-ubuntu/README.md)
- [home server laboratory](04-home-server-lab/README.md)
- [environment changelog](CHANGELOG.md)
