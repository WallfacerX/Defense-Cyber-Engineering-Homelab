
# Defense Cyber Engineering Homelab

A security-focused homelab built to develop practical experience in **cybersecurity engineering, network defense, Linux administration, offensive-security validation, and security architecture**.

Rather than focusing only on installing tools, this project emphasizes:

- Secure system design
- Network segmentation
- Least privilege
- Attack-surface reduction
- Configuration validation
- Defensive testing
- Reproducible build procedures
- Technical documentation
- Security engineering decision-making

---

## Project Philosophy

Every major component of the lab is:

1. Designed with a defined security purpose
2. Implemented incrementally
3. Tested after configuration
4. Validated from both allowed and denied perspectives
5. Documented as a reproducible build procedure

Intentional vulnerabilities are isolated to dedicated testing systems rather than introduced into administrative infrastructure.

---

## Current Project Areas

| Area | Status |
|---|---|
| pfSense firewall deployment | ✅ Complete |
| Network segmentation | ✅ Complete |
| Management network isolation | ✅ Complete |
| Offensive-security network | ✅ Complete |
| Linux administrative workstation hardening | 🟡 In Progress |
| STIG-style security assessment | ⏳ Planned |
| Centralized logging / SIEM | ⏳ Planned |
| Active Directory lab | ⏳ Planned |
| Vulnerability management | ⏳ Planned |
| Container security | ⏳ Planned |
| Embedded / Raspberry Pi systems | ⏳ Planned |

---

## Build Checklists

The primary documentation in this repository consists of **sanitized, reproducible build checklists**.

These are designed to serve simultaneously as:

- Build guides
- Security validation procedures
- Troubleshooting references
- Command study sheets
- Rebuild documentation

### Available

- [VLAN & Management Network Build Checklist](docs/build-checklists/VLAN_Network_Segmentation_Checklist.md)

---

## Documentation Approach

Public documentation intentionally generalizes operational details including:

- Internal IP addresses
- VLAN identifiers
- Internal network names
- Hostnames
- Usernames
- Interface assignments
- Switch port mappings
- Infrastructure identifiers

The goal is to demonstrate the **architecture, reasoning, implementation, and validation process** without publishing unnecessary details about the live environment.

---

## Current Focus

The current phase of the project is:

**Linux administrative workstation hardening**

This includes:

- Host firewall configuration
- Service reduction
- PAM authentication hardening
- Account lockout controls
- Privilege review
- SUID attack-surface assessment
- Kernel hardening
- Network kernel protections
- Logging and auditing

---

## Why I Built This

This homelab was created to move beyond classroom theory and develop practical experience designing, securing, validating, documenting, and troubleshooting real systems.

The long-term goal is to build an environment that can support increasingly realistic defensive and offensive cybersecurity exercises while maintaining a disciplined engineering approach to security.
