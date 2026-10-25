# Centralized Logging Source Verification

- Contributor: Eric Lindemulder
- Date: 10/25/26
- Parent Jira issue: [SCRUM-33](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-33)
- Child Jira issue: [SCRUM-111](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-111)
- Related acceptance test: T-01
- Packet Tracer file/version: CYBEROPS07_Configuration_v1_2.pkt, Packet Tracer Version 9.0.1.0858
- Monitoring inventory: [Monitoring Source Inventory](Network_Foundation/Monitoring_Source_inventroy.md)
- Central Syslog server: 10.20.50.10

## Objective

Verify that each intended direct logging source can send a
representative event to the central Syslog server.

This verification covers the tested event types only.

## Verification Matrix

| Source | Event tested | Central log observed? | Status | Reason / limitations | Evidence |
|---|---|---|---|---|---|
| RTR-EDGE-01 | Interface state change | Yes | Verified | Central log showed time, host IP, and message | [Router CLI Output](../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_interface_change_20261025.PNG), [Central Syslog Entry](../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_syslog_recieved_20261025.PNG)|
| RTR-INT-01 | Interface state change | Yes | Verified | Central log showed time, host IP, and message | [Router CLI Output](../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_interface_change_20261025.PNG), [Central Syslog Entry](../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_syslog_recieved_20261025.PNG)|
| RTR-INT-02 | Interface state change | Yes | Verified | Central log showed time, host IP, and message | [Router CLI Output](../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_interface_change_20261025.PNG), [Central Syslog Entry](../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_syslog_recieved_20261025.PNG)|
| SW-DIST-01 | Configuration change | Yes | Verified | Configuration-change notification received centrally. Interface state changes was also tested, but no corresponding message was observed.| [Switch CLI Output](../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_config_change_20261025.PNG), [Central Syslog Entry](../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_syslog_recieved_20261025.PNG)|
| SW-ACC-01 | Configuration change | Yes | Verified | Configuration-change notification received centrally. Interface state changes was also tested, but no corresponding message was observed.| [Switch CLI Output](../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_config_change_20261025.PNG), [Central Syslog Entry](../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_syslog_recieved_20261025.PNG)|
| SW-ACC-02 | Configuration change | Yes | Verified | Configuration-change notification received centrally. Interface state changes was also tested, but no corresponding message was observed.| [Switch CLI Output](../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_config_change_20261025.PNG), [Central Syslog Entry](../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_syslog_recieved_20261025.PNG)|
| SW-ACC-03 | Configuration change | Yes | Verified | Configuration-change notification received centrally. Interface state changes was also tested, but no corresponding message was observed.| [Switch CLI Output](../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_config_change_20261025.PNG), [Central Syslog Entry](../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_syslog_recieved_20261025.PNG)|

## Status Definitions

- Verified: The tested event appeared centrally and could be
  matched to its source.
- Partially verified: Central activity was observed, but source
  attribution or event information was incomplete.
- Unverified: No matching event was observed, or testing was
  not completed. Record the reason.
- Unsupported: Evidence confirms the intended logging capability
  is unavailable.
- N/A: Inventoried supporting device that is not intended to
  send logs directly. Record the reason.

## Test Record: [RTR-EDGE-01]

### Test Information

- Contributor:Eric Lindmeulder
- Test date and time, including timezone: 10/25/2026 3:15 PM EST
- Source device: RTR-EDGE-01
- Interface tested: Gigabit Ethernet 0/0/2
- Initial interface state: Administratively enabled, Physical link down no device connected

### Preconditions

- Central Syslog service is enabled.
- The selected interface is confirmed suitable for testing.
- The test preserves the device's path to the collector.

### Steps Performed

1. Record the existing collector entries and test start time.
2. Change the selected interface's administrative state.
3. Inspect the central Syslog server for a matching event.
4. Restore the interface to its original state.
5. Capture the CLI output and centralized log evidence.

### Commands Used

```text
configure terminal
interface gigabitethernet 0/0/2
shutdown
no shutdown
exit
```

