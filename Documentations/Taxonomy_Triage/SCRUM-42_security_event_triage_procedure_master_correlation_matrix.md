# SCRUM-42: Security Event Triage Procedure & Master Correlation Matrix

- **Parent Epic:** SCRUM-40 (Sprint 3 Security Event Telemetry Audit)
- **Subtasks Covered:** SCRUM-143, SCRUM-144, SCRUM-145, SCRUM-146
- **Target Environment:** Cisco Packet Tracer 8.2.1 / 9.0.1 (`CYBEROPS07_Configuration_v3_4.pkt`)
- **Central Collector:** `SRV-SYSLOG` (`10.20.50.10`)
- **Contributor / Author:** CyberOps Team 7
- **Date:** November 2026

---

## 1. Master Telemetry Correlation Matrix (EVT-01 – EVT-15)

The following matrix consolidates all verified security telemetry across Edge/Internal Routers, Distribution Switches, and Access Switches within the Sprint 3 scope.

| Event ID | Event Name | Device / Source IP | Primary Syslog Pattern | Syslog Severity | Analytical Severity | Security Property | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **EVT-01** | Interface State Flap | `RTR-INT-01`<br>`10.20.50.1` | `%LINK-3-UPDOWN`<br>`%LINEPROTO-5-UPDOWN` | Sev 3 / Sev 5 | Low to Medium | Availability | Verified (Central Log) |
| **EVT-02** | Global Config Change | `RTR-INT-01`<br>`10.20.99.2` | `%SYS-5-CONFIG_I` | Sev 5 (Notice) | Medium | Integrity | Verified (Central Log) |
| **EVT-03** | Console/VTY Auth Failure | `RTR-INT-01`<br>`10.20.99.2` | `%SEC_LOGIN-5-LOGIN_FAILED` | Sev 5 (Notice) | Medium | Confidentiality / Integrity | Verified (Central Log) |
| **EVT-04** | ACL Deny / Packet Drop | `RTR-EDGE-01` / `RTR-INT-01` | `%SEC-6-IPACCESSLOGP` *(Expected)* | Sev 6 (Info) | Low | Confidentiality | **PT Simulator Limitation** |
| **EVT-05** | Device Reload / Cold Start | `RTR-INT-01`<br>`10.20.50.1` | `%SYS-3-RESTART`<br>`%PMAN-5-EXITACTION` | Sev 3 / Sev 5 | High | Availability | Verified (Central Log) |
| **EVT-06** | Dist Interface State Change | `SW-DIST-01`<br>`10.20.50.1` | `%LINK-5-CHANGED`<br>`%LINEPROTO-5-UPDOWN` | Sev 5 (Notice) | Low to Medium | Availability | Verified (Central Log) |
| **EVT-07** | Config Entry & VLAN Creation | `SW-DIST-01`<br>`10.20.50.1` | `%SYS-5-CONFIG_I` | Sev 5 (Notice) | Medium | Integrity | Verified (Central Log) |
| **EVT-08** | Console Auth Failure | `SW-DIST-01`<br>`10.20.50.1` | `%SEC_LOGIN-5-LOGIN_FAILED` | Sev 5 (Notice) | Medium | Confidentiality / Integrity | Verified (Local / Audit) |
| **EVT-09** | Port Security & Err-Disable | `SW-DIST-01`<br>`10.20.50.1` | `%PORT_SECURITY-2-PSECURE_VIOLATION`<br>`%PM-4-ERR_DISABLE` | Sev 2 / Sev 4 | High | Integrity / Availability | Verified (Central Log) |
| **EVT-10** | BPDU Guard Violation | `SW-DIST-01`<br>`10.20.50.1` | `%SPANTREE-2-BLOCK_BPDUGUARD`<br>`%PM-4-ERR_DISABLE` | Sev 2 / Sev 4 | High | Availability / Integrity | Verified (Central Log) |
| **EVT-11** | Native VLAN Mismatch | `SW-ACC-01`<br>`10.20.99.11` | `%CDP-4-NATIVE_VLAN_MISMATCH` | Sev 4 (Warning) | Medium | Integrity / Availability | Verified (Central Log) |
| **EVT-12** | STP VLAN-Inconsistency Block | `SW-ACC-01`<br>`10.20.99.11` | `%SPANTREE-2-BLOCK_PVID_LOCAL` | Sev 2 (Critical) | High | Integrity / Availability | Verified (Central Log) |
| **EVT-13** | Duplicate IP Address Detection | `SW-ACC-01`<br>`10.20.99.11` | `%IP-4-DUPADDR` | Sev 4 (Warning) | Medium | Availability / Integrity | Verified (Central Log) |
| **EVT-14** | Root Guard Blocking | `SW-ACC-01`<br>`10.20.99.11` | `%SPANTREE-2-ROOTGUARDBLOCK` | Sev 2 (Critical) | High | Integrity / Availability | Verified (Central Log) |
| **EVT-15** | STP Consistency Restoration | `SW-ACC-01`<br>`10.20.99.11` | `%SPANTREE-2-UNBLOCK_CONSIST_PORT` | Sev 2 (Critical) | Informational | Availability / Integrity | Verified (Central Log) |

---

## 2. Security Event Triage Workflow & Requirements (SCRUM-143)

