# Security Event Taxonomy Structure

## 1. Document Information

- Contributor:Eric Lindemulder
- Date: 11/05/2026
- Jira issue:[SCRUM-41](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-41)
- Child Jira issue:[SCRUM-139](https://njit-team-lbmxd47l.atlassian.net/browse/SCRUM-139)
- Catalogue location: [Catalogue location](https://github.com/hdag-e/CyberOps-Team-7/tree/main/Evidence/Sprint_3/Event_Catalogue)
- Catalogue version / commit reviewed:
- Structure status: Draft
- Reviewer:
- Review record:

## 2. Purpose

Define a consistent structure for classifying the project's
documented security events by analytical severity, analytical
question, and response category.

The completed event catalogue is the source of truth.
Classifications must reference observed evidence and explicitly
identify uncertainty.

## 3. Catalogue Review

List every required event using its existing ID and name.
Add rows as needed.

| Event ID | Event name | Catalogue entry link | Review findings / missing information |
|---|---|---|---|
| EVT-01 | State Flap|[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/EVT01_State_Flap) | Needs links to evidence screenshots and jira issues|
| EVT-02 |Global Config | [Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/EVT02_global_config)| Needs links to evidence screenshots and jira issues|
| EVT-03 |Authentication  Failure |[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/EVT03_Authentication_Failure) | Needs links to evidence screenshots and jira issues|
| EVT-04 | ACL Deny |[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/EVT04_ACL_deny) | Needs links to evidence screenshots and jira issues|
| EVT-05 |Device Reload |[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/EVT05_device_reload) | Needs links to evidence screenshots and jira issues|
| EVT-06 |Distribution Switch Interface State Change |[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/scrum168_event_records%20(1).md) | Needs links to evidence screenshots and jira issues|
| EVT-07 | Distribution Switch Configuration Mode Entry & Unauthorized VLAN Creation|[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/scrum168_event_records%20(1).md) | Needs links to evidence screenshots and jira issues|
| EVT-08 | Log-in Authentication failure and success|[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/scrum168_event_records%20(1).md) | Needs links to evidence screenshots and jira issues|
| EVT-09 |Port Security Violation and Error-Disable Action |[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/scrum168_event_records%20(1).md) | Needs links to evidence screenshots and jira issues|
| EVT-10 | Spanning Tree BPDU Guard Violation and Port Error-Disable|[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/scrum168_event_records%20(1).md) | Needs links to evidence screenshots and jira issues|
| EVT-11 |Nataive VLAN mismatch |[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/event_evt11_native_vlan_mismatch_20261030.md) |No missing information identified |
| EVT-12 |STP VLAN-Inconsistency Port Blocking |[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/event_evt_12_stp_vlan_port_blocking_20261030.md) |No missing information identified |
| EVT-13 | Duplicate IP Address Detection | [Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/event_evt_13_duplicate_ip_detection_20261031.md) |No missing information identified |
| EVT-14 | Root Guard Blocking|[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/event_evt14_root_guard_blocking_20261101.md) | No missing information identified |
| EVT-15 | STP VLAN-Consistency Restoration|[Catalogue entry](https://github.com/hdag-e/CyberOps-Team-7/blob/main/Evidence/Sprint_3/Event_Catalogue/event_evt15_stp_consistency_restoration_20261101.md) | No missing information identified |

### Review Summary

- Required event types: 15 distinct and deliberately generated event types
- Catalogue entries reviewed: 15
- Missing or incomplete entries: events 1-11 just need links to screenshots and Jira issues.
- Potential duplicate event types: N/A
- Follow-up actions and owners: Add links to screenshots for events 1-5 Hussein, add specified links for events 6-10 Hasan.

## 4. Standard Taxonomy Entry Fields

| Field | Recording requirement |
|---|---|
| Event ID | Use the existing catalogue identifier |
| Event name | Use the catalogue name |
| Catalogue reference | Link to the source entry and identify the reviewed version |
| Syslog severity | Record the observed message severity; use Not available if absent |
| Analytical severity | Apply the agreed severity rules below |
| Classification status | Supported or Provisional |
| Analytical question | State what the analyst needs to determine |
| Response category | Immediate action, Correlate, or Log only |
| Rationale | Explain the classification using evidence and network context |
| Evidence limitations | State missing, ambiguous, or unverified information |
| Additional evidence needed | Identify what would resolve uncertainty |
| Evidence references | Link relevant screenshots, logs, and supporting records |

## 5. Proposed Analytical Severity Rules

These levels are proposed team conventions. Record any agreed
changes before applying them throughout the taxonomy.

| Level | Definition |
|---|---|
| Low | Evidence supports limited significance or routine/recovery activity, with no demonstrated significant impact |
| Medium | Activity warrants investigation because its authorization, significance, or potential impact requires clarification |
| High | Evidence supports significant impact or an active condition requiring prompt attention |
| Undetermined | Available evidence is insufficient for a defensible severity assignment |

Consider:
- Device and network-segment role.
- Affected services and demonstrated impact.
- Whether the action was authorized.
- Frequency and related activity.
- Existing controls and their observed response.

Syslog severity and analytical severity are separate.
Do not infer malicious intent solely from a message code,
severity number, missing authorization record, or event name.

For controlled tests, distinguish the observed test outcome
from the potential significance of the same event in operation.
State any conditions that would change the classification.

## 6. Response Categories

| Category | Definition |
|---|---|
| Immediate action | The observed condition warrants prompt action; identify the justified action and supporting reason |
| Correlate | Review related events or supporting records before deciding significance or further response |
| Log only | Retain the event; available context does not indicate a need for further action |

Do not assume every event at one analytical severity always
requires the same response. Explain the selected response.

## 7. Analytical Question Rules

Each question must identify the uncertainty an analyst needs
to resolve.

Questions may address:
- Was the activity authorized?
- Which device, account, interface, or service was affected?
- Was there actual service impact?
- Is the event related to other suspicious activity?
- Did a protective control or recovery action work?

Questions must not assume an attack occurred unless supporting
evidence establishes that conclusion.

## 8. Evidence and Uncertainty Rules

- Use the catalogue and linked evidence as the factual basis.
- Separate observed facts from interpretations and possibilities.
- Record missing fields as Not shown or Not available.
- Record checks not performed as Not assessed.
- Mark classifications Provisional when material uncertainty remains.
- Use Undetermined where analytical severity cannot be justified.
- Identify the evidence needed to resolve uncertainty.
- Do not label a behavior a confirmed Packet Tracer limitation
  without supporting evidence.
- Do not treat an unobserved event as confirmed unsupported.
- If a source entry appears incorrect, record a correction request
  rather than silently introducing different facts.

## 9. Reusable Taxonomy Entry

### [Event ID] — [Event Name]

- Catalogue reference:
- Catalogue version / commit:
- Syslog severity:
- Analytical severity:
- Classification status: Supported / Provisional
- Analytical question:
- Response category:

#### Classification Rationale

Explain the severity and response using the observed evidence,
device role, and relevant context.

#### Evidence Limitations

State what is missing or cannot be concluded.

#### Additional Evidence Needed

Identify checks or records needed to resolve uncertainty.
Use None identified if appropriate.

## 10. Review and Change Record

| Date | Reviewer / contributor | Finding or change | Reason | Resolution / commit link |
|---|---|---|---|---|
| | | | | |

### Review Outcome

- All required events identified:
- Structure consistent across entries:
- Source references checked:
- Unsupported assumptions identified:
- Outstanding corrections:
- Outcome: Approved / Changes required / Pending
