# Deliverable D4 — Security Event Escalation Matrix & Decision Framework

- **Jira Issue:** [SCRUM-43]
- **Subtasks Covered:** SCRUM-147, SCRUM-148, SCRUM-149, SCRUM-150
- **Parent Epic:** SCRUM-40 (Sprint 3 Security Telemetry & Incident Analysis)
- **Contributor / Role:** CyberOps Team 7 (Triage & Escalation Lead)
- **Target Environment:** Cisco Packet Tracer 8.2.1 / Central Collector (`SRV-SYSLOG` at `10.20.50.10`)
- **Date:** November 2026

---

## 1. Operational Decision Tiers & Escalation Triggers (SCRUM-147)

To ensure repeatable analyst decision-making, security events are assigned to one of three operational tiers based on analytical context, repetition, target critical asset (CIA impact), and supporting evidence—**never on technical Syslog severity alone**.

```text
                     +---------------------------------------+
                     |    Incoming Event Telemetry (Syslog)  |
                     +---------------------------------------+
                                         |
                                         v
                     +---------------------------------------+
                     |  Tier 1: Routine Analysis (Log Only)  |
                     |  - Single typo / Known baseline state |
                     +---------------------------------------+
                                         |
                       Evidence of Pattern or Anomalous Source
                                         |
                                         v
                     +---------------------------------------+
                     |  Tier 2: Investigate (Correlate)      |
                     |  - Repeated drops, unapproved configs |
                     +---------------------------------------+
                                         |
                      Confirmed Attack / Critical Asset Disruption
                                         |
                                         v
                     +---------------------------------------+
                     |  Tier 3: Escalate (Immediate Action)  |
                     |  - Hardware err-disable, Rogue Device |
                     +---------------------------------------+
```

### Operational Tier Definitions
1. **Tier 1: Routine Analysis (Log Only / Closed)**
   * **Definition:** Single, isolated, operational state changes or benign administrative activities that match expected baselines.
   * **Action:** Retain in central log server (`10.20.50.10`). No active SOC ticket required.
2. **Tier 2: Investigate (Correlate / Active Audit)**
   * **Definition:** Anomalous, repeated, or unverified events that do not pose immediate catastrophic risk but indicate potential scanning, configuration mistakes, or brute-force attempts.
   * **Action:** Open correlation ticket. Cross-reference source IP/MAC against asset inventory and change-control windows.
3. **Tier 3: Escalate (Immediate Incident Response)**
   * **Definition:** Confirmed security policy violations, active hardware containment triggers (err-disable), or unexpected core device reboots that disrupt network Availability or Integrity.
   * **Action:** Immediately escalate to Lead IR Analyst / Tier 2 SOC. Initiate containment playbooks (NIST SP 800-61 aligned).

---

## 2. Master Security Event Escalation Matrix (SCRUM-148 & SCRUM-149)

