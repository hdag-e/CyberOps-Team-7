# Repository Guidelines & File Naming Conventions

## Packet Tracer (.pkt) File Check-Out Protocol
Packet Tracer files cannot be merged concurrently. To prevent overwriting work:
1. Notify the team in chat before editing the master `.pkt` file.
2. Save updated topologies using explicit versioning: `CYBEROPS07_Topology_vX.Y.pkt` (e.g., `CYBEROPS07_Topology_v1.0.pkt`).

## General File Naming Conventions
* Use lowercase letters, numbers, and underscores (no spaces).
* Standard Format: `[category]_[description]_[date/version].[ext]`
* Examples:
  * Config: `router_edge_isr4331_v1.txt`
  * Evidence: `test_t01_syslog_verification_20261001.png`
  * Incident: `incident_01_reconstruction_v1.docx`

## Commit Message Format
All commits must reference the active Jira ticket:
`[JIRA-ID]: [Brief description of changes]`
* Example: `SCRUM-25: Added initial repository structure and README`