### Expected Result

An interface-state message appears at the central collector
and can be attributed to the tested device.

### Actual Result

Describe what was observed.
Paste the relevant centralized log entry if available.

- Source identifier displayed: Host IP, 10.20.252.1
- Event/interface details displayed: Interface gigabit ethernet 0/0/2 changed state to down
- Timestamp displayed: 10.06.2026 5:11:46.225 AM
- Timezone displayed, if any: None

### Status and Reason

[Verified]

The status is verified because the device produced a log that was sent and collected by the centralized server

### Evidence

- [Generating action and CLI output](../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_interface_change_20261025.PNG)
- [Centralized log entry](../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_syslog_recieved_20261025.PNG)

### Limitations / Follow-up

N/A

### Restoration

Interface was restored to the administrative up state

## Test Record: [RTR-INT-01]

### Test Information

- Contributor:Eric Lindemulder
- Test date and time, including timezone: 10/25/2026 3:16 PM EST
- Source device: RTR-INT-01
- Interface tested: Gigabit Ethernet 0/0/2
- Initial interface state: Administratively enabled, Physical link down no device connected

### Preconditions

- Central Syslog service is enabled.
- The selected interface is confirmed suitable for testing.
- The test preserves the device's path to the collector.

### Steps Performed

1. Record the existing collector entries and test start time.
2. Change the selected interface's administrative state.
3. Inspect the central Syslog server for a matching event.
4. Restore the interface to its original state.
5. Capture the CLI output and centralized log evidence.

### Commands Used

```text
configure terminal
interface gigabitethernet 0/0/2
shutdown
no shutdown
exit
```

### Expected Result

An interface-state message appears at the central collector
and can be attributed to the tested device.

### Actual Result

Describe what was observed.
Paste the relevant centralized log entry if available.

- Source identifier displayed: Host IP, 10.20.252.9
- Event/interface details displayed: Interface gigabit ethernet 0/0/2 changed state to down
- Timestamp displayed: 10.06.2026 5:14:07.900 AM
- Timezone displayed, if any: None

### Status and Reason

[Verified]

The status is verified because the device produced a log that was sent and collected by the centralized server

### Evidence

- [Generating action and CLI output](../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_interface_change_20261025.PNG)
- [Centralized log entry](../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_syslog_recieved_20261025.PNG)

### Limitations / Follow-up

N/A

### Restoration

Interface was restored to the administrative up state

## Test Record: [RTR-INT-02]

### Test Information

- Contributor:Eric Lindemulder
- Test date and time, including timezone: 10/25/2026 3:24 PM EST
- Source device: RTR-INT-02
- Interface tested: Gigabit Ethernet 0/0/2
- Initial interface state: Administratively enabled, Physical link down no device connected

### Preconditions

- Central Syslog service is enabled.
- The selected interface is confirmed suitable for testing.
- The test preserves the device's path to the collector.

### Steps Performed

1. Record the existing collector entries and test start time.
2. Change the selected interface's administrative state.
3. Inspect the central Syslog server for a matching event.
4. Restore the interface to its original state.
5. Capture the CLI output and centralized log evidence.

### Commands Used

```text
configure terminal
interface gigabitethernet 0/0/2
shutdown
no shutdown
exit
```

### Expected Result

An interface-state message appears at the central collector
and can be attributed to the tested device.

### Actual Result

Describe what was observed.
Paste the relevant centralized log entry if available.

- Source identifier displayed: Host IP, 10.20.252.13
- Event/interface details displayed: Interface gigabit ethernet 0/0/2 changed state to down
- Timestamp displayed: 10.06.2026 5:21:30.111 AM
- Timezone displayed, if any: None

### Status and Reason

[Verified]

The status is verified because the device produced a log that was sent and collected by the centralized server

### Evidence

- [Generating action and CLI output](../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_interface_change_20261025.PNG)
- [Centralized log entry](../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_syslog_recieved_20261025.PNG)

### Limitations / Follow-up

N/A

### Restoration

