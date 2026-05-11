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
Framework Mapping
NIST 800-53: SC-7, AC-4
CIS Controls: 12.2
NIST CSF: PR.AC-5
---

---
# FINDING F-002: Overly Permissive VLAN Trunking on Server Access Switch

**Severity:** HIGH  
**Likelihood:** 3 | **Impact:** 5 | **Risk Score:** 15  

---

## Condition
SW3 trunk port (Gi2/0/1) is configured to allow VLANs 10, 20, 30, and 40. SW3 is designated as the Server access switch serving VLAN 20 and does not require additional VLANs on this trunk.

---

## Evidence
- Screenshot: *SW3- sh int trunk.PNG*

**Observed Configuration:**
- VLANs allowed: 10, 20, 30, 40  
- VLANs active: 20, 40  

**Expected Configuration:**
- VLANs allowed: 20 only  

---

## Risk
User, Finance, and Engineering VLAN traffic is unnecessarily exposed to Server-layer infrastructure. This increases VLAN exposure and creates conditions where compromise of a server or network device may expand visibility across additional segments.

---

## Business Impact
- Server layer exposed to multiple business segments  
- Increased lateral movement potential  
- Reduced segmentation effectiveness  

---

## Attack Path
Compromised Server VLAN 20 device → SW3 trunk carries additional VLANs → Potential exposure to User/Finance/Engineering VLAN paths  

---
Framework Mapping
NIST 800-53: SC-7, AC-4
CIS Controls: 12.2
NIST CSF: PR.AC-5
---
---
# FINDING F-003: Firewall Not Functioning as Segmentation Control

**Severity:** HIGH  
**Likelihood:** 3 | **Impact:** 4 | **Risk Score:** 12  

---

## Condition
The Palo Alto firewall places all internal VLANs (10, 20, 30, 40) within a single “Inside” zone. Security policies allow unrestricted intrazone traffic, and no segmentation enforcement exists between internal segments.

The firewall is not functioning as a segmentation control.

---

## Evidence
- Zones: Only “Inside” and “Outside” configured  
- All VLAN subinterfaces assigned to “Inside”  
- Intrazone-default policy: Allow  
- No App-ID enforcement  
- No threat profiles  

---

## Risk
All internal traffic flows freely without inspection or restriction. Segmentation is defined logically through VLANs but not enforced through technical controls, resulting in a flat internal trust model.

---

## Business Impact
- No east-west visibility  
- No enforcement of least privilege  
- No defense-in-depth  
- Increased risk of lateral movement  
- Compliance gaps (NIST, SOX, CIS)  

---

## Attack Path
Attacker gains access to internal VLAN → Intrazone allow policy permits unrestricted movement → All segments accessible  

---

## Recommendation

### Implement Zone-Based Segmentation

- Users (VLAN 10)  
- Servers (VLAN 20)  
- Finance (VLAN 30)  
- Engineering (VLAN 40)  

### Enforce Policies
- Allow only required communication  
- Deny unnecessary traffic  

### Enable Security Controls
- App-ID  
- Threat profiles  
- Logging  

---

## Framework Mapping
- NIST 800-53: SC-7, AC-4, SI-4  
- CIS Controls: 12.3, 13.3  
- NIST CSF: PR.AC-5, DE.CM-1

---
# FINDING F-004: Missing Access Control Mechanisms on Finance Segment

**Severity:** MEDIUM  
**Likelihood:** 2 | **Impact:** 4 | **Risk Score:** 8  

---

## Condition
R2 is configured as the gateway for the Finance network (10.0.30.0/24). No access control mechanisms were identified in the provided evidence restricting traffic to this segment.

---

## Evidence
- Screenshot: *R2-config---sh ip route.PNG*  
- No evidence of ACLs in provided configuration  

---

## Risk
Once routing paths exist to the Finance network, there are no controls enforcing least privilege or segmentation at the router level.

---

## Business Impact
- No defense-in-depth for Finance systems  
- Increased likelihood of unauthorized access  
- Limited visibility into access attempts  
---
Framework Mapping
NIST 800-53: AC-4, SC-7, AU-2
CIS Controls: 12.6
---
---
# FINDING F-005: Native VLAN Security Best Practice Violation

**Severity:** LOW  
**Likelihood:** 1 | **Impact:** 2 | **Risk Score:** 2  

---

## Condition
All trunk ports use the default Native VLAN 1 instead of an unused VLAN.

---

## Evidence
- Core, SW2, SW3 trunk configurations show Native VLAN = 1  

---

## Risk
While not directly exploitable in isolation, this configuration contributes to a weakened segmentation posture and may introduce risk when combined with other vulnerabilities.

---

## Business Impact
- Deviation from industry best practices  
- Increased risk when combined with other issues  
---
Framework Mapping
CIS Controls: 12.2
NIST 800-53: SC-7
