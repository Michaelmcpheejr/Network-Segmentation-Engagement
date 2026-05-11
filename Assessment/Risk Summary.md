# Risk Summary

## Findings Overview

| ID | Finding | Severity |
|----|--------|--------|
| F-001 | SW2 Overly Permissive Trunk | High |
| F-002 | SW3 Overly Permissive Trunk | High |
| F-003 | Firewall Not Segmenting Internal VLANs | High |
| F-004 | Missing ACLs on Finance Router | Medium |
| F-005 | Native VLAN Default | Low |

---

## Risk Themes

### 1. Lack of Segmentation Enforcement
Segmentation is defined but not enforced across the network.

### 2. Excessive VLAN Exposure
Trunk configurations allow unnecessary VLAN propagation.

### 3. Absence of Access Control
No ACLs or filtering mechanisms protect sensitive segments.

### 4. Limited Visibility
Internal traffic is not effectively monitored or controlled.

---

## Overall Risk Posture

**High Risk**

The combination of:
- flat firewall design
- unrestricted VLAN propagation
- lack of access controls

creates a high likelihood of lateral movement in the event of compromise.

---

## Recommendation Summary

- Implement firewall-based segmentation
- Restrict VLANs on trunk links
- Deploy ACLs for sensitive segments
- Enforce least-privilege access
- Improve monitoring and logging