| Event ID | Catalogue Event Name | Primary Target / Source | Syslog / Tech Severity | Operational Decision Tier | Required Evidence to Examine | Escalation Trigger / Conditions | Response Category & Next Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **EVT-01** | Interface State Flap | `RTR-INT-01`<br>(`10.20.50.1`) | Sev 3 / Sev 5 | **Tier 1 (Routine)** $\rightarrow$ **Tier 2** | Physical access logs, change tickets, consecutive flap counter. | Single flap during window = **Tier 1**. $>3$ flaps in 5 min on core link = **Tier 2**. | **Correlate:** Check for physical link instability or cable tampering. |
| **EVT-02** | Global Config Change | `RTR-INT-01`<br>(`10.20.99.2`) | Sev 5 (Notice) | **Tier 2 (Investigate)** | Change-control authorization, `show running-config` diff. | Configuration change performed outside approved maintenance window. | **Correlate:** Match session timestamp with authorized admin shift. |
| **EVT-03** | Router VTY Auth Failure | `RTR-INT-01`<br>(`10.20.99.2`) | Sev 5 (Notice) | **Tier 1** $\rightarrow$ **Tier 3** | Source VTY line, failure rate per minute, local login log. | $<3$ failures = **Tier 1** (Typo). $\ge 5$ rapid failures from single IP = **Tier 3**. | **Escalate:** Initiate Brute-Force Response Playbook; block source IP. |
| **EVT-04** | ACL Packet Drop | `RTR-EDGE-01` | Sev 6 (Info) | **Tier 1** $\rightarrow$ **Tier 2** | Source/Dest IP headers, drop frequency. *(Documented via PT Analytical Gap)* | External drops = **Tier 1**. Internal drops targeting Server Segment (`10.20.30.0/24`) = **Tier 2**. | **Correlate:** Assess for internal port scan or lateral movement. |
| **EVT-05** | Device Reload / Cold Start | `RTR-INT-01`<br>(`10.20.50.1`) | Sev 3 / Sev 5 | **Tier 3 (Escalate)** | Pre-restart crash dump, power logs, administrative session logs. | Unexpected reboot of core routing gateway causing outage. | **Immediate Action:** Verify routing convergence; check for physical tampering. |
| **EVT-06** | Dist Interface Change | `SW-DIST-01`<br>(`10.20.50.1`) | Sev 5 (Notice) | **Tier 1 (Routine)** | Maintenance schedule, connected access switch status. | Pre-scheduled port reset or trunk bounce. | **Log Only:** Retain event record in central Syslog database. |
| **EVT-07** | Config Mode & VLAN Create | `SW-DIST-01`<br>(`10.20.50.1`) | Sev 5 (Notice) | **Tier 2 (Investigate)** | Change ticket, `show vlan brief` diff (e.g., VLAN 999 creation). | Unapproved VLAN creation altering Layer 2 trust boundary. | **Correlate:** Revert unapproved VLAN; audit administrative console session. |
| **EVT-08** | Switch Auth Failure | `SW-DIST-01`<br>(`10.20.50.1`) | Sev 5 (Notice) | **Tier 2 (Investigate)** | Local VTY session counter, subsequent `%SEC_LOGIN-5-LOGIN_SUCCESS`. | Login failure on distribution layer switch. | **Correlate:** Verify user identity; check for lockouts. |
| **EVT-09** | Port Security Violation | `SW-DIST-01`<br>(`10.20.50.1`) | Sev 2 / Sev 4 | **Tier 3 (Escalate)** | Offending MAC (`0030.A314.C145`), asset inventory, `show port-security`. | Automatic port suppression (`err-disable`) due to unknown MAC. | **Immediate Action:** Dispatch physical security / desktop support to locate rogue device. |
| **EVT-10** | BPDU Guard Violation | `SW-DIST-01`<br>(`10.20.50.1`) | Sev 2 / Sev 4 | **Tier 3 (Escalate)** | Interface status (`err-disabled`), attached device type. | Unauthorized switch sending STP BPDUs on access port. | **Immediate Action:** Isolate unauthorized switch; inspect for MitM or root attack. |
| **EVT-11** | Native VLAN Mismatch | `SW-ACC-01`<br>(`10.20.99.11`) | Sev 4 (Warning) | **Tier 2 (Investigate)** | Neighbor CDP payload, trunk port configuration on both ends. | Configuration error causing potential VLAN hopping or drop. | **Correlate:** Re-align native VLAN configuration across link. |
| **EVT-12** | STP PVID Blocking | `SW-ACC-01`<br>(`10.20.99.11`) | Sev 2 (Critical) | **Tier 3 (Escalate)** | Spanning-tree state output, native VLAN setup. | Automatic STP port blocking on VLAN due to mismatch. | **Immediate Action:** Fix native VLAN mismatch to restore network availability. |
| **EVT-13** | Duplicate IP Address | `SW-ACC-01`<br>(`10.20.99.11`) | Sev 4 (Warning) | **Tier 2 (Investigate)** | Conflicting MAC (`00E0.F759.B3D0`), DHCP lease table, asset list. | Rogue or misconfigured host claiming gateway/switch IP. | **Correlate:** Identify conflicting host; release duplicate static IP. |
| **EVT-14** | Root Guard Blocking | `SW-ACC-01`<br>(`10.20.99.11`) | Sev 2 (Critical) | **Tier 3 (Escalate)** | Superior BPDU bridge priority, switch port status. | Unauthorized bridge attempting to hijack STP Root Bridge role. | **Immediate Action:** Disconnect rogue switch; audit STP priority hierarchy. |
| **EVT-15** | STP Restoration | `SW-ACC-01`<br>(`10.20.99.11`) | Sev 2 (Critical) | **Tier 1 (Routine)** | Preceding EVT-11/12 logs, current port state. | Automatic recovery message after correcting VLAN mismatch. | **Log Only:** Verify port state returned to `forwarding`. |

