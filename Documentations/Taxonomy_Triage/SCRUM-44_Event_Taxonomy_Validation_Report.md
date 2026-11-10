# SCRUM 44 Event Taxonomy and Triage Validation Report

**Project:** NJIT CYBEROPS-07 Capstone  
**Prepared by:** Eduardo Ulloa Acosta  
**Sprint:** Sprint 3 - Analysis  
**Parent:** SCRUM-44  
**Subtasks:** SCRUM-151, SCRUM-152, SCRUM-153, SCRUM-154  
**Updated:** November 6, 2026  
**Outcome:** Review and evidence confirmation reported complete by the project contributor; repository review records and cross-document alignment remain incomplete.

## Review basis

The repository now contains the SCRUM-41 event taxonomy and taxonomy structure, SCRUM-42 triage procedure, and SCRUM-43 escalation matrix. The project contributor has confirmed that teammate review and evidence confirmation are complete. This report records that confirmation separately from results actually documented in GitHub. Reviewer identity/date, per-case results, and resolution details for that completed review are not yet fully recorded in the repository. Formal approval is not established by upload alone.

The standalone taxonomy is attributed to Eric Lindemulder and dated November 5, 2026. Its reviewer/date fields are blank; the structure document remains marked Draft. This report covers EVT-01, EVT-03, EVT-07, EVT-09, and EVT-12.

## Original observations and evidence

| Event | Original evidence | Remaining limitation |
|---|---|---|
| EVT-01 | Record: RTR-INT-01, 10.20.50.1, GigabitEthernet0/0/1 shutdown/no shutdown, dated October 30. Captures: FastEthernet0/1 down/up from 10.20.50.1 on October 6. | Direct screenshot links are now included in the source record. Date/interface differences and device-to-IP mapping remain unresolved in the written record. The new matrix repeats the IP; it does not resolve the conflict with inventory. |
| EVT-03 | Record: RTR-INT-01, 10.20.99.2, failed admin authentication with %SEC_LOGIN-5-LOGIN_FAILED. Central Syslog and CLI captures are available. | Source record now includes direct CLI and Syslog evidence links. CLI capture lacks device/time metadata; some console messages show source 0.0.0.0/localport 0. Record date differs from log date. Current framework identifies EVT-03 as authentication failure; older configuration-mode guidance needs reconciliation. |
| EVT-07 | Screenshot shows SW-DIST-01 creating VLAN 999 named SUSPICIOUS_MGMT_TEMP, followed by CONFIG_I at October 6, 05:21:50.2121. Central Syslog pane shows source 10.20.50.1. | This resolves the missing action/source evidence. Authorization and baseline configuration comparison remain unconfirmed; CONFIG_I alone does not record commands. |
| EVT-09 | Screenshots show Fa0/10 port-security violation for 0030.A314.C145, central receipt, Secure-shutdown, violation count 1, and configured allowed MAC 1111.2222.3333. | Missing screenshot/interface-output gap is resolved. Local timestamp 05:55:53.5555 and collector 05:55:53.272 differ; no clock correction is established. MAC alone does not identify a person or establish intent. |
| EVT-12 | SW-ACC-01, 10.20.99.11, Fa0/24, %SPANTREE-2-BLOCK_PVID_LOCAL; original observed timestamp 10.06.2026 01:22:52.919 PM; action and central Syslog evidence linked in source record. | Execution date October 30 differs from displayed log date; time zone/offset unverified. EVT-11 and EVT-12 share the same controlled mismatch test. |

## Expected results and document differences

Use the standalone taxonomy for its recorded classification and compare it with the procedure/matrix. The differences below need a documented team decision before one approved expected answer can be assigned. These are document values, not new teammate observations.

