# Security Event Record — STP VLAN-Inconsistency Port Blocking

- Event ID: EVT-12
- Jira issue: [SCRUM-40](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-40)
- Child Jira issue: [SCRUM-169](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-169)
- Contributor:Eric Lindemulder
- Execution date: 10/30/2026
- Observed event timestamp: 10.06.2026 01:22:52.919 PM
- Source device: SW-ACC-01
- Source IP: 10.20.99.11
- Packet Tracer file/version: [CYBEROPS07_Configuration_v3_4.pkt](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Packet_Tracer/Configurations/CYBEROPS07_Configuration_v3_4.pkt), 9.0.1.0858 
- Evidence status: Observed
- Local output: Observed
- Centralized receipt: Recieved

## Generating Action

Connected SW-ACC-01 FastEthernet0/24 to SW-TEST-01
FastEthernet0/1 using a dedicated test link.

Configured native VLAN 998 on the access-switch port and
native VLAN 1 on the temporary-switch port.

## Log Appearance

%SPANTREE-2-BLOCK_PVID_LOCAL: Blocking FastEthernet0/24 on VLAN0998. Inconsistent local vlan.

## Benign Explanation

An administrator accidentally configured different native VLANs on connected switch ports during maintenance, causing spanning tree to block the affected port/VLAN.

## Malicious Explanation

An attacker with configuration access deliberately created a VLAN mismatch to trigger spanning-tree blocking and disrupt connectivity.

## Distinguishing Evidence

Compare both ports’ native-VLAN configurations with the approved design and change records. Review administrator login and command records where available to identify who made the change. Check spanning-tree state and connectivity tests to confirm the blocking and any service impact.

## Classification

- Syslog severity: 2
- Analytical severity: pending - team taxonomy not yet available
- Analytical question: Was the VLAN inconsistency caused by an authorized change, an accidental misconfiguration, or unauthorized activity, and did the resulting spanning-tree blocking affect legitimate connectivity?
- Response category: pending - team taxonomy not yet available
- Security properties potentially affected: Integrity / Availability

## Limitations

The message identifies a mismatch but does not establish who
configured it, why it occurred, or whether traffic was affected.

## Evidence

- Test configuration/action: [SW-ACC-01 config/action](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt12_sw_acc_01_generating_action_20261030.png), [SW-TEST-01 config/action](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt12_sw_test_01_generating_action_20261030.png)
- Centralized log or documented absence: [Centralized log](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt12_syslog_message_20261030.png)

## Related Event

EVT-11 — Native VLAN mismatch
Both events resulted from the same controlled mismatch test.

## Restoration

Disconnect the cable between SW-TEST-01 FA0/1 and SW-ACC-01 FA0/24
run commands
```text
enable
configure terminal
default interface FastEthernet0/24
no vlan 998
end
```
remove SW-TEST-01