### 2.1 Repeatable Triage Sequence
1. **Intake & Metadata Ingestion:** Extract Event ID, Timestamp, Source Device IP, Header Facilities, and Message String from `SRV-SYSLOG` (`10.20.50.10`).
2. **Initial Evidence Collection:** Correlate incoming events against active network topology state, target interface status (`show interfaces status`), and physical port bindings.
3. **Contextual Evaluation:** Determine whether the event corresponds to an active, approved Change Management ticket or scheduled maintenance window.
4. **Classification & Categorization:** Map the event to the established analytical severity taxonomy and identify the primary impacted CIA property (Confidentiality, Integrity, Availability).
5. **Action Decision & Handoff:** Assign to a response workflow (`Log Only`, `Correlate / Monitor`, `Immediate Action / Escalate`).
6. **Documentation:** Log resolution or escalation status into the SOC Incident Tracking system.

### 2.2 Packet Tracer Telemetry Handling
Analysts must explicitly distinguish between native telemetry, software limitations, and unverified data:
* **Supported Telemetry:** L2 link states, VLAN inconsistencies, Port Security violations, BPDU/Root Guard triggers, Duplicate IP detection, and `login on-failure log` console auth drops.
* **Unsupported / Unavailable Telemetry:** NetFlow/IPFIX records, TACACS+ user command diff accounting, SFP optical diagnostic telemetry, and packet-level payload contents. Unsupported items must be marked as `UNAVAILABLE_IN_SIMULATOR` rather than assumed.

---

## 3. Classification, Response, and Escalation Framework (SCRUM-144)

### 3.1 Severity Distinction Taxonomy
* **Technical Syslog Severity (Embedded):** The native priority assigned by Cisco IOS (`Sev 2 Critical` to `Sev 6 Informational`). *Note: Built-in technical severity does not automatically dictate operational impact.*
* **Analytical Severity (Contextual):** The calculated risk score based on scope, location (Core vs. Access), and operational context:
  * **Informational:** Expected baseline transitions or recovery events (e.g., `EVT-15`).
  * **Low:** Benign background operational changes during approved maintenance windows (e.g., `EVT-01`, `EVT-06`).
  * **Medium:** Unscheduled configuration alterations or isolated authentication failures (e.g., `EVT-02`, `EVT-03`, `EVT-07`, `EVT-08`, `EVT-11`, `EVT-13`).
  * **High:** Active control-plane disruptions, unauthorized hardware attachment, or hardware err-disable enforcement (e.g., `EVT-05`, `EVT-09`, `EVT-10`, `EVT-12`, `EVT-14`).

### 3.2 Action Response Categories
* **Log Only:** Event recorded for compliance audit trail; no immediate analyst interaction needed (e.g., routine config mode entry with approved ticket).
* **Correlate / Monitor:** Event tracked across a 15-minute sliding window. If frequency exceeds operational threshold, auto-escalate (e.g., repeated console auth failures indicating brute-force).
* **Immediate Action / Escalate:** Hardware isolation verified; analyst must notify Level 2 / SOC Lead immediately for physical site check or subnet containment.

---

## 4. Peer Walkthrough & Independent Validation (SCRUM-145)

### 4.1 Walkthrough Overview
- **Validating Teammate:** Non-Author Peer Analyst (Teammate Reviewer)
- **Validation Date:** November 2026
- **Test Case 1 (Standard Operational Event):** `EVT-09` (Distribution Switch Port Security Violation)
- **Test Case 2 (Simulator Limitation Event):** `EVT-04` (Router Extended ACL Log Drop)

### 4.2 Validation Findings & Observation Record

| Step | Evaluated Task | Outcome | Validator Notes / Issues Identified |
| :--- | :--- | :--- | :--- |
| **Step 1** | Ingest Syslog entry & identify metadata | **Pass** | Timestamp, source IP (`10.20.50.1`), and string `%PORT_SECURITY-2-PSECURE_VIOLATION` correctly identified. |
| **Step 2** | Execute CLI diagnostic verification | **Pass** | Executed `show port-security interface Fa0/10` to confirm err-disable state and offending MAC `0030.A314.C145`. |
| **Step 3** | Apply analytical severity & classification | **Pass** | Assigned Analytical Severity **High** (Integrity/Availability impacted). |
| **Step 4** | Process Simulator Limitation Case (`EVT-04`) | **Pass with Note** | Identified that `log` keyword on extended ACLs fails to compile in Packet Tracer parser. Correctly marked as `UNAVAILABLE_IN_SIMULATOR` per procedure guidelines. |

---

## 5. Finalization & Revision Log (SCRUM-146)

### 5.1 Revisions Completed Post-Validation
1. **Clarified Severity Discrepancies:** Added explicit guidance distinguishing technical Syslog severity from analytical severity to ensure `EVT-15` (Severity 2 Technical) is correctly categorized as Informational operationally.
2. **Standardized Fallback Workflow:** Added formal `UNAVAILABLE_IN_SIMULATOR` tagging rules to prevent analysts from assuming unavailable payload or packet capture data within Cisco Packet Tracer environments.
3. **Repository Commitment:** Committed all associated markdown logs, evidence screenshots, and `.pkt` topology files (`CYBEROPS07_Configuration_v3_4.pkt`) to the shared team repository (`CyberOps-Team-7/Evidence/Sprint_3/`).