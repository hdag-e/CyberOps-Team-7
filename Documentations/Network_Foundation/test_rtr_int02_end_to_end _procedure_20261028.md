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
 -  Event catalogue ID: TBD
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

- Event ID and name.
- Contributor, Jira issue, and test date/time.
- Source device and Packet Tracer file/version.
- Evidence status: Observed, only after successful execution.
- Generating action.
- Actual centralized log and evidence links.
- Credible benign explanation.
- Credible malicious explanation.
- Evidence needed to distinguish those explanations.
- Classification using the team's taxonomy.
- Limitations of the observed log.

## 9. Expected Event

The shutdown event reaches the collector and is displayed with time stamp marking the date and time. The message will also be able to be matched to the source device with the IP address stored in the syslog. Finally the log will have a message containing the interface changed message with severity, interface changed, and state changed to.

## 10. Planned Evidence

- initial state and NTP/clock output
- Generating commands and local event output
- Matching centralized log with CLI output
- Completed event catalogue record
- Confirmation of restoration to original state
