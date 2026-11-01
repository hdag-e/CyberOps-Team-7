# Security Event Record — Root Guard Blocking

- Event ID: EVT-14
- Jira issue: [SCRUM-40](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-40)
- Child Jira issued: [SCRUM-169](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-169)
- Contributor: Eric Lindemulder
- Execution date: 11/01/26
- Observed event timestamp: 10.06.2026 02:29:01.724 PM
- Source device: SW-ACC-01
- Source IP: 10.20.99.11
- Packet Tracer file/version: [CYBEROPS07_Configuration_v3_4.pkt](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Packet_Tracer/Configurations/CYBEROPS07_Configuration_v3_4.pkt), 9.0.1.0858 
- Evidence status: Observed
- Local output: Observed
- Centralized receipt: Recieved

## Generating Action

Created temporary VLAN 996 on SW-ACC-01 and configured
Fa0/24 as an access port in that VLAN with Root Guard enabled.

Connected a temporary switch, SW-TEST-01, using Fa0/1 in
VLAN 996. SW-ACC-01 used STP priority 32768, while the
temporary switch used priority 0.

The temporary switch advertised superior BPDUs, triggering
Root Guard blocking on SW-ACC-01.

## Log Appearance

%SPANTREE-2-ROOTGUARDBLOCK: Port 0/24 tried to become non-designated in VLAN 996.

## Benign Explanation

An administrator accidentally connected a switch with a
lower bridge priority than intended, causing it to advertise
a superior root and trigger Root Guard.

## Malicious Explanation

An attacker connected or reconfigured a switch to advertise
superior BPDUs and attempt to become the spanning-tree root.

## Distinguishing Evidence

Compare the connected switch's identity, bridge priority,
and configuration with the approved topology and asset inventory.
Review change records and administrator activity where available.
Use spanning-tree output to verify the resulting port state.

The message alone does not establish malicious intent.

## Classification

- Syslog severity: 2
- Analytical severity: Pending — team taxonomy not yet established.
- Analytical question: Was the superior BPDU caused by an
  authorized topology change, a configuration mistake, or
  an unauthorized attempt to influence root election?
- Response category: Pending team taxonomy.
- Security properties potentially affected: Integrity / Availability

## Limitations

The event reports Root Guard's response to superior BPDUs.
It does not establish the sender's intent or prove that a
root takeover succeeded.

The isolated test does not demonstrate production service impact.
Centralized forwarding is confirmed only if the corresponding
entry was observed at the collector.

## Evidence

- SW-ACC-01 generating action: [SW-ACC-01 Generating action](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt14_sw_acc_01__generating_action_20261101.png)
- SW-TEST-01 generation action: [SW-TEST-01 Generation action](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt14_sw_test_01_generating_action_20261101.png)
- Local event: [Local event](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt14_sw_acc_01_local_event_20261101.png)
- Centralized log: [Syslog message](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt14_syslog_message_20261101.png)

## Restoration

Disconnected and removed the temporary switch, restored
Fa0/24 to its original configuration, and removed the temporary
VLAN 996 and its test priority setting.