| Event | SCRUM-41 taxonomy | SCRUM-42 procedure and SCRUM-43 matrix comparison |
|---|---|---|
| EVT-01 | Medium; Availability; Correlate | Procedure: Low to Medium. Matrix: Tier 1 for one authorized flap; Tier 2 for more than 3 flaps in 5 minutes on a core link. Record which context determines the accepted classification. |
| EVT-03 | Low; Confidentiality/Integrity; Correlate | Procedure: Medium. Matrix: fewer than 3 failures Tier 1; at least 5 rapid failures from one IP Tier 3. Clarify severity difference, treatment of 3-4 failures, and the time window for rapid. |
| EVT-07 | Medium; Integrity; Correlate | Aligned with procedure Medium and matrix Tier 2 for unapproved VLAN creation. Check configuration baseline and authorization. |
| EVT-09 | High; Integrity/Availability; Immediate action | Aligned with procedure High and matrix Tier 3 for unknown MAC causing err-disable. Verify inventory and port-security state. |
| EVT-12 | Medium; Integrity/Availability; Correlate; High conditional on significant impact | Procedure: High. Matrix: Tier 3 / Immediate Action for mismatch blocking. Reconcile impact/context requirements before final expected result is approved. |

## Independent teammate results

**Completion confirmation:** The project contributor reports that teammate review and evidence confirmation are complete. The table tracks repository documentation of the results, not whether the review took place.


SCRUM-43 section 4 identifies Eric Lindemulder / Access Switch Lead as the validating teammate and reports a passed walkthrough for EVT-09: technical severity 2 (Critical), err-disable condition recognized, and Tier 3 / Immediate Action selected. It also records an EVT-04 simulator-limitation walkthrough. EVT-04 is outside this five-event set.

SCRUM-42 also reports a walkthrough for EVT-09 and EVT-04, but identifies the reviewer only as Non-Author Peer Analyst and gives November 2026 as the date. These are related source-reported walkthroughs. Eric is also the named author of the newly uploaded taxonomy, so these walkthroughs alone do not establish non-author validation of that taxonomy. Record who performed the completed SCRUM-44 review and their authorship relationship.

| Event | Documented teammate result | SCRUM-152 status |
|---|---|---|
| EVT-01 | Case-specific result not recorded in reviewed repository | Review reported complete; result details to be recorded |
| EVT-03 | Case-specific result not recorded in reviewed repository | Review reported complete; result details to be recorded |
| EVT-07 | Case-specific result not recorded in reviewed repository | Review reported complete; result details to be recorded |
| EVT-09 | SCRUM-43 reports Eric selected Tier 3 / Immediate Action and passed. This agrees with the current matrix. | Related result documented; add review date, scope and evidence reference. Confirm the SCRUM-44 validator did not author the taxonomy/triage materials. |
| EVT-12 | Case-specific result not recorded in reviewed repository | Review reported complete; result details to be recorded |

## Findings and subtask documentation

- SCRUM-151: Five cases selected and source links available. Reconcile the SCRUM-41 versus SCRUM-42/43 differences above before approving one expected result per event.
- SCRUM-152: Review is reported complete. Add reviewer name/date, non-authorship confirmation, evidence used, and actual classification, triage, escalation, and expected-versus-observed comparison for each case. Retain the documented EVT-09 walkthrough with its source attribution.
- SCRUM-153: Record how the completed review addressed taxonomy/procedure conflicts and login thresholds, then link the revised versions and reviewer recheck. Do not invent the corrections or outcome.
- SCRUM-154: Add the final review record, approved versions and final report repository location. The latest repository does not contain a complete SCRUM-44 validation record.
- Evidence confirmation is reported complete. Document its resolution of EVT-01's device/IP/interface/date differences, EVT-03's attribution/date differences, and EVT-07's authorization. Existing written discrepancies remain visible until a correction or explanation is recorded.

**Outcome:** Review and evidence confirmation reported complete; final documentation and cross-document reconciliation still required. No new per-event pass/fail results or approvals have been inferred.

## Source references

Links below pin the reviewed GitHub revision so the basis of this report can be reproduced.

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

## Group review record

Complete this section with the actual review results. Use Not assessed where a check was not performed. Leave the outcome unsigned until the review record is complete.

**Reviewer name:** ____________________________________

**Review date:** ______________________________________

**Documents and versions reviewed:** ______________________________

**Reviewer did not author the taxonomy or triage materials:** Yes / No / Explain: ____________________

**Procedure followed without undocumented guidance:** Yes / No / Explain: ____________________