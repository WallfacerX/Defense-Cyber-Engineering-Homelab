# VLAN & Management Network Build Checklist

**Project:** Defense Cyber Engineering Homelab  
**Component:** Network Segmentation  
**Documentation Type:** Public / Sanitized

---

## pfSense VLAN Setup

- [ ] Identify WAN interface
- [ ] Identify LAN/trunk interface
- [ ] Create trusted VLAN
- [ ] Create security-testing VLAN
- [ ] Create management VLAN
- [ ] Assign each VLAN to a pfSense interface
- [ ] Enable each VLAN interface
- [ ] Configure static IPv4 gateway for each VLAN
- [ ] Save and apply configuration

---

## Trusted Network

- [ ] Connect administrative workstation to trusted VLAN
- [ ] Confirm IP address: `ip addr`
- [ ] Confirm routing table: `ip route`
- [ ] Confirm gateway reachability: `ping <TRUSTED-GATEWAY>`

---

## Security Network

- [ ] Connect security-testing workstation to security VLAN
- [ ] Confirm IP address: `ip addr`
- [ ] Confirm routing table: `ip route`
- [ ] Confirm gateway reachability: `ping <SECURITY-GATEWAY>`

---

## Management Network

- [ ] Assign management VLAN gateway in pfSense
- [ ] Restrict management access to approved administrative host
- [ ] Permit HTTPS management only where required
- [ ] Block security-testing network from management network
- [ ] Leave management-originating traffic default-deny unless explicitly required

---

## Firewall Rules

- [ ] Create narrow administrative management rule
- [ ] Define specific source host
- [ ] Define specific management destination
- [ ] Define required protocol
- [ ] Define required destination port
- [ ] Confirm rule order
- [ ] Apply firewall changes
- [ ] Remove obsolete management rules

---

## Switch Configuration

- [ ] Create required VLANs on managed switch
- [ ] Configure pfSense uplink as VLAN trunk
- [ ] Tag required VLANs on trunk port
- [ ] Assign endpoint ports to intended VLANs
- [ ] Confirm no unintended VLAN memberships
- [ ] Save switch configuration

---

## Management Access Validation

- [ ] Confirm administrative workstation can reach management HTTPS: `curl -kI https://<MGMT-IP>`
- [ ] Confirm administrative workstation cannot use unauthorized protocols
- [ ] Confirm security-testing workstation cannot ping management gateway: `ping <MGMT-IP>`
- [ ] Confirm security-testing workstation cannot reach management HTTPS: `curl -kI --connect-timeout 5 https://<MGMT-IP>`
- [ ] Review pfSense firewall logs for expected blocks
- [ ] Confirm obsolete management path is inaccessible

---

## Connectivity Troubleshooting

- [ ] Confirm endpoint IP address: `ip addr`
- [ ] Confirm route and gateway: `ip route`
- [ ] Test Layer 3 reachability: `ping <IP>`
- [ ] Test HTTPS service: `curl -kI https://<IP>`
- [ ] Confirm VLAN exists in pfSense
- [ ] Confirm VLAN interface is enabled
- [ ] Confirm switch VLAN membership
- [ ] Confirm trunk tagging
- [ ] Confirm firewall rule
- [ ] Confirm firewall rule order
- [ ] Review firewall logs

---

## Final Verification

- [ ] Confirm trusted VLAN operates correctly
- [ ] Confirm security-testing VLAN operates correctly
- [ ] Confirm management VLAN operates correctly
- [ ] Confirm firewall segmentation is enforced
- [ ] Confirm management access follows least privilege
- [ ] Confirm security-testing network cannot reach management network
- [ ] Confirm switch configuration is saved
- [ ] Back up pfSense configuration
- [ ] Back up switch configuration
- [ ] Update separate architecture documentation