Interface was restored to the administrative up state

## NOTE: there are timestamp discrepancies between the routers and switches tested this is because the packet tracer file was closed and re-opened without saving causing the time to go back to the last save.

## Test Record: [SW-DIST-01]

### Test Information

- Contributor:Eric Lindemulder
- Test date and time, including timezone: 10/25/2026 3:41 PM EST
- Source device: SW-DIST-01
- Interface tested: Gigabit Ethernet 0/2
- Initial interface state: Administratively enabled, Physical link down no device connected

### Preconditions

- Central Syslog service is enabled.
- The selected interface is confirmed suitable for testing.
- The test preserves the device's path to the collector.

### Steps Performed

1. Record the existing collector entries and test start time.
2. Change the selected interface's administrative state.
3. Inspect the central Syslog server for a matching event.
4. Restore the interface to its original state.
5. Capture the CLI output and centralized log evidence.

### Commands Used

```text
configure terminal
interface gigabitethernet 0/2
shutdown
no shutdown
exit
```

### Expected Result

An configuration change message appears at the central collector
and can be attributed to the tested device.

### Actual Result

Describe what was observed.
Paste the relevant centralized log entry if available.

- Source identifier displayed: Host IP, 10.20.50.1
- Event/interface details displayed: Configured from console by console
- Timestamp displayed: 10.06.2026 5:06:00.941 AM
- Timezone displayed, if any: None

### Status and Reason

[Verified]

The status is verified because the device produced a log that was sent and collected by the centralized server

### Evidence

- [Generating action and CLI output](../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_config_change_20261025.PNG)
- [Centralized log entry](../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_syslog_recieved_20261025.PNG)

### Limitations / Follow-up

N/A

### Restoration

Interface was restored to the administrative up state

## Test Record: [SW-ACC-01]

### Test Information

- Contributor:Eric Lindemulder
- Test date and time, including timezone: 10/25/2026 3:46 PM EST
- Source device: SW-ACC-01
- Interface tested: Gigabit Ethernet 0/2
- Initial interface state: Administratively enabled, Physical link down no device connected

### Preconditions

- Central Syslog service is enabled.
- The selected interface is confirmed suitable for testing.
- The test preserves the device's path to the collector.

### Steps Performed

1. Record the existing collector entries and test start time.
2. Change the selected interface's administrative state.
3. Inspect the central Syslog server for a matching event.
4. Restore the interface to its original state.
5. Capture the CLI output and centralized log evidence.

### Commands Used

```text
configure terminal
interface gigabitethernet 0/2
shutdown
no shutdown
exit
```

### Expected Result

An configuration change message appears at the central collector
and can be attributed to the tested device.

### Actual Result

Describe what was observed.
Paste the relevant centralized log entry if available.

- Source identifier displayed: Host IP, 10.20.99.11
- Event/interface details displayed: Configured from console by console
- Timestamp displayed: 10.06.2026 5:11:15.218 AM
- Timezone displayed, if any: None

### Status and Reason

[Verified]

The status is verified because the device produced a log that was sent and collected by the centralized server

### Evidence

- [Generating action and CLI output](../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_config_change_20261025.PNG)
- [Centralized log entry](../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_syslog_recieved_20261025.PNG)

### Limitations / Follow-up

N/A

### Restoration

Interface was restored to the administrative up state


## Test Record: [SW-ACC-02]

### Test Information

- Contributor:Eric Lindemulder
- Test date and time, including timezone: 10/25/2026 3:52 PM EST
- Source device: SW-ACC-02
- Interface tested: Gigabit Ethernet 0/2
- Initial interface state: Administratively enabled, Physical link down no device connected

### Preconditions

- Central Syslog service is enabled.
- The selected interface is confirmed suitable for testing.
- The test preserves the device's path to the collector.

### Steps Performed

1. Record the existing collector entries and test start time.
2. Change the selected interface's administrative state.
3. Inspect the central Syslog server for a matching event.
4. Restore the interface to its original state.
5. Capture the CLI output and centralized log evidence.

