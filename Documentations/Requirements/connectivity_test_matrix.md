
# Baseline Connectivity Test Matrix (SCRUM-88 / SCRUM-89)

## 1. Overview
This document records baseline connectivity verification for the CYBEROPS-07 enterprise topology in Cisco Packet Tracer. All tests confirm Layer 2/3 reachability across trust segments.

## 2. Test Matrix Results

| Test ID | Source Device | Source IP | Target Device | Target IP | Protocol | Expected Result | Observed Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **T-01.1** | PC-USER-01 | 10.20.10.10 | SW-DIST-01 | 10.20.10.1 | ICMP | Pass (Gateway Reachable) | Success (100%, 5/5) | ✅ Pass |
| **T-01.2** | PC-ADMIN-01 | 10.20.20.10 | SW-DIST-01 | 10.20.20.1 | ICMP | Pass (Gateway Reachable) | Success (100%, 5/5) | ✅ Pass |
| **T-01.3** | PC-USER-01 | 10.20.10.10 | SRV-APP-01 | 10.20.30.11 | ICMP | Pass (Inter-VLAN Route) | Success (100%, 5/5) | ✅ Pass |
| **T-01.4** | PC-ADMIN-01 | 10.20.20.10 | SRV-SYSLOG | 10.20.50.10 | ICMP | Pass (Inter-VLAN Route) | Success (100%, 5/5) | ✅ Pass |
| **T-01.5** | LAPTOP-ROGUE-01 | 192.168.50.10 | SW-DIST-01 | 192.168.50.1 | ICMP | Pass (Gateway Reachable) | Success (100%, 5/5) | ✅ Pass |
