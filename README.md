# Cyber Operations Center Engineering Program

![Status](https://img.shields.io/badge/status-active%20development-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Platform](https://img.shields.io/badge/platform-Ubuntu%20%7C%20Windows%20%7C%20Docker-orange)
![Documentation](https://img.shields.io/badge/documentation-first-success)
![Focus](https://img.shields.io/badge/focus-cybersecurity%20engineering-red)

> **Status:** 🚧 Active Development  
> **Version:** 1.5.0
> **License:** MIT  
> **Maintainer:** Scott Renny

---

## Executive Summary

The **Cyber Operations Center Engineering Program** is a long-term engineering initiative focused on designing, building, documenting, validating, and operating an enterprise-inspired cybersecurity environment.

Rather than functioning as a collection of disconnected lab exercises, this repository documents the complete lifecycle of a modern cyber operations environment—from architecture and governance through infrastructure deployment, monitoring, detection engineering, incident response, and continuous improvement.

Every phase is treated as an engineering project with defined objectives, requirements, implementation steps, validation evidence, operational considerations, and lessons learned.

---

## Project Vision

Build a professional cybersecurity engineering portfolio that demonstrates practical knowledge of:

- Infrastructure Engineering
- Network Security
- Security Operations
- Detection Engineering
- Threat Intelligence
- Digital Forensics
- Endpoint Engineering
- Incident Response
- Automation
- Cloud Security
- Operational Documentation

The focus is not simply on deploying individual technologies. The program is designed to demonstrate how systems, services, security controls, telemetry sources, and operational processes integrate into a secure, maintainable, and scalable environment.

---

## Program Objectives

This program is built around five primary objectives:

- Design an enterprise-inspired Cyber Operations Center.
- Develop practical cybersecurity engineering skills through hands-on implementation.
- Document architectural decisions and engineering milestones.
- Validate configurations through repeatable testing.
- Demonstrate disciplined engineering practices and continuous improvement.

---

## Engineering Philosophy

Every decision in this repository follows these principles:

- Security by Design
- Defense in Depth
- Zero Trust
- Least Privilege
- Documentation First
- Automation First
- Observability
- Continuous Validation
- Scalability
- Resilience
- Continuous Improvement

Technology is only one component of cybersecurity. Secure environments are created through thoughtful design, disciplined implementation, continuous monitoring, repeatable validation, and comprehensive documentation.

---

## Table of Contents

- [Repository Documentation](#repository-documentation)
- [Current Milestone](#current-milestone)
- [Repository Status](#repository-status)
- [Engineering Roadmap](#engineering-roadmap)
- [Architecture Overview](#architecture-overview)
- [Technology Stack](#technology-stack)
- [Repository Structure](#repository-structure)
- [Documentation Standards](#documentation-standards)
- [Long-Term Vision](#long-term-vision)
- [Future Enhancements](#future-enhancements)
- [Why This Repository Exists](#why-this-repository-exists)
- [Feedback](#feedback)

---

## Repository Documentation

| Document | Description |
|---|---|
| [README.md](README.md) | Program overview and repository landing page |
| [ROADMAP.md](ROADMAP.md) | Program roadmap and engineering phases |
| [ARCHITECTURE.md](ARCHITECTURE.md) | High-level system architecture |
| [SECURITY-PRINCIPLES.md](SECURITY-PRINCIPLES.md) | Security engineering principles |
| [DOCUMENTATION-STANDARDS.md](DOCUMENTATION-STANDARDS.md) | Documentation requirements and expectations |
| [RISK-REGISTER.md](RISK-REGISTER.md) | Program risks, mitigations, ownership, and review practices |
| [Data Governance](docs/DATA-GOVERNANCE.md) | Data classification, retention, evidence, and sanitization controls |
| [Device Inventory](docs/DEVICE-INVENTORY.md) | Authoritative asset-inventory and lifecycle schema |
| [Secrets Management](docs/SECRETS-MANAGEMENT.md) | Secrets, certificates, key rotation, and exposure-response standard |
| [Portfolio Policy](docs/PORTFOLIO-POLICY.md) | Public-release classification and sanitization requirements |
| [Operational Governance Mapping](docs/OPERATIONAL-GOVERNANCE-MAPPING.md) | Governance controls inherited by runbooks, playbooks, and campaign sequences |
| [Severity Standard](docs/SEVERITY-STANDARD.md) | Incident severity, priority, escalation, and closure standard |
| [Evidence Handling Standard](docs/EVIDENCE-HANDLING-STANDARD.md) | Evidence integrity, custody, retention, and sanitization requirements |
| [Change Management Standard](docs/CHANGE-MANAGEMENT-STANDARD.md) | Change planning, validation, rollback, and closure requirements |
| [Adversary-Emulation Standard](docs/ADVERSARY-EMULATION-STANDARD.md) | Authorization, stop conditions, cleanup, and publication controls |
| [Operational Document Migration Map](docs/DOCUMENT-MIGRATION-MAP.md) | Promotion path from legacy material to governed documents |
| [Runbook Index](runbooks/README.md) | Planned and validated repeatable operational procedures |
| [Playbook Index](playbooks/README.md) | Planned and validated incident-response procedures |
| [Campaign Index](campaigns/README.md) | Authorized adversary-emulation campaign roadmap |
| [Operational Templates](templates/README.md) | Reusable procedure, case, evidence, validation, and review templates |
| [Architecture Decision Records](docs/decisions/README.md) | Decision process and ADR index |
| [Phase 0 Completion Record](phases/phase-00-program-governance/README.md) | Governance completion evidence and Phase 1 entry gate |
| [Phase 1 Completion Record](phases/phase-01-foundation/README.md) | Clean-slate foundation implementation, validation, and lessons learned |
| [Phase 1 Validation Evidence](phases/phase-01-foundation/evidence/README.md) | Sanitized operating-system, storage, network, SSH, and power evidence |
| [Phase 2 Completion Record](phases/phase-02-base-hardening/README.md) | Hardened baseline and private HTTPS operations portal |
| [Phase 2 Validation Evidence](phases/phase-02-base-hardening/evidence/README.md) | Sanitized access-control, firewall, audit, update, and portal evidence |
| [Phase 3 Completion Record](phases/phase-03-container-platform/README.md) | Docker, Dockge, segmentation, logging, and secrets conventions |
| [Phase 3 Validation Evidence](phases/phase-03-container-platform/evidence/README.md) | Sanitized container-platform and management-plane evidence |
| [Phase 4 Completion Record](phases/phase-04-core-network-security/README.md) | Core network, VPN, DNS filtering, monitoring, and malware protection |
| [Phase 4 Validation Evidence](phases/phase-04-core-network-security/evidence/README.md) | Sanitized Phase 4 service and security-control evidence |
| [CONTRIBUTING.md](CONTRIBUTING.md) | Contribution and change-management guidelines |
| [CHANGELOG.md](CHANGELOG.md) | Version history and notable changes |
| [LICENSE](LICENSE) | MIT License |

---

## Current Milestone

The program has completed **Phase 4 — Core Network and Security Services**.

Phase 4 established:

- persistent private addressing for Atlas;
- hardened ISP-router and wireless settings;
- WireGuard remote access;
- Wazuh security monitoring;
- Pi-hole DNS filtering for controlled pilot clients;
- ClamAV malware detection and scheduled scanning;
- LAN- and VPN-scoped management firewall rules; and
- a documented safe deferral of Suricata until wired Ethernet is available.

Review the [Phase 4 completion record](phases/phase-04-core-network-security/README.md) and [validation evidence](phases/phase-04-core-network-security/evidence/README.md).

The next milestone is:

> **Phase 5 — Backup and Recovery**


## Repository Status

| Area | Status |
|---|---|
| Repository Foundation | ✅ Complete |
| Documentation Framework | ✅ Complete |
| Architecture Planning | ✅ Complete |
| Security Principles | ✅ Complete |
| Initial Risk Register | ✅ Complete |
| Phase 0 Documentation | ✅ Complete |
| Phase 1 Foundation | ✅ Complete |
| Phase 2 Base Hardening | ✅ Complete |
| Private Operations Portal | ✅ Complete |
| Container Platform | ✅ Complete |
| Core Network and Security Services | ✅ Complete |
| Infrastructure Deployment | 🚧 In Progress |
| Security Stack | 🚧 In Progress |
| Detection Engineering | ⏳ Planned |
| Incident Response | ⏳ Planned |
| Cloud Integration | ⏳ Planned |

Status definitions:

- ✅ **Complete** — Documented and reviewed
- 🚧 **In Progress** — Currently being developed
- ⏳ **Planned** — Approved for future implementation

---

## Engineering Roadmap

```text
Program Governance
        │
        ▼
Foundation
        │
        ▼
Base Hardening
        │
        ▼
Container Platform
        │
        ▼
Core Network and Security Services
        │
        ▼
Monitoring and Telemetry
        │
        ▼
Endpoint Engineering
        │
        ▼
Identity and Access Management
        │
        ▼
Detection Engineering
        │
        ▼
Incident Response and SOAR
        │
        ▼
Digital Forensics
        │
        ▼
Purple Team Validation
        │
        ▼
Security Operations
        │
        ▼
Cloud and Infrastructure Expansion
        │
        ▼
Continuous Improvement
```

The detailed 26-phase engineering plan is available in [ROADMAP.md](ROADMAP.md).

---

## Architecture Overview

```text
                           Internet
                               │
                               ▼
                        WireGuard VPN
                               │
                               ▼
                         Omada Network
                               │
                               ▼
                          Ubuntu Server
                               │
                               ▼
                      Docker Container Platform
                               │
      ┌────────────────────────┼────────────────────────┐
      ▼                        ▼                        ▼
  Monitoring              Security Stack          Core Services

  Grafana                 Wazuh                   Nextcloud
  Prometheus              Zeek                    Identity
  NET-WATCH               Suricata                Backup
                          Graylog                 Media Services
                          TheHive
                          Cortex
                          Velociraptor
                          MISP
```

This diagram represents the intended high-level architecture. Components marked as planned will be introduced and validated during their corresponding roadmap phases.

See [ARCHITECTURE.md](ARCHITECTURE.md) for additional architectural details.

---

## Technology Stack

The following technologies are planned or currently available within the environment.

### Infrastructure

- Ubuntu Server
- Windows 11 Pro
- Windows 11 Home
- Docker
- Docker Compose
- WireGuard
- Omada Networking

### Monitoring and Observability

- Grafana
- Prometheus
- NET-WATCH

### Security Operations

- Wazuh
- Zeek
- Suricata
- Graylog

### Threat Intelligence

- MISP

### Incident Response

- TheHive
- Cortex

### Digital Forensics

- Velociraptor

### Identity and Access Management

- Active Directory
- Role-Based Access Control
- Least-privilege administration

Technology names in this section represent the planned program architecture and should not be interpreted as completed implementations unless supported by phase documentation and validation evidence.

---

## Repository Structure

```text
cyber-operations-center-engineering-program/
│
├── .gitignore
├── LICENSE
├── README.md
├── ROADMAP.md
├── ARCHITECTURE.md
├── SECURITY-PRINCIPLES.md
├── DOCUMENTATION-STANDARDS.md
├── RISK-REGISTER.md
├── CONTRIBUTING.md
├── CHANGELOG.md
├── SECURITY.md
│
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   ├── config.yml
│   │   └── feature_request.md
│   └── PULL_REQUEST_TEMPLATE.md
│
├── docs/
│   ├── DATA-GOVERNANCE.md
│   ├── DEVICE-INVENTORY.md
│   ├── OPERATIONAL-GOVERNANCE-MAPPING.md
│   ├── PORTFOLIO-POLICY.md
│   ├── SECRETS-MANAGEMENT.md
│   ├── SEVERITY-STANDARD.md
│   ├── EVIDENCE-HANDLING-STANDARD.md
│   ├── CHANGE-MANAGEMENT-STANDARD.md
│   ├── ADVERSARY-EMULATION-STANDARD.md
│   ├── DOCUMENT-MIGRATION-MAP.md
│   ├── decisions/
│
├── runbooks/
│   └── README.md
├── playbooks/
│   └── README.md
├── campaigns/
│   └── README.md
├── templates/
│   ├── README.md
│   └── operational record templates
│
└── phases/
    ├── phase-00-program-governance/
    ├── phase-01-foundation/
    │   ├── README.md
    │   └── evidence/
    │       └── README.md
    ├── phase-02-base-hardening/
    │   ├── README.md
    │   ├── config/
    │   ├── evidence/
    │   └── portal/
    ├── phase-03-container-platform/
    │   ├── README.md
    │   ├── config/
    │   └── evidence/
    └── phase-04-core-network-security/
        ├── README.md
        └── evidence/
```

This tree shows the current governance and completed Phase 1–4 implementation baseline. Additional implementation, validation, diagram, evidence, and asset directories will be added as their corresponding phases begin.

---

## Documentation Standards

Each implementation phase is expected to include:

- Purpose
- Objectives
- Scope
- Requirements
- Dependencies
- Architecture
- Implementation
- Configuration
- Security Considerations
- Validation
- Troubleshooting
- Operational Procedures
- Lessons Learned
- Known Limitations
- Future Improvements
- Supporting Diagrams
- Screenshots or Evidence

Documentation is treated as a first-class engineering deliverable.

A phase is not considered complete solely because a service has been installed. Completion requires documented implementation, security review, validation evidence, and operational understanding.

See [DOCUMENTATION-STANDARDS.md](DOCUMENTATION-STANDARDS.md) for the full requirements.

---

## Long-Term Vision

When complete, this program will demonstrate practical engineering experience across:

- Cybersecurity Engineering
- Infrastructure Engineering
- Security Operations
- Detection Engineering
- Threat Hunting
- Digital Forensics
- Incident Response
- Threat Intelligence
- Endpoint Management
- Identity and Access Management
- Security Automation
- Network Engineering
- Cloud Security
- Backup and Recovery
- Operational Documentation

The objective is to understand how enterprise security technologies operate together—not simply how to install them individually.

---

## Future Enhancements

Planned repository additions include:

- Architecture Decision Records
- Infrastructure diagrams
- Network trust-zone diagrams
- Asset and service inventories
- Detection rules
- SIEM dashboards
- Threat-hunting playbooks
- Incident-response workflows
- SOAR automation
- Validation reports
- Operational runbooks
- Recovery procedures
- Performance benchmarks
- Configuration templates
- Phase completion reports
- Lessons learned for every completed phase

Tool-specific topics and repository metadata will be added as technologies are implemented and supported by meaningful documentation.

---

## Why This Repository Exists

This repository serves as a living engineering portfolio that demonstrates technical growth through disciplined planning, implementation, validation, and documentation.

Every deployment, configuration change, architectural decision, validation result, operational improvement, and lesson learned is recorded to create a transparent engineering history that reflects real-world cybersecurity practices.

The value of the program is not measured only by the number of technologies deployed. It is measured by how deliberately those technologies are selected, secured, integrated, validated, operated, and improved.

---

## Feedback

Constructive feedback, technical discussion, and suggestions for improvement are welcome.

Continuous learning and continuous improvement are core principles of this program.

---

> **Build deliberately. Validate continuously. Document everything.**
