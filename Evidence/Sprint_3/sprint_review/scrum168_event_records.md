# Security Event Records — Sprint 3 Set 

- Related Jira Issues: SCRUM-168 (Subtask of Scrum-40)
- Contributor: Hasan Dagdelen / Distribution Switch Lead
- Date: 10/30/2026
- Target Environment: Packet Tracer Centralized Logging (10.20.50.10)

---

## Event 6:

- **Event ID:** EVT-06
- **Event Name:** Distribution Switch Interface State Change
- **Jira Issue:** SCRUM-168
- **Contributor:** Hasan Dagdelen
- **Date and Time:** Oct 6 05:31:04.3131
- **Source Device:** SW-DIST-01 (10.20.50.1)
- **Packet Tracer file/version:** CYBEROPS07_Configuration_v3_0 / Cisco Packet Tracer 8.2.1
- **Evidence status:** Observed

### Generating Action
Accessed SW-DIST-01 CLI, navigated to interface FastEthernet0/1, executed `shutdown`, and subsequently executed `no shutdown`.

### Log Appearance
```text
*Oct 06, 05:31:01.3131: %LINK-5-CHANGED: Interface FastEthernet0/1, changed state to administratively down
*Oct 06, 05:31:01.3131: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/1, changed state to down
*Oct 06, 05:31:04.3131: %LINK-5-CHANGED: Interface FastEthernet0/1, changed state to up
*Oct 06, 05:31:04.3131: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/1, changed state to up
```

## Explanation
Legitimate: Scheduled interface maintenance, re-cabling, or administrative reset of a distribution port.

Malicious: An unauthorized user or attacker taking down a core trunk or access line to cause Denial of Service (DoS) across attached subnets.

## Distinguishing Evidence
Correlation with approved network maintenance windows and concurrent `%SYS-5-CONFIG_I` terminal session logs.

## Classification
Syslog severity, if available: Notice (Severity 5)

Assigned analytical severity and rationale: Low to Medium (Routine if part of maintenance; Medium if executed out-of-hours on a core distribution port).

Analytical question: Was this interface state change pre-approved by an active network change ticket?

Response category: Correlate

Security Property affected: Availability

## Limitations
Cisco Packet Tracer captures basic Layer 2 %LINK-5-CHANGED and %LINEPROTO-5-UPDOWN console events, but lacks real-world hardware telemetry such as SFP optical transceiver power levels, Time-Domain Reflectometry (TDR) cable diagnostics, or physical PHY layer negotiation errors.

---

## Event 7:

- **Event ID:** EVT-07
- **Event Name:** Distribution Switch Configuration Mode Entry & Unauthorized VLAN Creation
- **Jira Issue:** SCRUM-168
- **Contributor:** Hasan Dagdelen
- **Date and Time:** Oct 6 05:21:50.2121
- **Source Device:** SW-DIST-01 (10.20.50.1)
- **Packet Tracer file/version:** CYBEROPS07_Configuration_v3_0 / Cisco Packet Tracer 8.2.1
- **Evidence status:** Observed

### Generating Action
Accessed SW-DIST-01 CLI, entered global configuration mode (`configure terminal`), created an unapproved VLAN (`vlan 999 name SUSPICIOUS_MGMT_TEMP`), and exited using `end`.

### Log Appearance
```text
*Oct 06, 05:21:50.2121: %SYS-5-CONFIG_I: Configured from console by console
```

## Explanation
Legitimate: Network engineer configuring new network segments or modifying Layer 2/3 parameters during scheduled maintenance.

Malicious: An attacker attempting to establish persistent out-of-band management channels, bypass VLAN isolation, or perform VLAN hopping.

## Distinguishing Evidence
Running-configuration diff comparison showing the addition of `VLAN 999`, paired with change-control ticket verification.

## Classification
Syslog severity, if available: Notice (Severity 5)

Assigned analytical severity and rationale: Medium. Unapproved VLAN creation on a distribution switch alters Layer 2 network segmentation boundaries.

Analytical question: Do the newly added configuration parameters (VLAN 999) match an approved architecture ticket?

Response category: Correlate

Security Property affected: Integrity

## Limitations
While standard Cisco IOS generates a global %SYS-5-CONFIG_I syslog message confirming that configuration mode was entered/exited, Packet Tracer does not support advanced CLI command accounting (e.g., archive config or TACACS+ command logging). Consequently, the specific commands executed (such as vlan 999) must be audited manually via show running-config.
---

## Event 8:

- **Event ID:** EVT-08
- **Event Name:** Privilege Exec Mode Authentication Failure (`enable` secret)
- **Jira Issue:** SCRUM-168
- **Contributor:** Hasan Dagdelen
- **Date and Time:** Oct 6 05:25:00.000 (Approx)
- **Source Device:** SW-DIST-01 (10.20.50.1)
- **Packet Tracer file/version:** CYBEROPS07_Configuration_v3_0 / Cisco Packet Tracer 8.2.1
- **Evidence status:** Observed (Console) / PT Forwarding Limitation Documented

### Generating Action
Accessed SW-DIST-01 console/VTY interface, entered username 1 with an invalid password, resulting in an authentication failure.

### Log Appearance
```text
%SEC_LOGIN-5-LOGIN_FAILED: Login failed [user: 1] [localport: 0] [Reason: Login Authentication Failed] at 10:09:19 UTC Tue Oct 6 2026
```

## Explanation
Legitimate: Administrator password mistype or outdated credentials entered during routine switch management.

Malicious: Password guessing, credential stuffing, or brute-force attack targeting local administrative accounts on the distribution switch.

