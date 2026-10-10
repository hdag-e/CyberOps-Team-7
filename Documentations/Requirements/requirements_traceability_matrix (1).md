# Requirements Traceability Matrix & Review Process (SCRUM-80)

## 1. Overview & Operating Rules
This document establishes end-to-end traceability across the CYBEROPS-07 project lifecycle. It maps every Jira Parent Story and Child Subtask to its core scope requirement, Git evidence location, and validation status.

### Operating Rules for Team Members:
1. **Scope Mapping:** Every Jira subtask must map to at least one core scope deliverable or test case.
2. **Evidence Linking:** Subtasks cannot be marked `Done` in Jira without linking relative file paths to logs, documentation, or `.pkt` models in the repository.
3. **Living Lifecycle Document:** Update this table whenever new subtasks move to `In Progress` or `Complete`.

---

## 2. Sprint 1 Requirements & Traceability Matrix

| Parent Story | Subtask ID | Task Description | Scope Mapping | Evidence / File Path in Repository | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **SCRUM-23** | | **Establish enterprise network baseline** | Appx D & E | N/A (Parent Story) | :white_check_mark: Complete |
| | **SCRUM-74** | Define the enterprise network addressing plan | Appx D & E | [network_segmentation_and_roles.md](network_segmentation_and_roles.md) | :white_check_mark: Complete |
| | **SCRUM-75** | Define device roles and network segmentation | Appx D & E | `Documentations/Network_Foundation/network_segmentation_and_roles.md` | :white_check_mark: Complete |
| | **SCRUM-76** | Document baseline network architecture | Appx D & E | `Documentations/Network_Foundation/Baseline_Network_Architecture.md` | :white_check_mark: Complete |
| | **SCRUM-77** | Define baseline device configuration requirements | Appx B | `Documentations/Network_Foundation/baseline_config_requirements.md` | :white_check_mark: Complete |
| **SCRUM-24** | | **Finalize project requirements & acceptance criteria** | Appx A | N/A (Parent Story) | :white_check_mark: Complete |
| | **SCRUM-78** | Review project scope and required deliverables | Appx A | `Documentations/Requirements/Project_Scope_and_Deliverables.md` | :white_check_mark: Complete |
| | **SCRUM-79** | Define measurable project acceptance criteria | Charter | `Documentations/Requirements/Project_Acceptance_Criteria.md` | :white_check_mark: Complete |
| | **SCRUM-80** | Establish requirements traceability and review process | Charter / RTM | `Documentations/Requirements/requirements_traceability_matrix.md` | :white_check_mark: Complete |
| **SCRUM-25** | | **Set up shared repository and project structure** | Infra Setup | N/A (Parent Story) | :white_check_mark: Complete |
| | **SCRUM-81** | Initialize shared project repository | Infra Setup | Root (`README.md`, `CONTRIBUTING.md`) | :white_check_mark: Complete |
| | **SCRUM-82** | Establish repository folder structure and naming conventions | QA Standards | Repository Directory Tree | :white_check_mark: Complete |
| | **SCRUM-83** | Establish contribution and version-control workflow | QA Standards | `CONTRIBUTING.md` | :white_check_mark: Complete |
| **SCRUM-26** | | **Build and verify Packet Tracer topology** | Appx D | N/A (Parent Story) | :white_check_mark: Complete |
| | **SCRUM-84** | Build the enterprise network topology in Packet Tracer | Appx D | `Evidence/Sprint_1/network_evidence/Sprint 1-Scrum 84-Packet Tracer Topology.png` | :white_check_mark: Complete |
| | **SCRUM-85** | Configure baseline device interfaces and addressing | Appx D & E | `Evidence/Sprint_1/network_evidence/Rtr-Edge ip assignment.png` | :white_check_mark: Complete |
| | **SCRUM-86** | Configure baseline routing and switching behavior | Appx D & E | `Evidence/Sprint_1/network_evidence/inter-vlan routing.png` | :white_check_mark: Complete |
| | **SCRUM-87** | Verify topology configuration against the approved design | Appx D | `Evidence/Sprint_1/network_evidence/SCRUM-26_MasterTopology.png` | :white_check_mark: Complete |
| **SCRUM-27** | | **Verify baseline network connectivity** | Test T-01 | N/A (Parent Story) | In Progress |
| | **SCRUM-88** | Define baseline connectivity test matrix | Test T-01 | `Evidence/Sprint_1/connectivity_tests/` | In Progress |
| | **SCRUM-89** | Execute baseline connectivity tests | Test T-01 | `Evidence/Sprint_1/network_evidence/PC-admin1 ping test.png` | :white_check_mark: Complete |
| | **SCRUM-90** | Document and resolve baseline connectivity issues | Test T-01 | `Evidence/Sprint_1/baseline_verification/` | In Progress |
| **SCRUM-28** | | **Establish project evidence and documentation structure** | Quality Assurance | N/A (Parent Story) | :white_check_mark: Complete |
| | **SCRUM-91** | Establish project evidence repository structure | QA Standards | `Evidence/` Folder | :white_check_mark: Complete |
| | **SCRUM-92** | Define project documentation standards and templates | QA Standards | `Documentations/Templates/` | :white_check_mark: Complete |
| | **SCRUM-93** | Establish project decision, risk, and review records | QA Standards | Section 3 of RTM File | :white_check_mark: Complete |

---

## 3. Decision, Change, & Known Limitation Record

### A. Architectural Design Baseline
- **DEC-01 (Inter-VLAN Routing):** Selected Cisco Catalyst 3560 as the distribution layer switch to perform native Layer 3 routing between network trust segments per Appendix D.
- **DEC-02 (Centralized Services Subnet):** Designated `10.20.50.0/24` as the dedicated Logging & Time Services segment, housing the Syslog and NTP infrastructure per Appendix E.

### B. Observed Bugs & Technical Limitations
*(No simulator bugs or technical workarounds encountered yet. Issues will be documented here as testing and topology verification progress in Sprint 1.)*

---

## 4. Peer Review & Validation Sign-Off

- **Author: Hasan Dagdelen (hd352)** 
- **Peer Reviewer:** 
- **Review Date:** 
- **Review Outcome:** 
