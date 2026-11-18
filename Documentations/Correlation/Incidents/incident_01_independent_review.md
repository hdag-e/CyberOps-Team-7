# Incident #1 — Independent Reconstruction Review

- Reviewer: Eric Lindemulder
- Primary reconstruction author: Hussein Harb
- Review date: 11/18/2026
- Jira issue: [SCRUM-199](https://njit-team-lbmxd47l.atlassian.net/jira/browse/SCRUM-199)
- Sealed Syslog evidence: [Evidence](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_4/incident_logs/Incident_01_Syslog_Export.md)
- Finalized Incident #1 workbook: [Incident 1 reconstruction work sheet](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Documentations/Playbooks/Incident%201%20Reconstruction%20Workbook%20-%20Sheet1%20(1).pdf)
- Event catalogue: [Event Taxonomy](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Documentations/Taxonomy_Triage/event_taxonomy.md)

## 1. Event Traceability

For each event, add the workbook row or cell and link the catalogue entry.
Times below are the displayed Syslog timestamps for October 6, 2026.

| Time | Observed evidence | Catalogue match | Workbook reference / reviewer finding |
|---|---|---|---|
| 13:36:38.717–13:36:57.779 | Five failed SSH login entries from `10.20.10.11`: three for `secadmin` and two for `admin`. | EVT-03 — Authentication failure | Chronological order 1-2 |
| 13:37:00.238 | Successful `admin` login. Message lists `Source: 0.0.0.0` and `localport: 0`. |N/A no event for successful login | Chronological order 3] |
| 13:37:38.833–13:37:49.028 | `Gi0/0/0` was reported administratively down and then up about 10.2 seconds later. Link and line-protocol messages record the transitions. | EVT-01 — Interface State Flap | Chronological order 4-5 |
| 13:38:10.488 | `%SYS-5-CONFIG_I` reports configuration activity from the console. | EVT-02 — Global Config Change |Chronological order 6|

## 2. Timestamp and Clock-Skew Review

- Timestamp field used to order events: [Incident 1 reconstruction work sheet], chronological order, normalized timestamp. The work sheet orders the events in a chronological order using UTC time with miliseconds.
- How the author checked for or handled clock skew: the clock status / offset columns reports it was veriified with a sync to 10.20.50.10 and reported offset of 0s
- Independent check: The times shown in the workbook match those provided in however these time only come from a single device and do not verifiy time sync across the network
- Ordering limitation: Link and line-protocol messages with identical
  displayed timestamps cannot be placed in a finer order from this excerpt.

## 3. Major Conclusions and Supporting Evidence

| Workbook conclusion | Sealed Syslog evidence | Independent assessment |
|---|---|---|
| Orders 1–2: Repeated SSH failures confirm brute force. | Five failed SSH logins from `10.20.10.11` between `13:36:38.717` and `13:36:57.779`: three for `secadmin` and two for `admin`. | **Partially supported.** The repeated failures are consistent with possible password guessing, but they could be the result of someone trying to access their account these logs also do not show how is attempting access |
| Order 3: The same attacker switched from SSH to console access. | Successful `admin` login at `13:37:00.238`, with `Source: 0.0.0.0` and `localport: 0`. | **Partially supported.** does show that a successful login was confirmed however the logs to do not connect it with the previous device attempting |
| Orders 4–5: The attacker shut down and restored `Gi0/0/0`. | Link and line-protocol messages show the interface administratively down at `13:37:38.833` and up at `13:37:49.028`. | **Partially supported.** The logs do not identify why these ports change from stat up/down and why they were changed |
| Order 6: The console configuration message marked the end of the attack. | `%SYS-5-CONFIG_I` at `13:38:10.488` reports configuration activity from the console. | **Partially supported.** while it does show that a configuration took place it does not give any information about that change or who did it |

## 4. Limitations and Follow-up

- Limitations already documented by the author: Limitations are listed under the limitations / analyst notes in the work sheet
- **New gaps identified during review:**
- Orders 1-2 logs do not show who is attempting to access the account and do not explicitly confirm brute force attack
- order 3 the evidence from the syslog does not link the event to a specific device
- oders 4-5 logs do not identify why the port states were changed or by who
- order 6 logs do not give any information about the change such as who did the change or why it happened
- Orders 1-2 only shows 1 time for multiple events
- Follow-up: show different start times for each of the events in orders 1-2


## 5. Review Outcome and Handoff

- Outcome: validated
- Summary: the sealed evidence does support the conclusion of the author of the worksheet but do not 100% confirm intent or the identity of the one commiting the actions. This is more of a limitation of packet tracer and the syslog rather than that of the worksheet or incident author themselves.
- Documentation Lead: 
- Handoff date: 
- Completed review record: 
