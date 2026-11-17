# Incident #2 — Controlled Test Record & Sealed Evidence Package ( `SCRUM-51` )

## 1. Metadata & Package Control

| Field | Details |
| :--- | :--- |
| **Incident ID** | Incident #2 ( `SCRUM-51` / Sprint 4 ) |
| **Scenario Title** | Insider Sabotage (Failed Breach & Physical Pivot) |
| **Stager / Lead** | Project Manager / Red Team Lead |
| **Assigned Blind Reconstructor** | Analyst Teammate ( `SCRUM-52` ) |
| **Lab Environment File** | `CYBEROPS07_Configuration_v3_4.pkt` (Isolated Execution Copy) |
| **Central NTP & Syslog Server** | `SRV-NTP` / `SRV-SYSLOG` ( `10.20.50.10` ) |

---

## 2. Pre-Execution Clock & NTP Verification ( `SCRUM-51` )

Timestamp consistency across involved devices was verified prior to executing incident actions:

* **Central NTP Reference ( `10.20.50.10` ):** Stratum 1 / Reference Clock
* **SW-DIST-01 ( `10.20.50.1` ):** Synchronized, Stratum 2, Reference `10.20.50.10`, Clock Offset `0.00` msec
* **RTR-INT-01 ( `10.20.99.2` ):** Synchronized, Stratum 2, Reference `10.20.50.10`, Clock Offset `0.00` msec

---

## 3. Incident Scenario Narrative & Attack Path

### 3.1 Executive Narrative
An insider threat operating from a standard User segment workstation ( `PC-USER-01`, `10.20.10.11` ) attempts an unauthorized SSH login against the Distribution Switch ( `SW-DIST-01`, `10.20.50.1` ) using the `secadmin` account ( `EVT-03` ). After three failed attempts, the actor pivots laterally to an elevated Administrative workstation ( `PC-ADMIN-01`, `10.20.20.11` ) and attempts a remote SSH breach against the Internal Router ( `RTR-INT-01`, `10.20.99.2` ) using the `admin` account, which also fails ( `EVT-03` ). Frustrated by network access controls, the insider physical bypasses the network by connecting a local console cable directly to `RTR-INT-01`, authenticating successfully via `[localport: 0]` ( `EVT-03` ). Once in privileged EXEC mode, the actor enters global configuration mode ( `EVT-02` ), navigates to transit interface `GigabitEthernet0/0/0`, and executes an administrative shutdown ( `EVT-01` ) to sever upstream routing before exiting configuration mode ( `EVT-02` ).

### 3.2 Grading Hook (Earliest Evidence of Activity)
* **Earliest Observable Log Evidence:** The initial `%SEC_LOGIN-5-LOGIN_FAILED: Login failed [user: secadmin] [localport: 22]` authentication failure ( `EVT-03` ) at 11:36:58 UTC on `SW-DIST-01` ( `10.20.50.1` ) forwarded to `SRV-SYSLOG` ( `10.20.50.10` ).
* **Analytical Trap:** The attack spans two source IPs ( `10.20.10.11` and `10.20.20.11` ) and transitions from a remote VTY session (`[localport: 22]`) to a physical console session (`[localport: 0]`), requiring careful correlation to track the actor's physical movement.

---

## 4. Staged Action Sequence & Observed Evidence

| Stage | MITRE ATT&CK | Catalogue ID | Target Device (Interface / IP) | Deliberate Generating Action | Observed Syslog Message | Exact Timestamp (UTC) | Evidence Reference |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1. Initial Access (Failed)** | T1110 (Brute Force) | `EVT-03` | `SW-DIST-01` ( `10.20.50.1` ) | Execute 3 failed SSH login attempts from `PC-USER-01` ( `10.20.10.11` ) using username `secadmin`. | `%SEC_LOGIN-5-LOGIN_FAILED` (x3) | 11:36:58 – 11:37:00 UTC | Logged in `Incident_02_Syslog_Export.txt` |
| **2. Lateral Pivot (Failed)** | T1110 (Brute Force) | `EVT-03` | `RTR-INT-01` ( `10.20.99.2` ) | Execute 1 failed SSH login attempt from `PC-ADMIN-01` ( `10.20.20.11` ) using username `admin`. | `%SEC_LOGIN-5-LOGIN_FAILED` (x1) | 11:37:44 UTC | Logged in `Incident_02_Syslog_Export.txt` |
| **3. Physical Bypass** | T1091 (Replication Through Removable Media / Local) | `EVT-03` | `RTR-INT-01` ( `10.20.99.2` ) | Access `RTR-INT-01` via simulated local console cable and authenticate as `admin`. | `%SEC_LOGIN-5-LOGIN_SUCCESS [localport: 0]` | 11:37:46 UTC | Logged in `Incident_02_Syslog_Export.txt` |
| **4. Impact (Sabotage)** | T1498 (Network DoS) | `EVT-01` | `RTR-INT-01` ( `Gi0/0/0` — `10.20.250.2` ) | Enter interface `GigabitEthernet0/0/0`, execute `shutdown`. | `%LINK-5-CHANGED` and `%LINEPROTO-5-UPDOWN` (down) | 11:39:34 UTC | Logged in `Incident_02_Syslog_Export.txt` |
| **5. Tampering (Exit)** | T1565 (Data/Config Manipulation) | `EVT-02` | `RTR-INT-01` ( `10.20.99.2` ) | Exit configuration mode completely (`end`, `exit`). | `%SYS-5-CONFIG_I: Configured from console by console` | 11:39:36 UTC | Logged in `Incident_02_Syslog_Export.txt` |

