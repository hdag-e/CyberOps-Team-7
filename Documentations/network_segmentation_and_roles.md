# Network Segmentation and Device Role Specification (SCRUM-75) 

## 1. Overview & Purpose
This document defines the functional roles and trust segmentation for the CYBEROPS-07 enterprise baseline network topology in Cisco Packet Tracer. Segmentation is structured around trust levels to ensure lateral movement produces observable security events (e.g., access control denials and authentication failures).

---

## 2. Device Inventory & Functional Roles

### Core Infrastructure & Boundary Devices
- **1× ISR 4331 Router (Edge Router):** Functions as the perimeter boundary. Generates inbound access denial events, WAN interface state changes, perimeter SSH/AAA authentication logs, and configuration change events.
- **2× ISR 4331 Routers (Internal Routers):** Connects distinct trust zones. Enforces Inter-Segment ACLs and generates access control denial logs indicating potential lateral movement between subnets.
- **1× Catalyst 3560 Multilayer Switch (Distribution Switch):** Handles Inter-VLAN routing and core trunking. Source of VLAN state changes, trunking protocol logs, and routing configuration events.
- **3× Catalyst 2960 Switches (Access Switches):** Provides local endpoint connectivity. Enforces Port Security (MAC-based) and generates interface state changes, port security violation traps, and unauthorized connection events.

### Centralized Management & Monitored Services
- **1× Syslog Server (10.20.50.10):** Centralized log collection point for all switches and routers. This is the primary analytical repository for the project.
- **1× NTP Server (10.20.50.20):** Enterprise time source providing synchronized timestamps across all infrastructure devices to enable log correlation.
- **2× Application/File Servers (10.20.30.11, 10.20.30.12):** Protected enterprise assets hosting file and web services. Access attempts generate critical analytical telemetry.

### Endpoints
- **8× User PCs:** Distributed across User (10.20.10.0/24) and Admin (10.20.20.0/24) segments to simulate baseline normal traffic and staged administrative activity.
- **1× Rogue/Staging Laptop:** Unassigned endpoint used to trigger Port Security violations, unauthorized IP claims, and simulated insider/external threat vectors.

---

## 3. Network Segmentation & Subnet Plan

| Segment Name | Subnet Range | Trust Level | Primary Purpose & Monitored Events |
| :--- | :--- | :--- | :--- |
| **User Workstations** | `10.20.10.0/24` | Standard | General user traffic. Generates baseline authentication, DHCP, and HTTP logs. |
| **Admin Workstations** | `10.20.20.0/24` | Elevated | Management endpoints. Generates privileged administrative SSH access events and config changes. |
| **Server Segment** | `10.20.30.0/24` | Protected | Enterprise application targets. Generates server access logs and lateral movement denials. |
| **Logging & Time Services**| `10.20.50.0/24` | Critical | Infrastructure backbone hosting Syslog & NTP. Loss of logging is logged as an emergency event. |
| **Management Network** | `10.20.99.0/24` | Restricted | Infrastructure Out-of-Band management (In-band SSH/SNMP). Any unauthorized access is High Severity. |
| **Guest / Untrusted** | `192.168.50.0/24` | Untrusted | Isolated guest access. Inbound traffic to internal segments is strictly denied and logged. |
| **Edge / External WAN** | `203.0.113.0/24` | External | Simulated ISP link (RFC 5737). Captures perimeter port scans and untargeted external denials. |

---

## 4. Expected Communication Matrix & Flow Rules
1. **User Workstations (`10.20.10.0/24`)** $\rightarrow$ **Server Segment (`10.20.30.0/24`):** Permitted on HTTP/HTTPS/SMB. Direct access to Management (`10.20.99.0/24`) or Logging (`10.20.50.0/24`) is **DENIED & LOGGED**.
2. **Admin Workstations (`10.20.20.0/24`)** $\rightarrow$ **All Internal Segments:** Permitted via SSH (TCP 22) and ICMP for management tasks.
3. **Guest Network (`192.168.50.0/24`)** $\rightarrow$ **Internal Segments:** All traffic to `10.20.0.0/16` is **DENIED & LOGGED**. Internet-bound traffic only.
4. **Infrastructure Devices** $\rightarrow$ **Logging & Time (`10.20.50.0/24`):** All routers and switches MUST communicate with Syslog (`UDP 514`) and NTP (`UDP 123`).

---

## 5. Network Topology Diagram

```mermaid
graph TD
    WAN["Edge WAN / External (203.0.113.0/24)"] --> RTR_EDGE["RTR-EDGE-01 - ISR 4331 Edge Router"]

    RTR_EDGE --> RTR_INT1["RTR-INT-01 - Internal Router"]
    RTR_EDGE --> RTR_INT2["RTR-INT-02 - Internal Router"]

    RTR_INT1 --> SW_DIST["SW-DIST-01 - 3560 Distribution Switch"]
    RTR_INT2 --> SW_DIST

    SW_DIST --> SW_ACC1["SW-ACC-01 - Access Switch"]
    SW_DIST --> SW_ACC2["SW-ACC-02 - Access Switch"]
    SW_DIST --> SW_ACC3["SW-ACC-03 - Access Switch"]

    SW_ACC1 --> USERS["User Subnet (10.20.10.0/24) - PCs 1-4"]
    SW_ACC1 --> GUEST["Guest Subnet (192.168.50.0/24) - Laptop"]

    SW_ACC2 --> ADMIN["Admin Subnet (10.20.20.0/24) - PCs 5-8"]
    SW_ACC2 --> MGMT["Management Subnet (10.20.99.0/24)"]

    SW_ACC3 --> LOGGING["Logging & Time Subnet (10.20.50.0/24) - SRV-SYSLOG & SRV-NTP"]
    SW_ACC3 --> SERVERS["Server Subnet (10.20.30.0/24) - SRV-APP-01 & 02"]
```
