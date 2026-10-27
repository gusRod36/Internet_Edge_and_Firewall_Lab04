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

## Network Addressing

## Traffic-Flow Matrix

## Key Decisions

## Verification

## Challenges and Fixes

## Limitations

## What I'd Do Next