### 4.1 Raw Exported Syslog Extract (`SRV-SYSLOG` — `10.20.50.10`)
```text
10.06.2026 11:36:58.661 AM		10.20.50.1	%SEC_LOGIN-5-LOGIN_FAILED: Login failed [user: secadmin] [localport: 22] [Reason: Login Authentication Failed] at 11:36:58 UTC Tue Oct 6 2026
10.06.2026 11:36:59.760 AM		10.20.50.1	%SEC_LOGIN-5-LOGIN_FAILED: Login failed [user: secadmin] [localport: 22] [Reason: Login Authentication Failed] at 11:36:59 UTC Tue Oct 6 2026
10.06.2026 11:37:00.657 AM		10.20.50.1	%SEC_LOGIN-5-LOGIN_FAILED: Login failed [user: secadmin] [localport: 22] [Reason: Login Authentication Failed] at 11:37:00 UTC Tue Oct 6 2026
10.06.2026 11:37:44.417 AM		10.20.99.2	%SEC_LOGIN-5-LOGIN_FAILED: Login failed [user: admin] [localport: 22] [Reason: Login Authentication Failed] at 11:37:44 UTC Tue Oct 6 2026
10.06.2026 11:37:46.643 AM		10.20.99.2	%SEC_LOGIN-5-LOGIN_SUCCESS: Login Success [user: admin] [localport: 0] at 11:37:46 UTC Tue Oct 6 2026
10.06.2026 11:39:34.856 AM		10.20.99.2	%LINK-5-CHANGED: Interface GigabitEthernet0/0/0, changed state to administratively down
10.06.2026 11:39:34.856 AM		10.20.99.2	%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/0/0, changed state to down
10.06.2026 11:39:36.764 AM		10.20.99.2	%SYS-5-CONFIG_I: Configured from console by console
5. Packet Tracer Simulator Limitations Encountered
Source IP Omission on Initial Auth Failure ( EVT-03 ): Cisco Packet Tracer IOS firmware intermittently drops the `` header on the very first SSH failure against a device (observed at 11:36:58 AM and 11:37:44 AM). The source IP successfully populates on subsequent rapid attempts. This requires the reconstructing analyst to infer the initial source based on immediate successive logs.

Command-Level Audit Accounting ( EVT-02 ): Standard Cisco IOS emits %SYS-5-CONFIG_I upon entering/exiting configuration mode, but Packet Tracer lacks TACACS+ command accounting or archive configuration diff logging to record exact CLI commands executed during Stage 4.

Console vs. SSH Attribution Gap: The simulator does not differentiate physical location beyond [localport: 0] for console and [localport: 22] for SSH. The analyst must apply logical deduction to realize the attacker physically bypassed the network to achieve the console login.

6. Sealing & Blind Reconstruction Sufficiency Verification ( SCRUM-51 )
Evidence Sealing Declaration:

Event generation for Incident #2 ( SCRUM-51 ) concluded at 11:39:36 UTC (Tue Oct 6 2026). The exported syslog file is frozen and sealed with no post-capture modifications.

Sufficiency Check:

[x] All generated events map exclusively to the Sprint 3 Event Catalogue ( EVT-01, EVT-02, EVT-03 ).

[x] Raw syslog entries contain consistent, NTP-synchronized timestamps across primary attack phases.

[x] The assigned teammate ( SCRUM-52 ) can reconstruct the full timeline and identify the physical bypass pivot using only the sealed raw logs and Sprint 3 documentation.
