# Network Architecture

**Project:** Defense Cyber Engineering Homelab  
**Document:** Network Architecture  
**Documentation Type:** Public / Sanitized

---

## Overview

The homelab uses a segmented network architecture designed to separate administrative systems, security-testing systems, infrastructure management, and legacy devices.

A pfSense firewall provides:

- Inter-VLAN routing
- Firewall enforcement
- Network segmentation
- Management access control
- Traffic logging

A managed Layer 2 switch provides VLAN transport between physical systems and the firewall.

---

## Logical Architecture

```text
                         Internet
                            │
                            │
                         pfSense
                            │
                      VLAN Trunk
                            │
                    Managed Switch
                            │
          ┌─────────────────┼─────────────────┐
          │                 │                 │
          │                 │                 │
     Administrative     Security-Test     Management
        Network            Network           Network
          │                 │                 │
          │                 │                 │
     Admin / Linux       Kali / Test      Infrastructure
      Workstation        Systems           Management
```

A separate legacy/internal network remains available for hardware that cannot fully participate in the preferred management architecture.

---

## Network Zones

| Zone | Purpose |
|---|---|
| Administrative | Trusted engineering and administrative systems |
| Security Testing | Offensive-security and controlled testing systems |
| Management | Infrastructure administration interfaces |
| Legacy/Internal | Devices requiring compatibility or documented exceptions |
| WAN | External network connectivity |

Exact VLAN identifiers, subnet assignments, interface mappings, and device addresses are intentionally omitted from public documentation.

---

## Administrative Network

The administrative network contains systems used to configure, maintain, and monitor the environment.

Primary responsibilities include:

- Firewall administration
- Infrastructure management
- Linux administration
- Security engineering
- Documentation
- Future monitoring and defensive tooling

Administrative placement does not automatically provide unrestricted access to other network zones.

Access remains controlled through explicit firewall policy.

---

## Security-Testing Network

The security-testing network contains systems used for:

- Offensive-security exercises
- Network reconnaissance
- Vulnerability validation
- Controlled attack simulation
- Future penetration-testing workflows

This network is intentionally separated from the management plane.

Security-testing systems should not be able to directly administer core infrastructure unless a specific exercise explicitly requires it.

---

## Management Network

The management network is dedicated to infrastructure administration.

Examples of systems or interfaces that may belong here include:

- Firewall management interfaces
- Managed infrastructure
- Future monitoring appliances
- Future dedicated administration services

Access follows a least-privilege model.

```text
Approved Administrative Host
            │
            │ Required Management Protocol
            ▼
     Management Interface
```

Broad access from entire user networks is avoided where practical.

---

## Legacy / Internal Network

Some infrastructure may remain on a legacy or internal network when hardware capabilities prevent full implementation of the preferred architecture.

These situations are treated as documented exceptions rather than silently considered equivalent to dedicated management isolation.

The long-term goal is to reduce reliance on this network as hardware and architecture evolve.

---

## Traffic Flow Model

### Administrative → Management

```text
Administrative Workstation
           │
           │ Explicitly Authorized Service
           ▼
      Management Network

             ALLOW
```

Only required management services are permitted.

---

### Security Testing → Management

```text
Security Testing
       │
       │
       ▼
 Management Network

       BLOCK
```

Security-testing systems are prevented from directly accessing management infrastructure by default.

---

### Management → Internal Networks

```text
Management Network
        │
        │
        ▼
 Internal Networks

    DEFAULT DENY
```

Management infrastructure does not automatically receive unrestricted access back into other network zones.

Required communication must be explicitly authorized.

---

## Firewall Enforcement

VLAN separation alone does not define the complete security boundary.

The firewall controls communication between network zones.

Rules are designed around:

```text
Specific Source
      ↓
Specific Destination
      ↓
Specific Protocol
      ↓
Specific Port
```

Broad inter-network allow rules are avoided where practical.

---

## Switching Model

The managed switch carries multiple VLANs between the firewall and connected systems.

The firewall uplink operates as a VLAN trunk.

```text
pfSense
   │
   │ Tagged VLAN Traffic
   ▼
Managed Switch
```

Endpoint ports are assigned according to the role of the connected system.

---

## Management Hardware Exception

The deployed switch does not provide the dedicated management-VLAN capability required to fully isolate its own management interface using the preferred design.

Because of this limitation:

```text
Firewall Management
        ↓
Dedicated Management Network

Switch Management
        ↓
Documented Legacy/Internal Path
```

This is treated as a known architecture exception.

The management IP was not simply moved into the management subnet because changing addressing alone would not provide genuine management-plane isolation.

---

## Security Boundaries

The architecture currently establishes the following major trust boundaries:

```text
Internet
   │
   ▼
Firewall Boundary
   │
   ├── Administrative Zone
   │
   ├── Security-Testing Zone
   │
   ├── Management Zone
   │
   └── Legacy/Internal Zone
```

Traffic crossing these boundaries is subject to firewall policy.

---

## Design Goals

The network architecture is designed to support:

- Least privilege
- Network segmentation
- Dedicated infrastructure management
- Separation of offensive and administrative systems
- Default-deny security policy
- Controlled experimentation
- Future centralized monitoring
- Future SIEM deployment
- Future vulnerability-management infrastructure
- Future Active Directory environments
- Future containerized services
- Future embedded and Raspberry Pi systems

---

## Expansion Model

Future systems should be assigned according to their security role rather than simply connected to whichever network is convenient.

Example:

```text
New System
    │
    ▼
Determine Security Role
    │
    ├── Administrative
    ├── Security Testing
    ├── Management
    ├── Server / Service Network
    ├── Monitoring
    └── Dedicated Lab Target
```

Additional VLANs may be introduced as the environment grows.

---

## Public Documentation Note

Operational details intentionally excluded from this document include:

- Exact IPv4 addresses
- Exact subnet assignments
- VLAN identifiers
- Internal network names
- Hostnames
- Usernames
- Physical interface mappings
- Switch port assignments
- MAC addresses
- Device identifiers
- WAN addressing

The architecture and security model remain documented without exposing unnecessary details about the live environment.