### Commands Used

```text
configure terminal
interface gigabitethernet 0/2
shutdown
no shutdown
exit
```

### Expected Result

An configuration change message appears at the central collector
and can be attributed to the tested device.

### Actual Result

Describe what was observed.
Paste the relevant centralized log entry if available.

- Source identifier displayed: Host IP, 10.20.99.12
- Event/interface details displayed: Configured from console by console
- Timestamp displayed: 10.06.2026 5:17:02.203 AM
- Timezone displayed, if any: None

### Status and Reason

[Verified]

The status is verified because the device produced a log that was sent and collected by the centralized server

### Evidence

- [Generating action and CLI output](../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_config_change_20261025.PNG)
- [Centralized log entry](../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_syslog_recieved_20261025.PNG)

### Limitations / Follow-up

N/A

### Restoration

Interface was restored to the administrative up state


## Test Record: [SW-ACC-03]

### Test Information

- Contributor:Eric Lindemulder
- Test date and time, including timezone: 10/25/2026 3:53 PM EST
- Source device: SW-ACC-03
- Interface tested: Gigabit Ethernet 0/2
- Initial interface state: Administratively enabled, Physical link down no device connected

### Preconditions

- Central Syslog service is enabled.
- The selected interface is confirmed suitable for testing.
- The test preserves the device's path to the collector.

### Steps Performed

1. Record the existing collector entries and test start time.
2. Change the selected interface's administrative state.
3. Inspect the central Syslog server for a matching event.
4. Restore the interface to its original state.
5. Capture the CLI output and centralized log evidence.

### Commands Used

```text
configure terminal
interface gigabitethernet 0/2
shutdown
no shutdown
exit
```

### Expected Result

An configuration change message appears at the central collector
and can be attributed to the tested device.

### Actual Result

Describe what was observed.
Paste the relevant centralized log entry if available.

- Source identifier displayed: Host IP, 10.20.99.13
- Event/interface details displayed: Configured from console by console
- Timestamp displayed: 10.06.2026 5:18:42.780 AM
- Timezone displayed, if any: None

### Status and Reason

[Verified]

The status is verified because the device produced a log that was sent and collected by the centralized server

### Evidence

- [Generating action and CLI output](../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_config_change_20261025.PNG)
- [Centralized log entry](../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_syslog_recieved_20261025.PNG)

### Limitations / Follow-up

N/A

### Restoration

Interface was restored to the administrative up state

## Supporting Devices

| Device | Role | Direct logging verification applicability | Reason |
|---|---|---|---|
| PC-USER-01 | User PC | N/A | Not intended to forward Syslog directly |
| PC-USER-02 | User PC | N/A | Not intended to forward Syslog directly |
| PC-USER-03 | User PC | N/A | Not intended to forward Syslog directly |
| PC-USER-04 | User PC | N/A | Not intended to forward Syslog directly |
| PC-ADMIN-01 | Admin PC | N/A | Not intended to forward Syslog directly |
| PC-ADMIN-02 | Admin PC | N/A | Not intended to forward Syslog directly |
| PC-ADMIN-03 | Admin PC | N/A | Not intended to forward Syslog directly |
| PC-ADMIN-04 | Admin PC | N/A | Not intended to forward Syslog directly |
| SRV-SYSLOG | Centralized Log Collector | Collects forwarded syslogs | Central logging server that holds the forwarded logs from various devices |
| SRV-NTP | Time Synchronization Server | N/A | Not intended to forward Syslog directly |
| SRV-APP-01 | Application/File Server | N/A | Not intended to forward Syslog directly |
| SRV-APP-02 | Application/File Server | N/A | Not intended to forward Syslog directly |

## Overall Results

- Direct sources verified: 7
- Sources partially verified: 0
- Sources unverified: 0
- Unsupported sources: 0
- Supporting devices marked N/A:
- Outstanding gaps and follow-up actions: N/A

## Peer Review

- Reviewer:
- Review date:
- Review record: [Link]
- Outcome:
