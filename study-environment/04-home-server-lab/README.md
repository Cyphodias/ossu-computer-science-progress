# Home Server Laboratory

The home server laboratory provides persistent infrastructure for practical Computer Science study, systems administration and experimentation.

## Public Documentation Boundary

This is a **public repository**. The documentation intentionally avoids private infrastructure information.

Do not publish:

- Private IP addresses
- Public IP addresses
- Physical addresses
- ISP details
- Wi-Fi names or passwords
- VPN configuration or credentials
- DNS secrets
- API tokens
- SSH keys
- Serial numbers
- Hardware asset identifiers
- Firewall rules that expose private topology unnecessarily
- Personally identifying information

Server names are written in lowercase, for example `pve-main`.

## Platform

The laboratory uses **Proxmox VE hypervisors** to provide a persistent environment for virtual machines and containers.

The current documentation should describe the roles and capabilities of the hosts without exposing their private addressing or physical location.

## Host Roles

The lab includes multiple Proxmox VE hosts. Each host should have a short public-safe description such as:

- `pve-main` — Primary virtualization host
- `pve-chaos` — Secondary experimentation/virtualization host

Additional hosts can be documented as they are added, using lowercase names and generic role descriptions.

## Workloads

The laboratory supports categories of workloads including:

- Linux virtual machines
- Windows virtual machines
- Linux containers
- DNS infrastructure
- Monitoring and observability
- Security monitoring
- Network-management tools
- Media/services workloads
- Development environments
- Disposable experimentation environments

The exact private service inventory, addressing and access paths should remain outside this public repository unless deliberately sanitized.

## Learning Applications

### Operating Systems

Virtual machines and containers provide repeatable environments for practising Linux administration, process management, storage, networking and service deployment.

### Networking

The lab provides a controlled environment for learning routing, DNS, network services, monitoring and traffic analysis without exposing the private production topology.

### Distributed Systems

Multiple VMs and containers can be used to study communication between independent systems, service discovery, failure, replication and distributed application design.

### Security

Isolated environments can be used for defensive security practice, logging, monitoring and authorized testing.

### Systems Administration

The lab provides practical experience with virtualization, backups, updates, service management, monitoring and troubleshooting.

## Architecture Documentation

Public architecture diagrams should show **logical roles**, not real addresses or sensitive topology.

Example:

```text
                Internet
                   │
              Gateway/Router
                   │
             Managed Network
                   │
          ┌────────┴────────┐
          │                 │
      pve-main          pve-chaos
          │                 │
      ┌───┴───┐         ┌───┴───┐
      │       │         │       │
     VMs   Containers   VMs   Containers
```

## Operational Documentation

Future public documentation can cover:

- Proxmox installation principles
- VM/CT creation standards
- Storage concepts
- Backup strategy at a high level
- Update procedures
- Monitoring architecture
- Resource allocation
- Lab isolation principles
- Experiment lifecycle

Private operational values belong in a separate private repository or local documentation system.
