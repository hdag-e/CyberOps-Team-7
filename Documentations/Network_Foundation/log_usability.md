# Log Usability Assessment and Monitoring-Gap Register

## 1. Document Information

- Contributor: Eric Lindemulder
- Assessment date: 10/26/2026
- Parent Jira issue: [SCRUM-33](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-33)
- Child Jira issue: [SCRUM-112](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-112)
- Packet Tracer version: 9.0.1.0858
- Packet Tracer project file: [CYBEROPS07_Configuration_v1_2.pkt](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Packet_Tracer/Configurations/CYBEROPS07_Configuration_v1_2.pkt)
- Central logging destination: 10.20.50.10
- Monitoring inventory: [Inventory](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Documentations/Network_Foundation/Monitoring_Source_inventroy.md)
- Verification results: [Verification](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Documentations/Network_Foundation/Source_logging_verification.md)
- Initial event records: not yet available

## 2. Purpose and Scope

Assess whether collected centralized logs contain sufficient
information for event classification, triage, timestamp analysis,
and manual correlation.

This assessment covers only the sources and event types examined.
Successful delivery does not establish complete monitoring coverage.

## 3. Evidence Reviewed

| Evidence ID | Source device | Event type | Screenshot / log link |
|---|---|---|---|
| EVID-01 | RTR-EDGE-01 | Interface State Change |  [Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_interface_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_syslog_recieved_20261025.PNG)|
|EVID-02| RTR-INT-01 |Interface State Change | [Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_interface_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_syslog_recieved_20261025.PNG)|
|EVID-03| RTR-INT-02 | Interface State Change |[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_interface_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_syslog_recieved_20261025.PNG)|
|EVID-04 |SW-DIST-01 | Configuration Change |[Switch CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_syslog_recieved_20261025.PNG)|
|EVID-05|SW-ACC-01|Configuration Change|[Switch CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_syslog_recieved_20261025.PNG)|
|EVID-06|SW-ACC-02|Configuration Change|[Switch CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_syslog_recieved_20261025.PNG)|
|EVID-07|SW-ACC-03|Configuration Change|[Switch CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_syslog_recieved_20261025.PNG)|

## 4. Log Information Assessment

Record fields as they appear at the central collector.
Use "Not shown", "Unclear", or "Not assessed" where appropriate.

| Source / event type | Source identifier displayed | Event code / severity | Event details available | Missing or ambiguous details | Evidence |
|---|---|---|---|---|---|
|RTR-EDGE-01 - interface state change | IP source - 10.20.252.1 | 5 - changed, 3 - updown| %LINK-5-CHANGED: Interface GigabitEthernet0/0/2, changed state to administratively down, %LINK-3-UPDOWN: Interface GigabitEthernet0/0/2, changed state to down | Why the interface state was changed |[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_interface_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_syslog_recieved_20261025.PNG) |
|RTR-INT-01 - interface state change | IP source - 10.20.252.9 | 3 - updown |%LINK-3-UPDOWN: Interface GigabitEthernet0/0/2, changed state to down|Why the interface state was changed|[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_interface_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_syslog_recieved_20261025.PNG)|
|RTR-INT-02 - interface state change |IP source - 10.20.252.13 | 5 - changed, 3 - updown|%LINK-5-CHANGED: Interface GigabitEthernet0/0/2, changed state to administratively down, %LINK-3-UPDOWN: Interface GigabitEthernet0/0/2, changed state to down|Why the interface state was changed|[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_interface_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_syslog_recieved_20261025.PNG)|
|SW-DIST-01 - Configuration change|IP source - 10.20.50.1| 5 - system config|%SYS-5-CONFIG_I: Configured from console by console | What changed in the config and why it was changed | [Switch CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_syslog_recieved_20261025.PNG)|
|SW-ACC-01 - Configuration change|IP source - 10.20.99.11| 5 - system config|%SYS-5-CONFIG_I: Configured from console by console|What changed in the config and why it was changed|[Switch CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_syslog_recieved_20261025.PNG)|
|SW-ACC-02 - Configuration change|IP source - 10.20.99.12| 5 - system config|%SYS-5-CONFIG_I: Configured from console by console|What changed in the config and why it was changed|[Switch CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_syslog_recieved_20261025.PNG)|
|SW-ACC-03 - Configuration change|IP source - 10.20.99.13| 5 - system config|%SYS-5-CONFIG_I: Configured from console by console|What changed in the config and why it was changed|[Switch CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_syslog_recieved_20261025.PNG)|

