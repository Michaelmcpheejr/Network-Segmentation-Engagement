# Network Segmentation Engagement

## Overview
This engagement demostrates a network segmentation assessment performed on a multi-segment enterprise environment. The objective was to evaluate the effectiveness of segmentation controls, identify potential lateral movement risks, and provide actionable remediation guidance.

## Environment
- Core Switch (SW1)
- Access Switches (SW2 – Users/Finance, SW3 – Servers/Engineering)
- Routers (R1 Edge, R2 Finance, R3 Engineering)
- Palo Alto Firewall (Default Gateway for all VLANs)

## Business Context
- VLAN 10: Corporate Users  
- VLAN 20: Servers  
- VLAN 30: Finance  
- VLAN 40: Engineering  

## Key Focus Areas
- VLAN segmentation design
- Trunk configuration
- Firewall zoning and policy enforcement
- Access control mechanisms
- Lateral movement exposure

## Engagement Phases
1. Evidence Collection
2. Engineer Interview
3. Configuration Analysis
4. Risk Identification
5. Reporting & Recommendations

## Outcome
The assessment identified multiple control gaps that weaken segmentation boundaries and increase the risk of lateral movement. Findings were validated through both configuration analysis and engineer interview responses.

> Full findings and analysis are documented in the `/assessment` directory.
