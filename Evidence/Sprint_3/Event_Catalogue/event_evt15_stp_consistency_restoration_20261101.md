# Security Event Record — STP VLAN-Consistency Restoration

- Event ID: EVT-15
- Jira issue: [SCRUM-40](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-40)
- Jira child issue: [SCRUM-169](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-169)
- Contributor: Eric Lindemulder
- Execution date: 11/01/26
- Observed event timestamp: 10.06.2026 03:40:22.667 PM
- Source device: SW-ACC-01
- Source IP: 10.20.99.11
- Packet Tracer file/version: [CYBEROPS07_Configuration_v3_4.pkt](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Packet_Tracer/Configurations/CYBEROPS07_Configuration_v3_4.pkt), 9.0.1.0858 
- Evidence status: Observed
- Local output: Observed
- Centralized receipt: Recieved

## Generating Action

Created a native-VLAN mismatch on a dedicated test link:

- SW-ACC-01 FastEthernet0/24 used native VLAN 998.
- SW-TEST-01 FastEthernet0/1 used native VLAN 1.

After observing spanning-tree VLAN-inconsistency blocking,
changed the temporary switch's native VLAN to match:

    configure terminal
    interface FastEthernet0/1
    switchport trunk native vlan 998
    end

Spanning tree subsequently reported restored port consistency
and unblocked FastEthernet0/24 for VLAN 998.

## Log Appearance

    %SPANTREE-2-UNBLOCK_CONSIST_PORT: Unblocking FastEthernet0/24 on VLAN0998. Port consistency restored.

## Benign Explanation

An administrator corrected an accidental native-VLAN mismatch,
allowing spanning tree to restore the affected port/VLAN.

## Malicious Explanation

An unauthorized operator could correct an inconsistency after
causing a disruption or while attempting to establish an
unauthorized switch connection.

The recovery message alone does not establish malicious activity.

## Distinguishing Evidence

Compare both trunk configurations with the approved network
design and change records. Review administrator activity where
available and identify the connected switch.

Correlate the recovery message with the preceding mismatch
and blocking events. Check spanning-tree state and connectivity
to determine what communication was restored.

## Classification

- Syslog severity: 2 — Critical
- Analytical severity: Pending — team taxonomy not yet established.
- Analytical question: Was consistency restored through an
  authorized correction, and what connectivity resumed?
- Response category: Pending team taxonomy.
- Security properties affected: Availability / Integrity

The message reports recovery. Its built-in Syslog severity does
not independently establish an active critical incident.

## Limitations

The message confirms that spanning tree removed the
inconsistency-based block for VLAN 998 on FastEthernet0/24.

It does not identify who corrected the configuration, establish
whether the change was authorized, or prove end-to-end service
availability. Additional configuration records, spanning-tree
output, and connectivity tests are needed.

This isolated test does not demonstrate production service impact.

## Evidence

- Initial mismatch configuration: [Link](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt15_sw_acc_01_generating_action_20261101.png)
- Native-VLAN correction command: [Link](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt15_sw_test_01_vlan_correction_20261101.png)
- Local unblocking message: [Link](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt15_sw_test_01_vlan_correction_20261101.png)
- Centralized entry or documented absence: [Link](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/network_evidence/test_evt15_syslog_message_20261101.png)


## Related Events

- EVT-11 — Native-VLAN Mismatch
- EVT-12 — STP VLAN-Inconsistency Port Blocking

This entry records recovery after correction of the condition
that produced those events.

## Restoration

Disconnected and removed the temporary switch, restored
FastEthernet0/24 to its original configuration, and removed
test VLAN 998.

