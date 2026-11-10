# SCRUM-46 Representative Event Preparation Report

**Project:** NJIT CYBEROPS-07 Capstone  
**Prepared by:** Eduardo Ulloa Acosta  
**Sprint:** Sprint 3 - Analysis  
**Parent issue:** SCRUM-46 - Prepare representative events for manual correlation  
**Related subtasks:** SCRUM-159, SCRUM-160, SCRUM-161, SCRUM-162  
**Prepared:** November 6, 2026  
**Status:** Teammate review and evidence confirmation reported complete; detailed review record, timestamp findings, classification alignment, and publication record remain to be documented.

## Purpose and status

This report prepares a small event set for Sprint 4 manual correlation. It preserves timestamps as written in the source records and flags uncertainty instead of normalizing time or claiming a causal sequence. The Jira screenshots show subtasks for selecting events, verifying event fields, documenting timestamp considerations, and peer-reviewing/publishing the set. The project contributor reports teammate review and evidence confirmation complete. Reviewer details/results for this prepared set and its final publication location are not recorded in the latest repository.

## Candidate event set

The following five observed records provide multiple event types and two source devices. Their original IDs are retained. Selection reasons: EVT-06 provides an availability transition; EVT-07 a configuration change; EVT-08 authentication activity; EVT-09 a port-security enforcement action; and EVT-12 a second-device topology-protection event. This is a proposed representative set, not an established incident sequence.

| Event | Source and original timestamp | Recorded event / classification | Evidence and limitations |
|---|---|---|---|
| EVT-06 | SW-DIST-01, 10.20.50.1; October 6, 05:31:01.3131 down and 05:31:04.3131 up | Fa0/1 state transition; availability; author-assigned Low to Medium; Correlate | Event record contains action and log text. It documents a deliberate shutdown/no shutdown. Time zone and clock offset are not stated. |
| EVT-07 | SW-DIST-01, 10.20.50.1; October 6, 05:21:50.2121 | VLAN 999 configuration; integrity; author-assigned Medium; Correlate | The event-specific screenshot shows VLAN 999 creation and central Syslog source 10.20.50.1. Confirm authorization and baseline comparison; the generic Syslog message alone does not show commands. |
| EVT-08 | SW-DIST-01, 10.20.50.1; record gives approximately 05:25; embedded message states `10:09:19 UTC Tue Oct 6 2026` | Authentication failure for user `1`; author-assigned Medium; Correlate / Monitor | The record's approximate time and embedded message time differ. Preserve both; do not align without confirming clock, time zone, and source run. |
| EVT-09 | SW-DIST-01, 10.20.50.1; October 6, 05:55:53.5555 | Port-security violation on Fa0/10; offending MAC `0030.A314.C145`; error-disable; author-assigned High; Immediate action | Screenshots now confirm central receipt, Secure-shutdown, violation count 1, and last source MAC. Collector shows 05:55:53.272 versus local 05:55:53.5555; preserve both. MAC does not identify a person or prove intent. |
| EVT-12 | SW-ACC-01, 10.20.99.11; observed timestamp `10.06.2026 01:22:52.919 PM`; execution date October 30, 2026 | STP VLAN inconsistency on Fa0/24; Syslog severity 2. Original record classification pending; new SCRUM-41 taxonomy assigns Medium / Correlate; SCRUM-42 assigns High and SCRUM-43 Tier 3 / Immediate Action; alignment required | Record links switch action and central Syslog evidence. Execution date and observed timestamp differ; time zone/clock offset are unknown. EVT-11 shares the same controlled mismatch test. |

### Timestamp handling

- The event record set uses mixed timestamp styles, including Packet Tracer device time, an explicit UTC message, approximate times, and a numeric date string.
- No verified time zone, offset, or per-device clock-skew measurements were supplied for these selected records.
- Keep the original timestamp in any workbook. Add a separate normalized-time field only after the time zone and clock offset are verified, and document the conversion method.
- These entries are not asserted to form one incident or a causal chain. In particular, the record dates/times do not yet support a reliable cross-source sequence.

## Readiness by SCRUM-46 subtask

