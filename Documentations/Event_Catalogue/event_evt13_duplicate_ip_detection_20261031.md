# Security Event Record — Duplicate IP Address Detection

- Event ID: EVT-13
- Jira issue: [SCRUM-40]()
- Jira Child issue:[SCRUM-169]()
- Contributor: Eric Lindemulder
- Execution date: 10/30/26
- Observed event timestamp: 10.06.2026 01:57:48.596 PM
- Source device: SW-ACC-01
- Source IP: 10.20.99.11
- Packet Tracer file/version: [CYBEROPS07_Configuration_v3_4.pkt](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Packet_Tracer/Configurations/CYBEROPS07_Configuration_v3_4.pkt), 9.0.1.0858 
- Evidence status: Observed at centralized collector
- Local output: Observed
- Centralized receipt: Received

## Generating Action

Created temporary VLAN 997 on SW-ACC-01 and configured its
VLAN interface with IP address 192.0.2.1/24.

Configured Fa0/24 as an access port in VLAN 997 and connected
a temporary test PC. Attempted to assign 192.0.2.1 to that PC.

Packet Tracer rejected the duplicate address assignment in
the endpoint configuration screen. However, the centralized
Syslog collector received a duplicate-address warning.

## Log Appearance

%IP-4-DUPADDR: Duplicate address 192.0.2.1 on Vlan997, sourced by 00E0.F759.B3D0

- Conflicting address: 192.0.2.1
- Affected interface: Vlan997
- Reported conflicting MAC: 00E0.F759.B3D0
- Timestamp: 10.06.2026 01:57:48.596 PM

## Benign Explanation

An administrator accidentally assigned an address already
used by the switch, possibly because of a typing error,
outdated addressing documentation, or incorrect static-IP setup.

## Malicious Explanation

An unauthorized endpoint deliberately claimed the switch's
address to impersonate it or disrupt communication.

## Distinguishing Evidence

Compare the reported MAC address with the test PC and asset
inventory. Review the approved addressing plan, endpoint
configuration, and change records to determine whether the
address assignment was authorized or accidental.

The warning alone does not establish intent.

## Classification

- Syslog severity: 4 — Warning
- Analytical severity: Pending — team taxonomy not yet established.
- Analytical question: Which endpoint claimed 192.0.2.1, was the
  assignment authorized, and did the conflict affect connectivity?
- Response category: Pending team taxonomy.
- Security properties potentially affected: Availability / Integrity

## Limitations

The warning identifies the conflicting IP, VLAN interface,
and reported source MAC, but does not establish malicious intent.

Packet Tracer rejected the duplicate assignment in the PC
configuration screen. The observed warning does not prove that
the PC retained the conflicting address.

The isolated test does not demonstrate production service impact.
MAC attribution requires comparison with endpoint records.

## Evidence

- Switch test configuration: [Switch test config](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt13_sw_acc_01_generating_action_20261031.png)
- Endpoint configuration/rejection: [Endpoint IP assignment](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt13_endpoint_ip_assignment_20261031.png)
- Centralized duplicate-address message: [Syslog message](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt13_syslog_message_20261031.png)
- Endpoint MAC verification: [Endpoint MAC verification](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt13_endpoint_mac_verification_20261031.png)

## Restoration

Disconnected the temporary PC, restored Fa0/24 to its original
configuration, and removed interface Vlan997 and VLAN 997.
