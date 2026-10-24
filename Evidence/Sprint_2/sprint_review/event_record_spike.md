# Security Event Records — Initial Spike Set

- Related Jira Issues: SCRUM-32 (SCRUM-106, SCRUM-108)
- Contributor: Security Analyst Team
- Date: 10/24/2026
- Target Environment: Packet Tracer Centralized Logging (10.20.50.10)

---

## Event 1: EVT-01

- **Event ID:** EVT-01
- **Event Name:** Interface Link State Change
- **Jira Issue:** SCRUM-32
- **Contributor:** Security Analyst Team
- **Date and Time:** 10/24/2026 14:15:00.123
- **Source Device:** SW-ACC-01
- **Packet Tracer file/version:** CYBEROPS07_Configuration_v1_1
- **Evidence status:** Observed

### Generating Action
Navigated to SW-ACC-01 CLI, accessed FastEthernet0/24, executed `shutdown`, then `no shutdown`.

### Log Appearance
```text
*Oct 24 14:15:00.123: %LINK-3-UPDOWN: Interface FastEthernet0/24, changed state to down
*Oct 24 14:15:05.456: %LINK-3-UPDOWN: Interface FastEthernet0/24, changed state to up
```

## Explanation
Legitimate: Scheduled physical maintenance, re-patching a cable, or normal workstation power cycling.

Malicious: Unplugging a security device or plugging in an unauthorized rogue device to the switchport.

## Distinguishing Evidence
Check maintenance change tickets, port-security MAC learning logs, and physical rack access logs for Fa0/24.

## Classification
Syslog severity, if available: Level 3 (Error)

Assigned analytical severity and rationale: Low to Medium (Routine on access ports, critical on core links).

Analytical question: Is this port bounce tied to an approved maintenance ticket?

Response category: Correlate

Security Property affected: Availability

## Limitations
Packet Tracer does not log cable physical diagnostic metrics, optical transceiver power levels, or SFP telemetry.

---

## Event 2: EVT-02

- Event ID: EVT-02
- Event Name: Unauthorized Privileged Access Failure
- Jira Issue: SCRUM-32
- Contributor: Security Analyst Team
- Date and Time: 10/24/2026 14:22:10.012
- Source Device: RTR-EDGE-01
- Packet Tracer file/version: CYBEROPS07_Configuration_v1_1
- Evidence status: Simulated / PT Limitation Documented

### Generating Action
Executed disable to enter user EXEC mode on RTR-EDGE-01, ran the enable command, and entered an incorrect secret password three consecutive times.

### Log Appearance
```text
*Oct 24 14:22:10.012: %SYS-4-CONFIG_P: Access to privileged exec mode failed from vty0 (10.20.50.100)
```

## Explanation
Legitimate: Administrator password typo during routine maintenance.

Malicious: Password brute-force attempt or unauthorized privilege escalation attempt on the edge control plane.

## Distinguishing Evidence
Source IP address history, failure frequency/velocity, and active SSH user session context.

## Classification
Syslog severity, if available: Level 4 (Warning)

Assigned analytical severity and rationale: Medium (Indicates attempt to gain full control of the router).

Analytical question: Did this failure originate from an authorized admin IP address, and was it followed by a successful login?

Response category: Correlate

Security Property affected: Confidentiality / Integrity

## Limitations
Simulation Constraint: Packet Tracer IOS images fail to stream %SYS-4-CONFIG_P traps over UDP 514 to an external Syslog collector during local enable failures, despite configuring logging trap debugging and logging console.

Identity Attribution: Packet Tracer logs line information (vty0), but does not capture granular username attribution without external AAA/TACACS+ integration.

---

## Event 3: EVT-03

- Event ID: EVT-03
- Event Name: CLI Configuration Mode Entry
- Jira Issue: SCRUM-32
- Contributor: Security Analyst Team
- Date and Time: 10/24/2026 14:30:00.881
- Source Device: SW-DIST-01
- Packet Tracer file/version: CYBEROPS07_Configuration_v1_1
- Evidence status: Observed

### Generating Action
Entered configure terminal on SW-DIST-01 and exited configuration mode using end.

### Log Appearance
```text
*Oct 06, 04:26:15.2626: SYS-5-CONFIG_I: Configured from console by console
```

## Explanation
Legitimate: Authorized network configuration update or troubleshooting activity.

Malicious: Unapproved configuration modification, backdooring, or disabling security controls.

## Distinguishing Evidence
Diff between running-config and startup-config, paired with active change control ticket approvals.

## Classification
Syslog severity, if available: Level 5 (Notice)

Assigned analytical severity and rationale: Low (In-window approved change) / High (Out-of-hours unannounced).

Analytical question: Was configuration mode entered during an approved change window?

Response category: Correlate

Security Property affected: Integrity / Availability

## Limitations
Packet Tracer logs that configuration mode was entered and exited (%SYS-5-CONFIG_I), but does NOT stream individual CLI command strings or parameter changes to Syslog.
