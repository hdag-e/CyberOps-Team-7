# SCRUM-54 · Incident 3 Reconstruction

**NJIT CYBEROPS-07 · Team 7 · Sprint 4**  
**Analyst** — Eduardo Ulloa Acosta  
**Updated** — November 18, 2026  
**Status** — Preliminary reconstruction from the published Syslog export. Validation pending.

## Summary

The export records a port-security violation and interface state changes on SW-ACC-01, followed by failed SSH authentication, a successful authentication event of unverified origin, and VLAN 30 interface state changes on SW-DIST-01. The logs confirm that port security placed Fa0/6 into err-disable and that the VLAN 30 interface was later reported administratively down. The records leave endpoint identity, the relationship between the events across switches, and end-to-end service impact unresolved. [Incident 3 Syslog export](https://github.com/hdag-e/CyberOps-Team-7/blob/4f01842/Evidence/Sprint_4/incident_logs/Incident%203.md)

## Evidence and timeline

The source inventory maps 10.20.99.11 to SW-ACC-01 and 10.20.50.1 to SW-DIST-01. The companion CSV preserves all 15 messages, timestamps as shown, any embedded UTC timestamp, and direct links to the raw log lines. INC3 identifiers are local worksheet references. The exact Sprint 3 catalogue matches and incident-specific clock offsets are pending verification. [Monitoring source inventory](https://github.com/hdag-e/CyberOps-Team-7/blob/4f01842/Documentations/Network_Foundation/Monitoring_Source_inventroy.md) · [Sprint 3 event catalogue](https://github.com/hdag-e/CyberOps-Team-7/tree/4f01842/Evidence/Sprint_3/Event_Catalogue)

| Time shown on 10.06.2026 | Rows | Observed activity |
| --- | --- | --- |
| 01:36:38.216 PM | INC3-01–06 | SW-ACC-01 records a port-security violation for MAC 0001.6350.4CCD on Fa0/6 and explicitly reports err-disable due to that violation. The same timestamp appears on the line-protocol down, administratively down, line-protocol up and link up messages. Their exact order within the timestamp remains uncertain. [Logs](https://github.com/hdag-e/CyberOps-Team-7/blob/4f01842/Evidence/Sprint_4/incident_logs/Incident%203.md#L1-L10) |
| 01:40:50.771 PM and 01:42:16.953 PM | INC3-07–09 | SW-ACC-01 records a console configuration event and later reports that both Fa0/6 and its line protocol are up. The configuration entry leaves the command and its relationship to the port state unverified. [Logs](https://github.com/hdag-e/CyberOps-Team-7/blob/4f01842/Evidence/Sprint_4/incident_logs/Incident%203.md#L14-L18) |
| 01:42:47.538–01:42:49.859 PM | INC3-10–12 | Two SW-DIST-01 messages log failed SSH authentication for admin from 192.168.50.10 on local port 22. A successful admin login message follows with source 0.0.0.0 and local port 0. The source and port fields do not establish a link to the SSH failures. [Logs](https://github.com/hdag-e/CyberOps-Team-7/blob/4f01842/Evidence/Sprint_4/incident_logs/Incident%203.md#L22-L24) |
| 01:46:18.308 PM and 01:46:20.395 PM | INC3-13–15 | SW-DIST-01 reports VLAN 30 administratively down and its line protocol down, then records a generic console configuration message. The export leaves the responsible action, operator, and service impact unverified. [Logs](https://github.com/hdag-e/CyberOps-Team-7/blob/4f01842/Evidence/Sprint_4/incident_logs/Incident%203.md#L25-L29) |

**Earliest evidence in the supplied export** — The Fa0/6 event group at 01:36:38.216 PM. The port-security entry appears first in the export. The shared timestamp limits ordering within the group.

## Timestamp assessment

The export displays `10.06.2026`. The three authentication messages explicitly embed Tuesday, October 6, 2026 UTC and align with the displayed clock to the second. This does not establish the time zone for every exported entry or verify synchronization across switches. The report orders rows by the times shown and leaves normalized timestamps blank. Exact cross-device timing requires clock or NTP evidence for this run. [Sprint 3 clock-skew guidance](https://github.com/hdag-e/CyberOps-Team-7/blob/4f01842/Documentations/Clock_Skew/epic39_45-controlled_clock_skew-documentation.md)

## Findings and response

- **Verified relationship.** The err-disable message explicitly attributes the Fa0/6 state to the port-security violation. The later up messages confirm a reported up state. Recovery steps and connectivity after that change remain unverified.
- **Endpoint and login correlation.** The export supplies a MAC for the violation and an IP for the failed SSH attempts. An endpoint record or MAC-to-IP evidence is needed to link them. The successful login has different source and port fields, and its association with the failed attempts is unresolved.
- **VLAN 30 impact.** The observed effect is a down VLAN interface and line protocol. Service reachability, outage duration, and any recovery require additional evidence. Operator actions, command details, and results beyond the logged state are pending.

## Evidence review

Reviewed the published Incident 3 Syslog export on November 19, 2026. The timestamps and reported events matched the draft timeline. No timeline changes were needed. This check covered the Syslog export. [Incident 3 Syslog export](https://github.com/hdag-e/CyberOps-Team-7/blob/4f01842/Evidence/Sprint_4/incident_logs/Incident%203.md)

## Completion and handoff

| Work item | Status |
| --- | --- |
| Evidence intake | Syslog export linked and inventoried. Completed Incident 3 Packet Tracer file, available device or endpoint captures, and controller record remain to be collected. |
| Event worksheet and timeline | Fifteen source messages recorded and grouped into a preliminary timeline. Check event catalogue mappings and verify clock basis when supporting records arrive. |
| Reconstruction findings | Preliminary conclusions documented. Device state, endpoint correlation, and service impact remain open where the export leaves gaps. |
| Team workbook | Companion CSV ready for import. Hussein’s SCRUM-48 methodology and workbook were not located on GitHub main at 4f01842. The official workbook entry remains pending. |
| Controller comparison and peer review | Compare the analysis with the staging record once available and record differences. Send the completed reconstruction to Hasan for the separate SCRUM-200 review. |
| Final submission | Publish the reconciled report, workbook entries, and supporting evidence links in the team repository. Live SCRUM-54 subtask IDs, criteria, and completion statuses remain unverified. |

Suggested report location is `Documentations/Correlation/Incidents/`. Keep the original evidence link attached to the final reconstruction.
