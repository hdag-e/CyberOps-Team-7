# Logging Severity Rationale and Event Handling Requirements

- **Document ID:** DOC-SCRUM34-01
- **Jira Issue:** SCRUM-34
- **Author / Contributor:** Security Analyst Team
- **Date:** 10/24/2026
- **Target Environment:** Packet Tracer Centralized Logging (`10.20.50.10`)
- **Version:** 1.0

---

## 1. Executive Summary & Objective (SCRUM-34)
This document establishes the official SOC interpretation framework for security logging severity across the baseline event set (`EVT-01`, `EVT-02`, and `EVT-03`). It bridges technical Syslog severity levels (RFC 5424 / Cisco IOS defaults) with analytical security significance, maps each event to standard analytical questions and response categories, and explicitly documents Packet Tracer simulation limitations.

---

## 2. Severity Review of Initial Event Set (SCRUM-114)

| Event ID | Event Name | Device / Interface | Observed / Expected Log Line | Observed Syslog Severity | Severity Source | Supporting Evidence Reference |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **EVT-01** | Interface Link State Change | `SW-ACC-01` (`Fa0/24`) | `%LINK-3-UPDOWN: Interface FastEthernet0/24, changed state to down` / `up` | Level 3 (Error) | Explicitly provided in log header (`%LINK-3-UPDOWN`) | `Evidence/Sprint_2/network_evidence/EVT-01_syslog_receipt.png` |
| **EVT-02** | Unauthorized Privileged Access Failure | `RTR-EDGE-01` (`vty0`) | `%SYS-4-CONFIG_P: Access to privileged exec mode failed from vty0` | Level 4 (Warning) | Documented Cisco IOS standard (`%SYS-4-CONFIG_P`) | **PT Simulation Limitation:** Traps not emitted remotely over UDP 514 on local failure (`Evidence/Sprint_2/network_evidence/EVT-02_syslog_receipt.png`) |
| **EVT-03** | CLI Configuration Mode Entry | `SW-DIST-01` (Console/VTY) | `%SYS-5-CONFIG_I: Configured from console by console` | Level 5 (Notice) | Explicitly provided in log header (`%SYS-5-CONFIG_I`) | `Evidence/Sprint_2/network_evidence/EVT-03_syslog_receipt.png` |

---

## 3. Severity Interpretation Rationale (SCRUM-115)

### 3.1 Syslog Severity Standard Mapping
The logging architecture adheres to standard Cisco IOS Syslog severity levels (0–7):
- **Level 3 (Error):** Error conditions that impact interface or protocol operational states.
- **Level 4 (Warning):** Warning messages indicating potential security risks or operational anomalies.
- **Level 5 (Notice):** Normal but significant operational events (e.g., system configuration changes).

### 3.2 Technical Log Severity vs. Analytical Security Significance
Technical Syslog severity reflects system health or state change impact, **not inherent security malice**. SOC analysts must evaluate events based on context:
1. **Context-Driven Risk:** A Level 3 (`%LINK-3-UPDOWN`) on an edge access port (`Fa0/24`) during business hours is typically benign (workstation reboot), whereas the same alert on a core trunk link or server port indicates a critical operational outage or physical tampering.
2. **Intent & Velocity:** A Level 4 (`%SYS-4-CONFIG_P`) single failure is likely a human typo; three consecutive failures within seconds indicate a brute-force or privilege escalation attempt.
3. **Handling Unobserved / Missing Severity Events:** When Packet Tracer fails to stream explicit remote traps (e.g., `EVT-02`), analysts must rely on local CLI buffer inspection (`show logging`) or secondary telemetry rather than inferring unverified syslog payloads.

### 3.3 Packet Tracer Telemetry & Severity Visibility Limitations
- **UDP 514 Suppression (`EVT-02`):** Cisco IOS in Packet Tracer does not stream `%SYS-4-CONFIG_P` Syslog messages across the network to `SRV-SYSLOG` during local `enable` password failures, despite `logging trap debugging` execution.
- **Granular Command Lack (`EVT-03`):** `%SYS-5-CONFIG_I` logs configuration mode entry/exit, but PT does not support TACACS+ command accounting or individual CLI string logging to Syslog.
- **Transceiver/Diagnostic Metrics (`EVT-01`):** Physical layer diagnostic metrics (DOM/SFP light levels) are unsupported in PT.

---

## 4. Analytical Question & Response Category Mapping (SCRUM-116)

The standard response categories utilized across the SOC taxonomy are defined as:
- **Correlate:** Match event telemetry with change tickets, session timestamps, and secondary device logs before taking action.
- **Investigate:** Perform active forensic analysis to identify source IP, active user sessions, and potential compromise scope.
- **Escalate:** Notify Tier 2/3 SOC or Incident Response team for active containment.

### Mapping Table

| Event ID | Primary Analytical Question | Response Category | Mapping Rationale | Missing Evidence / Uncertainty |
| :--- | :--- | :--- | :--- | :--- |
| **EVT-01** | Is this interface link bounce tied to an approved physical maintenance ticket or known workstation activity? | **Correlate** | Interface bounces occur routinely during physical work or PC restarts. Cross-referencing against change control prevents false-positive escalation. | PT does not log physical MAC learning transitions or cable diagnostic metrics alongside port bounce. |
| **EVT-02** | Did this privilege failure originate from an authorized management IP address, and was it followed by a successful login? | **Investigate** | Multiple failed `enable` attempts signal unauthorized access attempts. Investigating source IP and velocity determines brute-force intent. | PT suppresses remote UDP 514 trap transmission for this event and lacks TACACS+ username attribution. |
| **EVT-03** | Was configuration mode entered during an authorized maintenance window by an approved network administrator? | **Correlate** | Configuration changes alter infrastructure security posture. Correlation against change tickets verifies authorization. | PT logs config mode entry/exit but does not stream individual CLI command strings to Syslog. |

---

## 5. Peer Review Record (SCRUM-117)

### Review Summary
- **Reviewer:** Teammate / Security Analyst Reviewer (`CyberOps-Team-7`)
- **Review Date:** 10/24/2026
- **Status:** Approved with Modifications Resolved

### Checklist & Verification
- [x] **Catalogue Consistency:** Severity definitions and event details align 100% with `event_records_spike.md`.
- [x] **Traceability:** References accurately point to screenshots in `Evidence/Sprint_2/network_evidence/`.
- [x] **Simulation Accuracy:** Packet Tracer limitations (missing `%SYS-4-CONFIG_P` UDP stream, lack of CLI string logging) are explicitly documented and not assumed.
- [x] **Structure:** Analytical questions and response categories are standardized across all three baseline events.

### Resolved Review Findings
1. *Finding:* Initial draft inferred that `EVT-02` Syslog receipt was fully observed on `SRV-SYSLOG`.  
   *Resolution:* Corrected in Section 2 and 3.3 to explicitly document `EVT-02` as a Packet Tracer simulation constraint.
