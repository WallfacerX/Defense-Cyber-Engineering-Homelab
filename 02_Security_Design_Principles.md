# Security Design Principles

**Project:** Defense Cyber Engineering Homelab  
**Document:** Security Design Principles  
**Documentation Type:** Public / Sanitized

---

## Purpose

This document defines the core security principles used to guide design decisions throughout the homelab.

The environment is intended to model practical security engineering, not simply tool installation.

---

## Least Privilege

Access is granted only when required for a specific task.

Examples include:

- Restricting management access to approved administrative systems
- Limiting firewall rules to required protocols and ports
- Removing unnecessary group memberships
- Avoiding broad inter-VLAN allow rules
- Retaining privileged functionality only when it serves a known purpose

General pattern:

```text
Specific Source
      ↓
Specific Destination
      ↓
Required Protocol
      ↓
Required Port
```

---

## Default Deny

Traffic and access should be denied unless explicitly permitted.

This principle is applied to:

- Inter-VLAN firewall policy
- Management network access
- Host firewall configuration
- Service exposure
- Future server and infrastructure deployments

A missing requirement should not automatically become an allow rule.

---

## Separation of Duties

Systems are assigned roles based on their purpose.

Examples:

```text
Administrative Workstation
→ Engineering and infrastructure administration

Security Workstation
→ Offensive-security testing

Management Network
→ Infrastructure management

Dedicated Targets
→ Controlled vulnerable systems
```

Administrative systems are not intentionally weakened for offensive-security practice.

Testing environments are separated from systems used to manage the lab.

---

## Minimize Attack Surface

Unnecessary services, packages, network listeners, and privileged components are reviewed and removed when practical.

Before removing a component:

- Determine its purpose
- Check dependencies
- Simulate removal when possible
- Understand potential impact
- Validate system behavior afterward

Security hardening should reduce exposure without blindly breaking required functionality.

---

## Explicit Trust Boundaries

Network placement does not automatically imply unlimited trust.

A system on an administrative network may still receive only narrow access to management infrastructure.

Likewise, a management network is not automatically allowed to initiate traffic into every internal network.

Trust is defined through policy, not merely topology.

---

## Validate Both Allowed and Denied Behavior

A security control is not considered validated only because permitted traffic works.

Testing should also confirm that prohibited traffic fails.

Examples:

```text
Expected management connection
→ ALLOWED

Unauthorized protocol
→ BLOCKED

Security-testing network to management
→ BLOCKED

Deprecated management path
→ BLOCKED
```

Negative testing provides evidence that security boundaries are actually enforced.

---

## Configuration Is Not Proof

A configured control should be tested whenever practical.

Examples include:

- Reviewing firewall logs after blocked traffic tests
- Testing authentication lockout behavior
- Confirming disabled services are no longer listening
- Verifying persistent kernel settings
- Confirming obsolete access paths are inaccessible

The intended state and the observed state should match.

---

## Preserve Administrative Integrity

Administrative systems should remain trustworthy.

Intentional vulnerabilities belong on dedicated lab targets rather than on the workstation used to manage infrastructure.

Preferred model:

```text
Administrative System
→ Hardened

Security Testing System
→ Offensive Tooling

Target Systems
→ Intentionally Vulnerable When Required
```

This keeps testing realistic without weakening the control plane.

---

## Document Exceptions

Hardware and software limitations should be documented rather than hidden.

If a device cannot support the preferred architecture:

- Identify the limitation
- Record the affected security control
- Document the resulting exception
- Apply compensating controls where practical
- Reassess when hardware or architecture changes

A limitation should never be represented as a security feature.

---

## Prefer Supported Configuration Methods

Security changes should use supported operating-system or application mechanisms whenever practical.

Examples include:

- Package-management tools
- Supported configuration directories
- Native firewall interfaces
- Service-management tools
- Vendor-supported settings

Direct modification of generated or managed configuration should be avoided when a supported method exists.

---

## Make Changes Incrementally

Security changes are applied in small, testable steps.

Typical workflow:

```text
Inspect
   ↓
Understand
   ↓
Back Up
   ↓
Change
   ↓
Validate
   ↓
Document
```

This reduces troubleshooting complexity and makes rollback easier.

---

## Maintain Recovery Paths

High-impact security changes should include a recovery plan.

Examples include:

- Configuration backups
- Known-good authentication files
- System snapshots
- Firewall configuration backups
- Staged testing before persistence
- Temporary privileged recovery sessions during authentication changes

Security hardening should not create unnecessary risk of administrative lockout.

---

## Treat Dependencies as Security-Relevant

A package or service should not be removed solely because it appears unnecessary.

Dependencies may support:

- Networking
- Authentication
- Desktop functionality
- Package management
- Hardware access
- Application sandboxing

Removing unused functionality is valuable, but dependency impact must be understood first.

---

## Separate Security From Compliance

Practical security controls and formal compliance requirements are related but not identical.

The lab distinguishes between:

```text
Security Engineering Baseline
```

and:

```text
Compliance / STIG Assessment
```

This allows controls to be evaluated based on:

- Actual risk reduction
- Operational impact
- Compliance requirements
- Engineering tradeoffs

A control should not be assumed optimal merely because it appears in a checklist.

---

## Reproducibility

Major lab components should be rebuildable from documented procedures.

Public documentation focuses on:

- Build checklists
- Security design
- Validation methodology
- Lessons learned
- Architecture decisions

Private operational notes retain the detailed implementation history.

---

## Public Documentation Security

Public documentation intentionally excludes unnecessary operational details.

Generalized information includes:

- Exact internal addressing
- VLAN identifiers
- Internal network names
- Hostnames
- Usernames
- Interface mappings
- Switch ports
- MAC addresses
- Infrastructure identifiers
- WAN addressing

The objective is to demonstrate technical capability without exposing the live environment.

---

## Guiding Principle

Every security control in the lab should answer three questions:

1. **What risk does this reduce?**
2. **How do I know it is working?**
3. **What could it break?**

If those questions cannot be answered, the control requires further investigation before implementation.