## 5. Timestamp Assessment

| Source / event type | Date/time displayed | Year / timezone shown? | Fractional seconds shown? | Clock accuracy / synchronization evidence | Usability and limitations | Evidence |
|---|---|---|---|---|---|---|
|RTR-EDGE-01 - interface state change | 10.06.2026 05:11:46.225 AM | 2026 / No timezone shown | Yes |Times match between the CLI output and the syslog server log / Device reports "Clock is synchronized" to NTP server 10.20.50.20| Timestamp is usable only limitation is no timezone is shown | [Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_interface_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_syslog_recieved_20261025.PNG), [NTP Status Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_edge_01_ntp_status_20261026.PNG)| 
|RTR-INT-01 - interface state change|10.06.2026 05:14:07.900 AM|2026 / No timezone shown|Yes|Times match between the CLI output and the syslog server log / Device reports "Clock is synchronized" to NTP server 10.20.50.20|Timestamp is usable only limitation is no timezone is shown|[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_interface_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_syslog_recieved_20261025.PNG), [NTP Status Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_01_ntp_status_20261026.PNG)|
|RTR-INT-02 - interface state change|10.06.2026 05:21:04.650 AM|2026 / No timezone shown|Yes|Times match between the CLI output and the syslog server log / Device reports "Clock is synchronized" to NTP server 10.20.50.20|Timestamp is usable only limitation is no timezone is shown|[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_interface_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_syslog_recieved_20261025.PNG), [NTP Status Output](../../Evidence/Sprint_2/baseline_verification/test_rtr_int_02_ntp_status_20261026.PNG)|
|SW-DIST-01 - Configuration change|10.06.2026 05:06:00.941 AM| 2026 / No timezone shown|Yes|Times match between the CLI output and the syslog server log / Device reports "Clock is synchronized" to NTP server 10.20.50.20|Timestamp is usable only limitation is no timezone is shown|[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_syslog_recieved_20261025.PNG), [NTP Status Output](../../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_ntp_status_20261026.PNG)|
|SW-ACC-01 - Configuration change|10.06.2026 05:11:15.218 AM | 2026 / No timezone shown|Yes|Times match between the CLI output and the syslog server log / Device reports "Clock is synchronized" to NTP server 10.20.50.20|Timestamp is usable only limitation is no timezone is shown|[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_syslog_recieved_20261025.PNG), [NTP Status Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_01_ntp_status_20261026.PNG)|
|SW-ACC-02 - Configuration change|10.06.2026 05:17:02.203 AM | 2026 / No timezone shown|Yes|Times match between the CLI output and the syslog server log / Device reports "Clock is synchronized" to NTP server 10.20.50.20|Timestamp is usable only limitation is no timezone is shown|[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_syslog_recieved_20261025.PNG), [NTP Status Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_02_ntp_status_20261026.PNG)|
|SW-ACC-03 - Configuration change|10.06.2026 05:18:42.780 AM | 2026 / No timezone shown|Yes|Times match between the CLI output and the syslog server log / Device reports "Clock is synchronized" to NTP server 10.20.50.20|Timestamp is usable only limitation is no timezone is shown|[Router CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_syslog_recieved_20261025.PNG), [NTP Status Output](../../Evidence/Sprint_2/baseline_verification/test_sw_acc_03_ntp_status_20261026.PNG)|
### Timestamp Interpretation

