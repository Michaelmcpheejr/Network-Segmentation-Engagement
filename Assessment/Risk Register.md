# Risk Register

| ID | Risk Description | Affected Area | Likelihood (1–5) | Impact (1–5) | Risk Score | Severity | Control Gap | Recommended Action | Status |
|----|-----------------|--------------|------------------|--------------|------------|----------|-------------|--------------------|--------|
| F-001 | Unnecessary VLAN exposure on user access switch due to permissive trunk configuration | SW2 / VLAN 10,30,40 | 3 | 5 | 15 | High | VLAN segmentation not enforced at access layer | Restrict trunk to VLAN 10 only | Open |
| F-002 | Excessive VLAN exposure on server switch increases cross-segment visibility | SW3 / VLAN 20,10,30,40 | 3 | 5 | 15 | High | Improper trunk configuration | Restrict trunk to VLAN 20 only | Open |
| F-003 | Firewall does not enforce segmentation between internal VLANs (flat trust model) | Palo Alto Firewall | 3 | 4 | 12 | High | No internal zone segmentation or policy enforcement | Implement zone-based segmentation and least-privilege policies | Open |
| F-004 | Lack of access control mechanisms protecting Finance network | R2 / VLAN 30 | 2 | 4 | 8 | Medium | No ACLs or filtering applied | Implement inbound ACLs for Finance segment | Open |
| F-005 | Use of default Native VLAN (VLAN 1) across trunk links | All switches | 1 | 2 | 2 | Low | Security hardening not applied | Change native VLAN to unused VLAN (e.g., 999) | Open |