---

## 3. Handling Missing Evidence & Packet Tracer Limitations (SCRUM-148)

An essential rule of this escalation framework is that **the absence of a log in Packet Tracer does NOT prove that an incident did not occur**.

### Simulator Constraint Escalation Protocol

1. **Uncertain / Insufficient Evidence Path:**
   * When an analyst suspects malicious activity but simulator limitations prevent verification (e.g., missing ACL logs for EVT-04 or missing TACACS+ username tracking for EVT-08), the event **MUST NOT be closed as benign**.
   * It is automatically routed to **Tier 2 (Investigate)** with the tag: `[STATUS: UNVERIFIED - SIMULATOR LIMITATION]`.
2. **Explicit Simulator Gaps Documented:**
   * **ACL Logging (`EVT-04`):** Packet Tracer omits the `log` keyword execution. Analyst must fall back to inspecting interface byte counters (`show interfaces`) and manual ping sweeps to detect scanning.
   * **AAA Command Accounting (`EVT-02`, `EVT-07`):** Packet Tracer logs entry into config mode (`%SYS-5-CONFIG_I`), but not the specific commands entered. Analyst must manually issue `show running-config` and compare against GitHub baseline configs.

---

## 4. Scenario Validation & Peer Walkthrough (SCRUM-149 & SCRUM-150)

To fulfill the acceptance criteria for SCRUM-149 and 150, two representative events were triaged using this matrix by a validating teammate (Eric Lindemulder / Access Switch Lead).

### Validation Test Case 1: Routine Event vs. Rogue Device (EVT-09)
* **Tested Event:** Port Security Violation (`%PORT_SECURITY-2-PSECURE_VIOLATION` on `SW-DIST-01`).
* **Provided Telemetry:** MAC `0030.A314.C145` connected to port Fa0/10.
* **Validator Execution:**
  1. Checked matrix for `EVT-09`.
  2. Identified technical severity: Sev 2 (Critical).
  3. Checked condition: Port put into `err-disable` due to unknown MAC address.
  4. Decision reached: **Tier 3 (Escalate / Immediate Action)**.
* **Validator Outcome:** **PASSED.** The validator correctly bypassed Tier 1/2 and escalated to physical isolation.

### Validation Test Case 2: Evidence-Limited / Ambiguous Event (EVT-04)
* **Tested Event:** Suspected ICMP Reconnaissance Scan against Server Gateway (`10.20.30.1`).
* **Provided Telemetry:** Central Syslog collector shows 0 logs (due to Packet Tracer ACL logging omission).
* **Validator Execution:**
  1. Observed no incoming UDP 514 log entry.
  2. Applied **Section 3 (Simulator Constraint Escalation Protocol)**.
  3. Recognized that absent log $\neq$ non-occurrence.
  4. Executed manual CLI check (`show ip access-lists`) to verify drop count matches.
  5. Decision reached: **Tier 2 (Investigate / Active Audit)** with `[UNVERIFIED - SIMULATOR LIMITATION]` tag.
* **Validator Outcome:** **PASSED.** The validator did not incorrectly dismiss the event.