- Is the displayed time identified as event time or collector receipt time? Displayed time is the collector receipt time however the event time is shown in the CLI Output evidence.
- Can events from the same device be placed in order? Yes with the timestamp and IP address
- Is reliable ordering across devices established? Yes ordering can be done by timestamp device IP or message
- Are any timestamps missing, inconsistent, or ambiguous? There is an inconsistency between some timestamps when testing switches vs the routers. This is because the packet tracer file was closed and restarted without saving causing the time to reset to earlier. Overall there are no major inconsistencies.

## 6. Analytical Usability

| Intended use | What the reviewed logs support | Limitations / additional evidence needed |
|---|---|---|
| Event classification | Message codes and descriptions distinguish the interface-state changes from configuration changes. Severity numbers are displayed | The events cover only observed event types. Severity number does not identify if the activity is malicious or not|
| Triage | Source identifiers and event description help to identify the event and the affected device| Logs do not establish if the changes were authorized, why the changes took place, or in the case of configuration changes what specifically was changed. Administrative context is needed|
| Timestamp analysis | Displayed timestamps allow for comparison of recorded events. NTP status confirms synchronization on all 7 of the tested devices that were individually checked | Timezone is missing from timestamp, NTP server is not updated to current date and time|
| Manual correlation | Source identifiers, timestamps, and event details can be combined into a basic timeline across the reviewed logs. | Closely spaced events may require additional evidence to establish their exact order as the time between CLI output and syslog collector vary slightly.|

## 7. Monitoring-Gap Register

Assign sequential gap IDs: GAP-01, GAP-02, etc.

| Gap ID | Affected source / event type | Observed gap | Impact on analysis | Cause assessment | Supporting evidence | Follow-up / owner | Status |
|---|---|---|---|---|---|---|---|
| GAP-01 | Tested switches/interface-state changes|No interface-state messages observed during unused-port shutdown/no shutdown tests | Those actions do not appear in the centralized logs | Cause Unconfirmed | [Switch CLI Output](../../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_config_change_20261025.PNG), [Central Syslog Entry](../../Evidence/Sprint_2/baseline_verification/test_sw_dist_01_syslog_recieved_20261025.PNG)|Investigate with a connected port test / Hussein Harb| Open |
| GAP-02 | Source producing configuration change logs|Messages do not report what was changed in the configuration only that something was changed.| Cannot determine what was changed in configuration from the configuration messages| Cause unconfirmed: detail absent from reviewed messages| [Central Syslog Entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_2/baseline_verification/test_syslog_server_config_message_20261026.PNG)|Compare exported configurations and configuration logs / Hussein Harb | Open | 
### Cause Assessment Labels

- Confirmed configuration problem
- Confirmed Packet Tracer limitation
- Suspected Packet Tracer limitation
- Cause unconfirmed


### Status Labels

- Open
- Investigating
- Resolved — correction and retest evidence linked
- Accepted limitation — acceptance decision linked


## 8. Untested or Unavailable Event Types

| Source / event type | Status | Basis / evidence | Planned follow-up |
|---|---|---|---|
| Devices intended to enforce ACLs / access-denial events | Not tested; configuration dependency | Previously reviewed configurations did not show ACL logging | Confirm the approved implementation and test when configured |
| Access switches / port-security violations | Not tested; configuration dependency | Previously reviewed access-switch configuration did not show port security | Confirm the approved implementation and test when configured |
| Tested switches / interface-state changes | Tested but not observed | No corresponding centralized messages appeared during unused-port tests | Clarify scope and investigate if required |


Distinguish:
- Not tested
- Tested but not observed
- Confirmed unsupported
- Outside approved scope

## 9. Overall Assessment

### What the Logs Currently Support

Currently the logs show that a baseline centralized logging is working as well as a synchronization to the NTP server.

### Important Limitations

No interface change messages from the access switches (GAP-01). No specific messages about configuration changes just messages that the config has changed (GAP-02).

## 10. Review Record

- Review status: Pending
- Reviewer:
- Review date:
- Review evidence:
- Findings / corrections:
