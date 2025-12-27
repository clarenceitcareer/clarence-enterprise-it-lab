# Day 03 — Access VLAN Segmentation (USERS vs ADMINS)

## Objective
Implement and validate Layer-2 access VLAN segmentation to isolate USERS and ADMINS on a Cisco access switch.

## Scope
This exercise focuses strictly on Layer-2 behavior. No routing or default gateways are used.

## Topology
- 1 × Cisco 2960 access switch
- 2 × End devices
- PC1 → Fa0/1 (VLAN 10 — USERS)
- PC2 → Fa0/2 (VLAN 20 — ADMINS)

## Design Decisions
- VLANs enforce broadcast domain separation at Layer 2.
- Edge ports are forced into access mode to eliminate negotiation risk.
- Unused access ports are administratively shut down to reduce attack surface.
- Port descriptions are applied for operational clarity and audit readiness.

## Implementation Summary
- VLAN 10 created and named USERS
- VLAN 20 created and named ADMINS
- Fa0/1 statically assigned to VLAN 10
- Fa0/2 statically assigned to VLAN 20
- Fa0/3–Fa0/24 administratively shut down

## Verification
Commands used:
- show interfaces status

Results:
- Fa0/1 is connected and assigned to VLAN 10
- Fa0/2 is connected and assigned to VLAN 20
- No unintended active access ports detected

Raw evidence is stored separately under:
- 99-EVIDENCE/day03-vlans-access/

## Failure Injection
Scenario:
- Fa0/1 intentionally misassigned to VLAN 20

Observed Impact:
- USERS device placed into the incorrect broadcast domain
- Segmentation boundary violated

## Recovery
- Fa0/1 reassigned back to VLAN 10
- Interface status re-verified to confirm isolation restoration

## Key Takeaway
Access-layer segmentation depends on disciplined ingress port assignment and verification, not on IP addressing or routing.
