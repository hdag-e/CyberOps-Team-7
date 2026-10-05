# Project Acceptance Criteria (SCRUM-79)

## 1. Purpose

This document defines measurable acceptance criteria for CYBEROPS-07.
The criteria provide objective conditions for determining whether the
project requirements and major deliverables have been successfully
completed.

## 2. Monitoring Foundation

### AC-01 — Network Baseline
The Packet Tracer topology contains all required network devices,
servers, and endpoints defined in the approved architecture.

### AC-02 — Baseline Connectivity
Required baseline connectivity tests complete successfully for all
permitted communication paths.

### AC-03 — Centralized Logging
Network devices successfully send logs to the centralized Syslog server
at 10.20.50.10.

### AC-04 — Time Synchronization
Required network devices successfully synchronize with the NTP server at
10.20.50.20.

### AC-05 — Clock-Skew Demonstration
A deliberate clock-skew condition can be demonstrated, documented, and
then restored to synchronized time.

## 3. Security Event Catalogue

### AC-06 — Event Coverage
At least 15 distinct security event types are deliberately generated and
documented.

### AC-07 — Event Documentation
Each event includes:
- Generating action
- Log appearance
- Benign explanation
- Malicious explanation
- Distinguishing evidence

## 4. Taxonomy and Triage

### AC-08 — Event Taxonomy
All documented events are classified according to the project's defined
severity, analytical question, and response-category criteria.

### AC-09 — Triage Procedure
The documented triage procedure can be followed by a team member who did
not create the procedure.

### AC-10 — Escalation
The escalation matrix identifies when and how events should be escalated.

## 5. Correlation and Incident Reconstruction

### AC-11 — Correlation Workbook
The correlation methodology allows events from multiple sources to be
manually compared and related.

### AC-12 — Multi-Stage Incidents
At least three staged multi-stage incidents are generated and
reconstructed.

### AC-13 — Evidence Traceability
Incident conclusions are supported by documented event evidence. When
available evidence does not support a conclusion, the limitation is
explicitly documented rather than assumed.

## 6. Incident Response Playbooks

### AC-14 — Playbook Coverage
At least four NIST SP 800-61-aligned incident response playbooks are
completed.

### AC-15 — Detection Mapping
Playbook detection procedures identify the relevant event taxonomy
entries.

### AC-16 — ATT&CK Mapping
Relevant analytical activities are mapped to named MITRE ATT&CK
techniques where applicable.

## 7. Monitoring Coverage

### AC-17 — Coverage Gap Assessment
The project identifies meaningful monitoring coverage gaps and documents
their impact and limitations.

## 8. Blind Exercise

### AC-18 — Blind Exercise
The team successfully completes the Week 8 blind exercise using the
documented monitoring, triage, correlation, and response procedures.

### AC-19 — Independent Usability
A team member who did not create a procedure can use the documentation
to perform the required analytical task.

## 9. Evidence Requirements

### AC-20 — Evidence
Each major acceptance criterion has supporting evidence stored in the
project repository and linked to the relevant Jira work item where
applicable.

### AC-21 — Testing
Acceptance tests are executed and results are documented before final
submission.

### AC-22 — Limitations
Known failures, unsupported conclusions, and project limitations are
documented with their cause and impact.

## 10. Review and Approval

Acceptance criteria will be reviewed by the team during Sprint 1 and
used throughout subsequent sprints to evaluate completed work.

Changes to acceptance criteria require team review and documentation of
the reason for the change.