| Subtask | Work evidenced so far | Remaining item |
|---|---|---|
| SCRUM-159 - Select representative events | Five observed records selected with reasons above, multiple event types, and two devices. | Review reported complete; record reviewer/date, selected-set confirmation and findings. |
| SCRUM-160 - Verify sources, timestamps, classifications, and evidence | Original fields and discrepancies preserved; current classification/response documents and EVT-07/09 screenshots are available. | Evidence confirmation reported complete; record how device/timestamp discrepancies were resolved and identify approval/version. |
| SCRUM-161 - Document timestamp-correlation considerations | Timestamp caveats and no-unsupported-sequence rule documented. | Add actual clock-skew demonstration findings if the SCRUM-39 results are available. They were not in the materials reviewed. |
| SCRUM-162 - Peer-review and publish | Contributor reports completed teammate review. Related EVT-09/04 walkthrough remains documented in SCRUM-43. | Add reviewer/date, findings, corrections and final repository path/link for this set; these details are not recorded in the reviewed repository. |

## Current classification and evidence references

The standalone SCRUM-41 taxonomy is now available. It assigns EVT-06 Low / Correlate, EVT-07 Medium / Correlate, EVT-08 Medium / Correlate or Monitor, EVT-09 High / Immediate action, and EVT-12 Medium / Correlate. Original record values above are preserved.

SCRUM-42 and SCRUM-43 agree for EVT-07/08/09, but SCRUM-42 gives EVT-06 Low to Medium and EVT-12 High; SCRUM-43 uses Log Only for scheduled EVT-06 resets and Tier 3 / Immediate Action for EVT-12 blocking. Record the contextual rules or corrections that reconcile these values. The taxonomy structure is Draft with blank reviewer fields; publication does not establish final approval.

EVT-06 through EVT-09 trace to the SCRUM-168 record; EVT-12 to its individual catalogue entry. The taxonomy now supplies evidence links for EVT-06 and EVT-08, added below. EVT-09/04 walkthrough results do not by themselves document review of this complete prepared set.

## Overall outcome

**Teammate review and evidence confirmation reported complete; documentation still needs finalization.** Record the actual review details and confirmation findings. The latest repository still has no located SCRUM-39 clock-skew result or verified offsets for this set. Preserve original timestamps, leave normalized times unset, and avoid a cross-source incident sequence until timing evidence supports it.

## Source references

Links pin the reviewed GitHub revision.

- [SCRUM-42 triage procedure and classification framework](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Documentations/Taxonomy_Triage/SCRUM-42_security_event_triage_procedure_master_correlation_matrix.md)
- [SCRUM-43 escalation matrix and walkthrough](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Documentations/Taxonomy_Triage/SCRUM-43_deliverable_d4_security_event_escalation_matrix.md)
- [EVT-01 source record](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/Event_Catalogue/EVT01_State_Flap)
- [EVT-03 source record](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/Event_Catalogue/EVT03_Authentication_Failure)
- [EVT-06 through EVT-10 source records](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/Event_Catalogue/scrum168_event_records%20%281%29.md)
- [EVT-12 source record](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/Event_Catalogue/event_evt_12_stp_vlan_port_blocking_20261030.md)
- [EVT-07 VLAN creation screenshot](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/network_evidence/EVT-07_SW-DIST-01_vlan_creation.png)
- [EVT-09 Syslog and CLI screenshot](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/network_evidence/EVT-09_SW-DIST-01_port_security_violation_1.png)
- [EVT-09 port-security verification screenshot](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/network_evidence/EVT-09_SW-DIST-01_port_security_violation_2.png)

- [SCRUM-41 event taxonomy](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Documentations/Taxonomy_Triage/event_taxonomy.md)
- [Taxonomy structure and draft review fields](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Documentations/Taxonomy_Triage/taxonomy_structure.md)

- [EVT-06 action and Syslog screenshot](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/network_evidence/EVT-06_SW-DIST-01_interface_state_change.png)
- [EVT-08 authentication failure screenshot](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/network_evidence/EVT-08_SW-DIST-01_auth_failure.png)
- [EVT-08 authentication log screenshot](https://github.com/hdag-e/CyberOps-Team-7/blob/619b30bbad7789d98da4c182aafee1b11bd19751/Evidence/Sprint_3/network_evidence/EVT-08_SW-DIST-01_auth_log.png)

## Group review record

Complete this section with the actual review findings. Use Not assessed or Unknown where appropriate. Preserve original timestamps when recording any correction.

**Reviewer name:** ____________________________________

**Review date:** ______________________________________

**Event set and document version reviewed:** ________________________

**Selected events suitable for Sprint 4 correlation:** Yes / No / Explain: ____________________