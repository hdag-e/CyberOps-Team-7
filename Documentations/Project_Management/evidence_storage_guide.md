# Evidence Storage Guide

## 1. Purpose

This guide defines where CYBEROPS-07 project artifacts and supporting evidence are stored. It helps all four team members locate work, understand what evidence demonstrates, and connect it to Jira issues and project requirements.

## 2. Storage Locations

Use the following locations consistently. Create any missing folders before using them.

| Artifact | Repository location |
|---|---|
| Packet Tracer files | `Packet_tracer/` |
| Exported device configurations | `Packet_tracer/Configurations/` |
| Network design and configuration explanations | `Documentations/Network_Foundation/` |
| Event catalogue and completed event records | `Documentations/Event_catalogue/` |
| Taxonomy, triage procedure, and escalation matrix | `Documentations/Taxonomy_Triage/` |
| Correlation workbook and methodology | `Documentations/Correlation/` |
| Incident reports and reconstructions | `Documentations/Correlation/Incidents/` |
| Incident response playbooks | `Documentations/Playbooks/` |
| Final report and monitoring coverage gap assessment | `Documentations/Final_Report/` |
| Meeting notes | `Meetings and PM/` |
| Decisions, risks, blockers, and tracking logs | `Documentations/Project_management/` |
| Blank documentation templates | `Documentations/Templates/` |
| Test results, screenshots, captured logs, and review evidence | Appropriate category under `Evidence/Sprint_#/` |

Store the main artifact in its designated location and link to its supporting evidence. Avoid maintaining duplicate working copies.

## 3. Sprint Evidence Categories

Evidence is stored under the sprint in which it was collected: `Sprint_1` through `Sprint_5`.

Each sprint uses the following categories:

| Category | Contents |
|---|---|
| `Baseline_verification/` | Baseline configuration and monitoring verification results |
| `Connectivity_tests/` | Connectivity test records and supporting output |
| `Network_evidence/` | Topology diagrams, network screenshots, and other network evidence |
| `Sprint_review/` | Sprint review records and review of the overall documentation/evidence structure |
| `Event_generation/` | Captured logs and screenshots demonstrating deliberate event generation |
| `Triage_and_escalation/` | Results showing application and validation of triage and escalation procedures |
| `Incident_reconstruction/` | Raw incident evidence, timeline verification, and reconstruction validation |
| `Playbook_validation/` | Playbook desk-check results and supporting evidence |

Place completed test records alongside their supporting evidence. Place artifact-specific peer-review records alongside the reviewed artifact or its supporting evidence, and link them from the artifact.

These folders can be added to each sprint as needed for that sprints requirements

## 4. File Naming

Follow the general naming convention in `Contributing.md`:

`[category]_[description]_[date/version].[ext]`

Use lowercase letters, numbers, and underscores, without spaces.

Examples:

- `test_t01_syslog_verification_20261007.png`
- `test_t01_syslog_result_20261007.md`
- `event_evt01_failed_login_20261007.txt`
- `incident_01_reconstruction_v1.md`
- `review_evidence_structure_20261007.md`

Include the relevant acceptance test ID where applicable. Use descriptive filenames that distinguish separate evidence captures.

Packet Tracer files follow the specific versioning convention in `Contributing.md`, such as `CYBEROPS07_Topology_v1.0.pkt`.

## 5. Evidence Traceability

Completed documentation records must identify:

- Responsible contributor.
- Date and, where relevant, capture time and timezone.
- Related Jira issue.
- Related project requirement or acceptance test, where applicable.
- Device and Packet Tracer version, where relevant.
- Result or finding.
- Links to supporting evidence.
- Known limitations or required follow-up.

A screenshot or log file must be linked from a record explaining what it demonstrates. Use relative repository links where practical.

Acceptance test IDs such as `T-01` refer to Appendix F of the project brief. Event and incident IDs are assigned consistently by the team.

Jira issues must link to the relevant repository artifacts, evidence folders, or commits. Commit messages must follow the Jira issue format required by `Contributing.md`.

## 6. Saving Evidence

When completing project work:

1. Copy the appropriate blank template and complete it.
2. Save the completed record in its designated location.
3. Save supporting evidence in the relevant sprint and category.
4. Link the evidence from the completed record.
5. Preserve original log output and visible timestamps. Label illustrative material clearly.
6. Commit the files and link them from the related Jira issue.

Record failed or blocked tests honestly, including corrective actions. If evidence is collected again after a correction, retain the earlier evidence and distinguish the new capture by date or description.

## 7. Peer Review and Team Understanding

Another team member reviews the structure and confirms that evidence can be located and understood.

The review record identifies the reviewer, date, artifact or commit reviewed, findings, corrections, and outcome.

All four members receive a walkthrough of this guide. Meeting notes record attendance, questions, and confirmation of understanding.

## 8. Changes to the Structure

Record changes to folder locations, evidence categories, or naming rules in:

`Documentations/Project_management/structure_change_log.md`

Include the date, contributor, change, reason, affected paths, and related Jira issue or commit. Update this guide and communicate changes to the team.

## 9. Final Submission Support

Use the project scope and deliverables document and Appendix F test plan to check that every required deliverable has a location and supporting evidence.

Before final submission, confirm that repository links work, required evidence is present, reviews are recorded, and limitations are documented.
