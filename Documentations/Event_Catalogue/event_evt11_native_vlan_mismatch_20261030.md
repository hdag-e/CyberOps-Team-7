# Security Event Record — Native-VLAN Mismatch

- Event ID: EVT-11
- Jira issue: [SCRUM-40](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-40)
- Child Jira issue: [SCRUM-169](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-169)
- Contributor:Eric Lindemulder
- Execution date: 10/30/2026
- Observed event timestamp: 10.06.2026 12:38:12.561 PM
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

%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/24 (998), with SW-TEST-01 FastEthernet0/1 (1).

## Benign Explanation

An administrator accidentally configured different native VLANs
on the two ends of a trunk during deployment or maintenance.

## Malicious Explanation

An unauthorized operator intentionally altered the native VLAN
to disrupt segmentation or interfere with network operation.

## Distinguishing Evidence

Compare both ports' configurations with the approved design,
change records, and administrator activity. The warning alone
does not establish malicious intent.

## Classification

- Syslog severity: 4
- Analytical severity: pending - team taxonomy not yet available
- Analytical question: Was the native-VLAN mismatch authorized
  as part of testing, or caused by an unintended change?
- Response category: pending - team taxonomy not yet available
- Security properties potentially affected: Integrity / Availability

## Limitations

The message identifies a mismatch but does not establish who
configured it, why it occurred, or whether traffic was affected.

## Evidence

- Test configuration/action: [SW-ACC-01 config/action](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt11_sw_acc_01_generating_action_20261030.png), [SW-TEST-01 config/action](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt11_sw_test_01_generating_action_20261030.png)
- Centralized log or documented absence: [Centralized log](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt11_syslog_message_20261030.png)

## Related Event

EVT-12 — STP VLAN-Inconsistency Port Blocking.
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
