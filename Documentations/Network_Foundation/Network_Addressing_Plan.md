# Enterprise Network Addressing Plan (SCRUM-74)

## 1. Purpose

This document defines the IPv4 addressing plan for the CYBEROPS-07
simulated enterprise network. The addressing plan supports the approved
network segmentation, Packet Tracer implementation, centralized logging,
time synchronization, baseline connectivity testing, and later security
event analysis.

## 2. Network Addressing Plan

| Segment | Network/CIDR | Default Gateway | Purpose |
|---|---|---|---|
| User Workstations | 10.20.10.0/24 | 10.20.10.1 | Standard user endpoints |
| Admin Workstations | 10.20.20.0/24 | 10.20.20.1 | Administrative endpoints |
| Server Segment | 10.20.30.0/24 | 10.20.30.1 | Enterprise application/file servers |
| Logging & Time Services | 10.20.50.0/24 | 10.20.50.1 | Centralized Syslog and NTP |
| Management Network | 10.20.99.0/24 | 10.20.99.1 | Network infrastructure management |
| Guest / Untrusted | 192.168.50.0/24 | 192.168.50.1 | Untrusted/guest endpoint |
| Edge / External WAN | 203.0.113.0/24 | TBD | Simulated external/ISP network |

## 3. Device Addressing

| Device | Role | IP Address |
|---|---|---|
| SRV-SYSLOG | Centralized Syslog Server | 10.20.50.10 |
| SRV-NTP | NTP Server | 10.20.50.20 |
| SRV-APP-01 | Application/File Server | 10.20.30.11 |
| SRV-APP-02 | Application/File Server | 10.20.30.12 |

Additional device-level addresses will be assigned during Packet Tracer
implementation using the subnet and gateway assignments defined above.

## 4. Address Allocation Convention

The following convention will be used when assigning addresses within
each internal /24 network:

- .1 = Default gateway
- .2-.9 = Network infrastructure
- .10-.49 = Servers and infrastructure services
- .50-.199 = Endpoints
- .200-.254 = Reserved for future use

Exceptions are permitted where a device has an explicitly assigned
address, such as the Syslog, NTP, and application servers.

## 5. Addressing and Security Considerations

Network segments are separated according to their trust level and
functional purpose. Access between segments will be controlled according
to the communication rules defined in the Network Segmentation and Device
Role Specification.

The Logging & Time Services network is treated as critical because it
contains the centralized Syslog and NTP services required for security
event collection and accurate timestamp correlation.

## 6. Validation

The addressing plan will be validated during Packet Tracer
implementation and baseline connectivity testing.

Validation will include:

- Correct IP addressing on network devices and endpoints
- Correct default gateways
- Connectivity between permitted network segments
- Denial of traffic between restricted segments
- Communication with the centralized Syslog server
- Communication with the NTP server
- Verification that addressing matches the approved topology

## 7. Dependencies

This addressing plan is based on the Network Segmentation and Device Role
Specification (SCRUM-75).

The plan will be used by the Packet Tracer implementation work in
SCRUM-84 and SCRUM-85.

## 8. Change Control

If the approved topology changes during implementation, this addressing
plan will be updated before the corresponding Packet Tracer configuration
is finalized.
