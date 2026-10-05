# Baseline Network Architecture (SCRUM-76)

## 1. Purpose

This document describes the baseline architecture of the CYBEROPS-07
simulated enterprise network. The architecture establishes the network
structure required for centralized monitoring, security event generation,
baseline connectivity testing, and later incident analysis.

## 2. Architecture Overview

The enterprise network is organized into separate trust and functional
segments. An edge router provides the simulated external boundary, while
internal routers and a multilayer distribution switch provide connectivity
between the network segments.

Access switches provide endpoint connectivity within the User, Admin,
Guest, Management, Logging/Time, and Server segments.

## 3. Core Architecture

The baseline topology consists of:

- 1 ISR 4331 Edge Router
- 2 ISR 4331 Internal Routers
- 1 Catalyst 3560 Multilayer Distribution Switch
- 3 Catalyst 2960 Access Switches
- 1 Syslog Server
- 1 NTP Server
- 2 Application/File Servers
- 8 User/Admin PCs
- 1 Rogue/Staging Laptop

## 4. Network Segmentation

The network is divided into the following functional segments:

| Segment | Network | Function |
|---|---|---|
| User Workstations | 10.20.10.0/24 | Standard user endpoints |
| Admin Workstations | 10.20.20.0/24 | Administrative endpoints |
| Server Segment | 10.20.30.0/24 | Enterprise application/file servers |
| Logging & Time Services | 10.20.50.0/24 | Syslog and NTP services |
| Management | 10.20.99.0/24 | Network infrastructure management |
| Guest / Untrusted | 192.168.50.0/24 | Untrusted endpoint access |
| Edge / External WAN | 203.0.113.0/24 | Simulated external network |

## 5. Monitoring Architecture

Network devices send security and operational logs to the centralized
Syslog server at 10.20.50.10.

The NTP server at 10.20.50.20 provides a common time source for network
devices. Consistent timestamps support later manual correlation of events
across multiple devices.

## 6. Trust and Access Model

The network uses trust-based segmentation:

- User networks have standard access.
- Admin networks have elevated administrative access.
- Server networks contain protected enterprise assets.
- Logging and time services are treated as critical infrastructure.
- The Management network is restricted.
- Guest traffic is treated as untrusted.
- Traffic between restricted segments is denied and logged where
  specified by the communication rules.

## 7. Baseline Architecture Diagram

The topology follows this general structure:

External WAN
    |
Edge Router
    |
Internal Routers
    |
Distribution Switch
    |
+---+---+---+---+
|   |   |   |   |
User Admin Server Logging/Time Management/Guest
Networks Networks Network Network Networks

Access switches provide endpoint connectivity within the appropriate
segments.

## 8. Dependencies

This architecture is based on SCRUM-75, Network Segmentation and Device
Role Specification, and SCRUM-74, Enterprise Network Addressing Plan.

The architecture will be implemented and verified through SCRUM-84
through SCRUM-87.

## 9. Validation

The architecture will be validated by confirming that:

- All required devices are represented in the Packet Tracer topology.
- Devices are connected according to the approved architecture.
- Each segment uses the assigned network.
- Required monitoring and time services are reachable.
- Restricted traffic is controlled according to the communication rules.
- The implemented topology matches the documented design.

## 10. Change Control

Any significant topology change will be documented and reviewed before
the baseline architecture is considered final.
