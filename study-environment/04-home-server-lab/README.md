# home server laboratory

The home server laboratory provides persistent infrastructure for practical Computer Science study, systems administration and experimentation.

## public documentation boundary

This is a **public repository**. The documentation intentionally avoids private infrastructure information.

Do not publish:

- private IP addresses
- public IP addresses
- physical addresses
- ISP details
- Wi-Fi names or passwords
- VPN configuration or credentials
- DNS secrets
- API tokens
- SSH keys
- serial numbers
- hardware asset identifiers
- firewall rules that expose private topology unnecessarily
- personally identifying information

Server names are written in lowercase, for example `pve-main`.

## platform

The laboratory uses **Proxmox VE hypervisors** to provide a persistent environment for virtual machines and containers.

The current documentation should describe the roles and capabilities of the hosts without exposing their private addressing or physical location.

## host roles

The lab includes multiple Proxmox VE hosts. Each host should have a short public-safe description such as:

- `pve-main` — primary virtualization host
- `pve-chaos` — secondary experimentation/virtualization host

Additional hosts can be documented as they are added, using lowercase names and generic role descriptions.

## workloads

The laboratory supports categories of workloads including:

- Linux virtual machines
- Windows virtual machines
- Linux containers
- DNS infrastructure
- monitoring and observability
- security monitoring
- network-management tools
- media/services workloads
- development environments
- disposable experimentation environments

The exact private service inventory, addressing and access paths should remain outside this public repository unless deliberately sanitized.

## learning applications

### operating systems

Virtual machines and containers provide repeatable environments for practising Linux administration, process management, storage, networking and service deployment.

### networking

The lab provides a controlled environment for learning routing, DNS, network services, monitoring and traffic analysis without exposing the private production topology.

### distributed systems

Multiple VMs and containers can be used to study communication between independent systems, service discovery, failure, replication and distributed application design.

### security

Isolated environments can be used for defensive security practice, logging, monitoring and authorized testing.

### systems administration

The lab provides practical experience with virtualization, backups, updates, service management, monitoring and troubleshooting.

## architecture documentation

Public architecture diagrams should show **logical roles**, not real addresses or sensitive topology.

Example:

```text
                internet
                   │
              gateway/router
                   │
             managed network
                   │
          ┌────────┴────────┐
          │                 │
      pve-main          pve-chaos
          │                 │
      ┌───┴───┐         ┌───┴───┐
      │       │         │       │
     vms   containers   vms   containers
```

## operational documentation

Future public documentation can cover:

- Proxmox installation principles
- VM/CT creation standards
- storage concepts
- backup strategy at a high level
- update procedures
- monitoring architecture
- resource allocation
- lab isolation principles
- experiment lifecycle

Private operational values belong in a separate private repository or local documentation system.