## Distinguishing Evidence
Frequency of failed attempts within a short time window, connection source line, and failure patterns preceding or following successful logon events (%SEC_LOGIN-5-LOGIN_SUCCESS).

## Classification
Syslog Severity: Notice (Severity 5)

Assigned Analytical Severity & Rationale: Medium. Indicates unauthorized access attempts targeting control-plane management interfaces.

Analytical Question: Did this login failure originate from an authorized console/management station, and was it followed by account lockout?

Response Category: Correlate / Monitor

Security Property Affected: Confidentiality / Integrity

## Limitations
Cisco IOS standard local security auditing captures the attempted username (1) and local port (0), but Packet Tracer does not capture higher-layer identity attributes such as TACACS+ session tokens or client MAC addresses without external AAA integration.

---

## Event 9:

- **Event ID:** EVT-09
- **Event Name:** Port Security Violation and Error-Disable Action
- **Jira Issue:** SCRUM-168
- **Contributor:** Hasan Dagdelen
- **Date and Time:** Oct 6 05:55:53.5555
- **Source Device:** SW-DIST-01 (10.20.50.1)
- **Packet Tracer file/version:** CYBEROPS07_Configuration_v3_0 / Cisco Packet Tracer 8.2.1
- **Evidence status:** Observed

### Generating Action
Configured port security on SW-DIST-01 interface FastEthernet0/10 with static MAC `1111.2222.3333` and violation mode `shutdown`. Connected host PC0 (MAC `0030.A314.C145`) and initiated traffic (`ping 10.20.50.1`).

### Log Appearance
```text
*Oct 06, 05:55:53.5555: %LINK-5-CHANGED: Interface FastEthernet0/10, changed state to administratively down
*Oct 06, 05:55:53.5555: %LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/10, changed state to down
*Oct 06, 05:55:53.5555: %PM-4-ERR_DISABLE: psecure-violation error detected on Fa0/10, putting Fa0/10 in err-disable state.
*Oct 06, 05:55:53.5555: %PORT_SECURITY-2-PSECURE_VIOLATION: Security violation occurred, caused by MAC address 0030.A314.C145 on port FastEthernet0/10.
```

## Explanation
Legitimate: User swapping out an authorized workstation or attaching an unapproved personal device (BYOD) to a secured port.

Malicious: Rogue device insertion or MAC spoofing attempt targeting the distribution layer to intercept subnet traffic.

## Distinguishing Evidence
Output of `show port-security interface FastEthernet0/10` confirming violation count `1` and last source MAC `0030.A314.C145`.

## Classification
Syslog severity, if available: Critical (Severity 2) / Warning (Severity 4)

Assigned analytical severity and rationale: High. Represents an unauthorized physical connection attempt, resulting in automatic port suppression.

Analytical question: Is MAC address `0030.A314.C145` listed in the corporate asset management inventory?

Response category: Immediate action

Security Property affected: Integrity / Availability

## Limitations
Port security logging (%PORT_SECURITY-2-PSECURE_VIOLATION) effectively captures the offending MAC address (0030.A314.C145) and puts the interface in err-disable. However, Layer 2 security telemetry alone cannot identify higher-layer host attributes, such as the attached device's hostname, operating system, or whether the MAC address was spoofed.

---

## Event 10:

- **Event ID:** EVT-10
- **Event Name:** Spanning Tree BPDU Guard Violation and Port Error-Disable
- **Jira Issue:** SCRUM-168
- **Contributor:** Hasan Dagdelen
- **Date and Time:** Oct 6 06:04:19.044
- **Source Device:** SW-DIST-01 (10.20.50.1)
- **Packet Tracer file/version:** CYBEROPS07_Configuration_v3_0 / Cisco Packet Tracer 8.2.1
- **Evidence status:** Observed

### Generating Action
Enabled `spanning-tree portfast` and `spanning-tree bpduguard enable` on interface FastEthernet0/11 on SW-DIST-01, then connected a device transmitting Spanning Tree Bridge Protocol Data Units (BPDUs).

### Log Appearance
```text
*Oct 06, 06:04:19.044: %SPANTREE-2-BLOCK_BPDUGUARD: Received BPDU on port FastEthernet0/11 with BPDU Guard enabled. Disabling port.
*Oct 06, 06:04:19.044: %PM-4-ERR_DISABLE: bpduguard error detected on 0/11, putting 0/11 in err-disable state.
```

## Explanation
Legitimate: Accidental connection of an unauthorized switch, hub, or wireless router by an employee attempting to expand port availability.

Malicious: Rogue switch insertion attempt to manipulate Spanning Tree topology, perform STP root bridge hijacking, or conduct Layer 2 Man-in-the-Middle (MitM) attacks.

## Distinguishing Evidence
`show interfaces FastEthernet0/11 status` output showing `err-disabled` state with `bpduguard` cause code.

## Classification
Syslog severity, if available: Critical (Severity 2) / Warning (Severity 4)

Assigned analytical severity and rationale: High. Unauthorized STP BPDUs threaten Layer 2 topology stability and routing path integrity.

Analytical question: Was an unauthorized switch or bridge device physically attached to access interface FastEthernet0/11?

Response category: Immediate action

Security Property affected: Availability / Integrity

## Limitations
BPDU Guard immediately shuts down the port (%SPANTREE-2-BLOCK_BPDUGUARD) upon detecting an unauthorized STP frame to protect topology stability. Because the port is isolated at the physical layer instantly, no further packet capture or payload analysis can be conducted on the offending device through that interface.
