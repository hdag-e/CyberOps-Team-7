# Baseline Connectivity Troubleshooting Log (SCRUM-90)

## Incident 01: Initial ARP Packet Timeout
- **Symptom:** Initial pings dropped 1 packet (80% success) while resolving MAC addresses across switch trunks.
- **Resolution:** Advanced Packet Tracer clock via Fast-Forward time button; subsequent tests yielded 100% success (5/5).
- **Status:** Resolved / Expected behavior.

## Incident 02: Switch Virtual Interface (SVI) State Verification
- **Symptom:** Ensured all SVIs on `SW-DIST-01` were up before executing ping tests.
- **Resolution:** Ran `show ip interface brief` on `SW-DIST-01` and confirmed Vlan10, Vlan20, Vlan30, Vlan50, Vlan99, and Vlan500 showed `up / up`.
- **Status:** Resolved.
