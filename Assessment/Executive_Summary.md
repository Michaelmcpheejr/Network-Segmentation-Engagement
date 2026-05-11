# Executive Summary

## Overview
A network segmentation assessment was conducted to evaluate the effectiveness of controls across VLAN architecture, switching infrastructure, firewall policy, and access control mechanisms.

## Key Findings
- Segmentation is defined through VLAN design but not enforced through security controls
- Firewall is not functioning as an internal segmentation control (flat trust model)
- Trunk configurations allow unnecessary VLAN propagation across access switches
- No access control mechanisms restrict access to sensitive Finance systems
- Monitoring and incident response capabilities are limited

## Risk Summary
The current architecture introduces a high risk of lateral movement in the event of a compromised system. Lack of enforcement controls allows internal traffic to move freely across segments without restriction or visibility.

## Business Impact
- Increased risk of unauthorized access to sensitive financial data
- Lack of defense-in-depth controls
- Limited visibility into internal network activity
- Potential compliance gaps (SOX, NIST, CIS)

## Conclusion
While segmentation intent exists, the absence of enforcement mechanisms results in a flat internal trust model. Remediation efforts should focus on implementing layered controls, including firewall segmentation, ACLs, and least-privilege access policies.
