# Baseline Device Configuration Checklist & Standards (SCRUM-77)

## 1. Overview
This document specifies the core operational baseline configuration required for every infrastructure device in the enterprise Packet Tracer topology prior to applying security hardening or monitoring features in subsequent tasks.

---

## 2. Naming Conventions & Standard Identifiers
All devices must be named consistently across CLI hostnames and Packet Tracer canvas labels:

- **Edge Router:** `RTR-EDGE-01`
- **Internal Routers:** `RTR-INT-01`, `RTR-INT-02`
- **Distribution Switch:** `SW-DIST-01`
- **Access Switches:** `SW-ACC-01`, `SW-ACC-02`, `SW-ACC-03`
- **Servers:** `SRV-SYSLOG`, `SRV-NTP`, `SRV-APP-01`, `SRV-APP-02`

---

## 3. Mandatory Baseline CLI Configuration Checklist
Every router and switch must have the following core baseline settings applied:

### A. Device Identity & Hostname
```cisco
enable
configure terminal
hostname <DEVICE_NAME>
ip domain-name cyberops.local
```
### B. Console & Line Control Baseline
```cisco
! Console Port Execution & Sync
line con 0
 exec-timeout 10 0
 logging synchronous
exit

! VTY Lines Execution & Sync
line vty 0 15
 exec-timeout 10 0
 logging synchronous
exit
```
### C. Clock & Timezone Setup
```cisco
! Uniform Timezone Baseline
clock timezone UTC 0 
```

---

### 4. Layer 3 Inter-VLAN Routing Standards (SW-DIST-01)
```cisco
! Step 1: Create Layer 2 VLAN Database Entries 
vlan 10
 name Users
vlan 20
 name Admins
vlan 30
 name Servers
vlan 50
 name Logging_NTP
vlan 99
 name Management
vlan 500
 name Guest
exit

! Step 2: Enable Layer 3 Inter-VLAN Routing
ip routing

! Step 3: Configure Layer 3 SVI Gateways
interface Vlan10
 description User_Subnet_Gateway
 ip address 10.20.10.1 255.255.255.0
 no shutdown

interface Vlan20
 description Admin_Subnet_Gateway
 ip address 10.20.20.1 255.255.255.0
 no shutdown

interface Vlan30
 description Server_Subnet_Gateway
 ip address 10.20.30.1 255.255.255.0
 no shutdown

interface Vlan50
 description Logging_NTP_Subnet_Gateway
 ip address 10.20.50.1 255.255.255.0
 no shutdown

interface Vlan99
 description Management_Subnet_Gateway
 ip address 10.20.99.1 255.255.255.0
 no shutdown

interface Vlan500
 description Guest_Untrusted_Gateway
 ip address 192.168.50.1 255.255.255.0
 no shutdown

! Step 4: Configure Trunk Ports to Access Switches 
interface range Gig1/0/1 - 3
 switchport trunk encapsulation dot1q
 switchport mode trunk
 description Trunk_To_Access_Switches
 no shutdown
```
