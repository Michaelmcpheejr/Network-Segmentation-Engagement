## Overview
Post-remediation validation confirms that segmentation controls were partially implemented to reduce exposure of critical systems while maintaining operational communication between user groups.

---

## Key Improvements

### 1. Server Segmentation Enforced
- Access to VLAN 20 (Servers) is now restricted
- User and Finance VLANs cannot directly communicate with server systems

**Validation Evidence:**
- PC1 unable to ping SRV1
- R2 unable to reach VLAN 20

**Impact:**
- Critical infrastructure (servers) is no longer broadly accessible
- Lateral movement to high-value assets is reduced

---

### 2. Firewall Policy Improvements
- Firewall zones and policies updated
- Traffic now follows defined paths rather than unrestricted flow

**Impact:**
- Increased control over inter-VLAN traffic
- Improved enforcement of network boundaries

---

## Remaining Exposure

### Flat User/Business VLAN Communication
- VLAN 10 (Users), VLAN 30 (Finance), and VLAN 40 (Engineering) remain fully accessible to each other

**Observed Behavior:**
- PC1 can communicate with VLAN 30 and VLAN 40
- VLAN 40 can communicate with all VLANs

---

## Risk Position (Post-Remediation)

| Area | Before | After |
|------|--------|--------|
| Server Exposure | High | Reduced |
| Firewall Segmentation | None | Partial |
| VLAN Isolation | Weak | Improved |
| Lateral Movement Risk | High | Low-Moderate |

---

## Conclusion

Remediation efforts successfully reduced exposure to critical systems by enforcing segmentation around server infrastructure. However, internal user and business VLANs remain in a flat trust model for communication purposes, leaving residual lateral movement risk.
