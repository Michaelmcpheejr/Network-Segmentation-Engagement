# Findings

## Overview
The following findings were identified through configuration analysis and validated through the network engineer's interview responses.

A total of 5 findings were identified:
- 3 High
- 1 Medium
- 1 Low

---
# Network Segmentation Engagement

---

## FINDING F-001: Overly Permissive VLAN Trunking on User Access Switch

**Severity:** HIGH  
**Likelihood:** 3 | **Impact:** 5 | **Risk Score:** 15  

---

### Condition
SW2 trunk port (Gi1/0/1) is configured to allow VLANs 10, 20, 30, and 40. SW2 is designated as the User access switch serving VLAN 10, and operational requirements do not justify carrying Finance (VLAN 30) or Engineering (VLAN 40) traffic through this trunk.

---

### Evidence
- Screenshot: *SW2- Sh int Trunk.PNG*  

**Observed Configuration:**
- Port Gi1/0/1: Mode = on, Status = trunking  
- VLANs allowed on trunk: 10, 20, 30, 40  
- VLANs active in management domain: 10, 30  

**Expected Configuration:**
- VLANs allowed on trunk: 10 only  

---

### Risk
Finance (VLAN 30) and Engineering (VLAN 40) traffic is unnecessarily exposed to User access-layer infrastructure. This increases VLAN exposure beyond intended design boundaries and introduces risk if combined with misconfiguration, unauthorized trunking, or device compromise.

---

### Business Impact
- Increased exposure of sensitive Finance and Engineering traffic to User-layer infrastructure  
- Expanded attack surface at the access layer  
- Increased likelihood of lateral movement under adverse conditions  

---

### Attack Path
Compromised User VLAN 10 device → SW2 trunk carries unnecessary VLANs → Potential exposure to Finance/Engineering VLAN paths  

---

### Recommendation

```bash
interface Gi1/0/1
 switchport trunk allowed vlan 10
