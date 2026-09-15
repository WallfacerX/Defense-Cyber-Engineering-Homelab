# Homelab Hardware Build and Repurposing

## Overview

This homelab was built as a hands-on engineering environment rather than assembled entirely from preconfigured systems or virtual machines.

Part of the project involved physically preparing, upgrading, repurposing, and deploying hardware for different roles within the lab.

The goal was to gain experience across the full system lifecycle:

```text
Hardware
    ↓
Operating System
    ↓
Network
    ↓
Security Controls
    ↓
Monitoring and Validation
```

Working from the hardware layer upward provides a better understanding of how infrastructure actually behaves and how security controls depend on the systems underneath them.

---

# Repurposed Linux Workstation

One of the primary engineering systems in the lab began as an older Apple desktop that was no longer being used as a modern daily workstation.

Rather than discard the hardware, it was repurposed into a dedicated Linux engineering and administration system.

## Hardware Upgrade

The original storage was replaced with a new SSD.

This involved:

- opening and servicing the existing system
- removing the previous storage device
- installing replacement solid-state storage
- preparing the machine for a clean operating system installation
- validating the upgraded hardware after installation

The SSD upgrade improved the usefulness of the older system and gave it a new role within the lab.

---

## Linux Installation

Linux Mint was installed as the workstation operating system.

The machine was then developed into a dedicated administrative and engineering platform for the homelab.

Its role includes activities such as:

- firewall administration
- network configuration
- system hardening
- logging and auditing
- infrastructure documentation
- Linux administration
- security testing support
- lab troubleshooting

Rather than using the workstation as an intentionally vulnerable target, it is being maintained as a hardened administrative system.

This creates a clear separation between trusted engineering infrastructure and systems used for offensive-security experimentation.

---

# Raspberry Pi Builds

Multiple Raspberry Pi systems were also physically assembled and prepared for use within the lab.

The process included the practical work required to turn individual components into usable computing nodes rather than treating the systems as prebuilt appliances.

This included:

- assembling the Raspberry Pi hardware
- preparing storage media
- installing operating systems
- performing initial system configuration
- connecting the systems to the lab network
- validating boot and network connectivity
- preparing the devices for future infrastructure and security roles

The Raspberry Pi systems provide flexible, low-power platforms that can be reused for different projects as the lab expands.

Possible lab roles include infrastructure services, monitoring, automation, isolated services, and other dedicated workloads.

Their final roles can evolve without changing the core network architecture.

---

# Dedicated Security Hardware

The lab also includes dedicated physical network-security infrastructure rather than relying entirely on a consumer router.

A dedicated firewall appliance provides routing and security enforcement between network segments.

A managed Ethernet switch provides VLAN-aware Layer 2 connectivity between systems and the firewall.

Together, these systems allow the lab to implement and test concepts such as:

- network segmentation
- VLAN trunking
- firewall policy
- management-plane isolation
- default-deny communication
- administrative trust boundaries

This allows security controls to be tested on real network hardware instead of only being simulated inside a hypervisor.

---

# Hardware Reuse as an Engineering Principle

A major objective of this project is to learn how infrastructure works rather than simply purchase finished solutions.

Repurposing older hardware provides several advantages:

- reduces unnecessary hardware cost
- extends the useful life of existing equipment
- creates dedicated systems for specific security roles
- provides hands-on hardware troubleshooting experience
- makes destructive testing less risky to daily-use systems
- encourages understanding of the entire computing stack

The older workstation is a good example.

Instead of being retired, it was upgraded with solid-state storage, given a clean Linux installation, hardened, and transformed into a dedicated engineering workstation.

---

# Physical Systems and Security Roles

The lab intentionally assigns different responsibilities to different systems.

```text
Hardened Linux Workstation
        │
        ├── Administration
        ├── Engineering
        ├── Documentation
        └── Infrastructure Management


Dedicated Security System
        │
        └── Offensive / Security Testing


Raspberry Pi Nodes
        │
        ├── Infrastructure
        ├── Monitoring
        ├── Automation
        └── Future Dedicated Services


Firewall Appliance
        │
        └── Routing and Security Enforcement


Managed Switch
        │
        └── VLAN and Layer 2 Segmentation
```

This separation reduces the temptation to make every device serve every purpose.

It also creates more realistic trust boundaries between administrative infrastructure, security testing systems, network services, and future targets.

---

# Skills Practiced

The physical build portion of the homelab provided hands-on experience with:

- computer hardware servicing
- SSD replacement and storage upgrades
- operating system installation
- Linux workstation deployment
- Raspberry Pi assembly and provisioning
- removable storage preparation
- network hardware deployment
- managed Ethernet switching
- firewall appliance deployment
- physical troubleshooting
- hardware reuse and lifecycle planning
- infrastructure role separation

These hardware tasks complement the networking, Linux administration, cybersecurity, and monitoring work performed elsewhere in the project.

---

# Project Philosophy

The objective of the homelab is not simply to produce a working network.

It is to understand how the environment works from the physical hardware upward.

That means learning how to:

```text
build it
configure it
secure it
observe it
break it
troubleshoot it
repair it
document it
```

The hardware build and repurposing work forms the physical foundation for the rest of the Defense Cyber Engineering Homelab.