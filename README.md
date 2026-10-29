## TNARC HQ: Internet Edge and Perimeter Firewall

## The Problem
TNARC's HQ has no internet connection yet. Staff need web access, and clients need to reach a public website and DNS hosted by TNARC. Additionally, As a financial company, TNARC cannot rely on a single provider. One ISP outage takes the business offline. Public facing servers must never become a path to the internal network. Leadership wants the perimeter secured before any branch connects.

## Requirements
1. Users reach an "internet" test server through either ISP.
2. If the primary ISP fails, traffic fails over automatically, and fails back when it recovers.
3. Internal addresses never appear on the internet side, configure NAT or PAT.
4. TNARC's public address block is reachable through both ISPs.
5. Internet users can reach the DMZ web and DNS servers, and nothing else.
6. DMZ servers can't start connections to the inside network.
7. Every allowed and denied flow is documented in a traffic-flow matrix and tested.
8. New edge devices follow the Stage 2 and Stage 3 baselines.

## Topology Changes
| Device | Model | Role | Connects to |
|--------|-------|------|-------------|
| ISP1-RTR | ISR 4331 | Simulated Internet Service Provider 1 | Edge-RTR |
| ISP2-RTR | ISR 4331 | Simulated Internet Service Provider 2 | Edge-RTR |
| Edge-RTR | 2911 | eBGP to both ISPs | ISP1, ISP2, ASA outside | 
| ASA | 5506-X | Perimeter firewall | Edge-RTR, Core-1, Core-2, DMZ-SW |
| DMZ-SW | 3650 | 

## Network Addressing

| Device | Port | | Device | Port | Subnet | Autonomous System |
|--------|------|-|--------|------|--------|-------------------|
| ISP1-RTR | g0/0/0 | -> | Edge-RTR | g0/0 | 198.51.100.0/30 | 65001 |
| ISP2-RTR | g0/0/0 | -> | Edge-RTR | g0/1 | 198.51.100.4/30 | 65002 |
| Edge-RTR | g0/0 | -> | ISP1-RTR | g0/0/0 | 198.51.100.0/30 | 65100 |
| Edge-RTR | g0/1 | -> | ISP2-RTR | g0/0/0 | 198.51.100.4/30 | 65100 |
| Edge-RTR | g0/2 | -> | ASA 5506 | g1/1 | 10.0.250.0/30 |
| ASA 5506 | g1/1 | -> | Edge-RTR | g0/2 | 10.0.250.0/30 |
| ASA 5506 | g1/2 | -> | Core-1 | g1/0/7 | 10.0.255.52/30 |
| ASA 5506 | g1/3 | -> | Core-2 | g1/0/7 | 10.0.255.56/30 |

## Traffic-Flow Matrix

## Key Decisions

## Verification

## Challenges and Fixes

## Limitations

## What I'd Do Next

