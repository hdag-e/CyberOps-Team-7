## 1. Test Information

 - Contributor: Eric Lindemulder
 -  Date Prepared: 10/28/2026
 -  Parent Jira issue: [SCRUM-36](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-36)
 -  Child Jira issue: [SCRUM-122](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-122)
 -  Packet Tracer Version: 9.0.1.0858
 -  Project file: [CYBEROPS07_Configuration_v1_2.pkt](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Packet_Tracer/Configurations/CYBEROPS07_Configuration_v1_2.pkt)
 -  Source: RTR-INT-92
 -  Interface: GigabitEthernet 0/0/2
 -  Event: Interface state change to administratively shut down
 -  Event catalogue ID: EVT-04
 -  Related event record: not yet available
 -  Central logging destination: 10.20.50.10

## 2. Objective

Verify that a deliberately generated interface shutdown produces an identifiable centralized log and can be documented using the team's event catalogue structure.

## 3. Preconditions

- G0/0/2 is unused and is not part of the logging path
- record the interfaces initial state
- centralized logging is configured
- check NTP synchronization and record the device's clock
- Identify the source IP expected in the collector's logs

## 4. Planned test steps

1. Capture the initial state of the interface, clock, and NTP status
2. Check if there are any preexisting logs on the server
3. Record the time G0/0/2 is shutdown
4. Check the central syslog server for the matching message
5. Compare the source, timestamp, and reported state
6. Capture CLI and collector evidence

## 5. Commands

```text
show ip interface brief
show clock
show ntp status
conf t
int g0/0/2
no shutdown
shutdown
end
```

## 6. Expected centralized log

%LINK-5-CHANGED: Interface GigabitEthernet0/0/2, changed state to administratively down

This is based on previous observation during the centralized logging verification

The message will be identifiable to the RTR-INT-02 by the IP address in the syslog hostname field

## 7. Required Fields

|Field| Expected information|
|---|---|
|Source|10.20.252.13|
|Time stamp|Event date and time|
|Event code| Link-5-changed|
|Severity|5|
|Interface|GigabitEthernet0/0/2|
|Sate/action| Changed to administratively down|

## 8. Event Catalogue Fields to Validate

- Event ID and name. EVT- 04 Interface State change
- Contributor, Jira issue, and test date/time. Eric Lindemulder
- Source device and Packet Tracer file/version. RTR-INT-02, [CYBEROPS07_Configuration_v1_2.pkt](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Packet_Tracer/Configurations/CYBEROPS07_Configuration_v1_2.pkt), 9.0.1.0858
- Evidence status: Observed
- Generating action: Changing the interface state to administratively down 
- Actual centralized log and evidence links: [Router CLI Output](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_2/baseline_verification/test_rtr_int_02_endpoint_test_cli_20261028.PNG), [Syslog server](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_2/baseline_verification/test_syslog_server_endpoint_test_20261028.PNG)
- Credible benign explanation: Admin user logs into a switch and intentional shuts down  and unused interface as part of network maintenance or configuration
- Credible malicious explanation: an attacker with administrative access deliberate disabling the interface to cause disruption in the network (because the port is unused no disruption was caused)
- Evidence needed to distinguish those explanations: Admin login records and command history. Compare the account, access source, time and action
- Classification using the team's taxonomy: Team Taxonomy not yet available
- Limitations of the observed log: Log identifies the interface and the state it was changed to as well as the source it came from and the time/date. However it does not record what account changed the state or for what purpose

## 9. Expected Event

The shutdown event reaches the collector and is displayed with time stamp marking the date and time. The message will also be able to be matched to the source device with the IP address stored in the syslog. Finally the log will have a message containing the interface changed message with severity, interface changed, and state changed to.

## 10. Planned Evidence

- initial state and NTP/clock output
- Generating commands and local event output
- Matching centralized log with CLI output
- Completed event catalogue record
- Confirmation of restoration to original state

## 11. Execution Results
- Executed by: Eric Lindemulder
- Execution date/time and timezone: 10/28/2026 2:11 AM EST
- Procedure Followed / Deviations: no deviations followed the procedure as it was laid out
- Actual local output: %LINK-5-CHANGED: Interface GigabitEthernet0/0/2, changed state to administratively down
- Central received: Yes
- Source identifier displayed: IP address 10.20.252.13
- Source attribution: IP in the centralized log matching the IP of the device the event was generated on
- Timestamp Displayed: 10.28.2026 02:11:09.097 AM
- Event Code and Details: Link-5-changed GigabitEthernet 0/0/2 changed state to administratively down
- Failed steps / unexpected behavior: None
- Limitations / cause unconfirmed: None
- Original interface state restored: Yes
- Result: Pass
- Initial state evidence: [Router CLI output](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_2/baseline_verification/test_rtr_int_02_initial_state_20261028.PNG)
- Generation-action evidence: [Router CLI Output](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_2/baseline_verification/test_rtr_int_02_endpoint_test_cli_20261028.PNG)
- Centralized-log evidence: [Syslog server](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_2/baseline_verification/test_syslog_server_endpoint_test_20261028.PNG)

## 12. Final Outcome

- Outcome: passed
- Supporting reasons: log is generated and shown on the syslog server with the expected output for the event.
- Missing or ambiguous information: User or account that changed the state or reason that interface state was changed
- Explanation of differences or failures: N/A
- Follow-up actions: Update the events provisional classification once the team taxonomy is available
- Completed event catalogue entry: [Event Catalogue Entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Documentations/Event_Catalogue/event_evt04_interface_admin_shutdown_20261028.md)
- Supporting screenshots: [Initial state router CLI output](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_2/baseline_verification/test_rtr_int_02_initial_state_20261028.PNG), [Generation-action Output](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_2/baseline_verification/test_rtr_int_02_endpoint_test_cli_20261028.PNG), [Syslog server](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_2/baseline_verification/test_syslog_server_endpoint_test_20261028.PNG)
