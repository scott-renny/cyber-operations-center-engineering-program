# Cyber Operations Center Engineering Program Roadmap

> **Status:** Active Development  
> **Version:** 1.6  
> **Repository:** Cyber Operations Center Engineering Program

---

# Purpose

This roadmap defines the engineering lifecycle for the Cyber Operations Center Engineering Program.

Rather than deploying technologies at random, every phase is designed to build upon previous work, ensuring the environment remains secure, scalable, maintainable, and fully documented.

Each completed phase represents a measurable engineering milestone.

---

# Engineering Philosophy

This project follows several core principles:

- Security by Design
- Zero Trust
- Defense in Depth
- Least Privilege
- Documentation First
- Automation First
- Observability
- Continuous Validation
- Scalability
- Resilience
- Continuous Improvement

Every engineering decision should support one or more of these principles.

---

# Phase Completion Criteria

A phase is considered complete only when all of the following have been finished:

- Planning completed
- Architecture documented
- Installation completed
- Configuration documented
- Validation performed
- Security considerations documented
- Lessons learned recorded
- Screenshots captured or an approved sanitized evidence substitute recorded
- Repository documentation updated

If one of these items is incomplete, the phase remains in progress.

---

# Engineering Roadmap

| Phase | Status | Description |
|--------|--------|-------------|
| Phase 0 | 🟩 Complete | [Program Governance](phases/phase-00-program-governance/README.md) |
| Phase 1 | 🟩 Complete | [Foundation: Full Wipe & Clean-Slate Rebuild](phases/phase-01-foundation/README.md) |
| Phase 2 | 🟩 Complete | [Base Hardening and Operations Portal](phases/phase-02-base-hardening/README.md) |
| Phase 3 | 🟩 Complete | [Container Platform and Service Management](phases/phase-03-container-platform/README.md) |
| Phase 4 | 🟩 Complete | [Core Network & Security Services](phases/phase-04-core-network-security/README.md) |
| Phase 5 | 🟩 Complete | [Backup & Recovery](phases/phase-05-backup-recovery/README.md) |
| Phase 6 | 🟩 Complete | [NET-WATCH](phases/phase-06-netwatch/README.md) |
| Phase 7 | 🟩 Complete | [Telemetry Backbone](phases/phase-07-telemetry-backbone/README.md) |
| Phase 8 | 🟩 Complete | [Endpoint Engineering](phases/phase-08-endpoint-engineering/README.md) — laptop, workstation, phone, and tablet baselines complete |
| Phase 8.5 | ⬜ Planned | [Windows 11 Pro Workstation Migration](phases/phase-08-5-workstation-migration/README.md) |
| Phase 9 | ⬜ Planned | Nextcloud Platform |
| Phase 10 | ⬜ Planned | Identity Services |
| Phase 11 | ⬜ Planned | Detection Engineering |
| Phase 12 | ⬜ Planned | Attack Map |
| Phase 13 | ⬜ Planned | Threat Intelligence |
| Phase 14 | ⬜ Planned | Incident Response |
| Phase 15 | ⬜ Planned | SOAR Platform |
| Phase 16 | ⬜ Planned | Endpoint Management |
| Phase 17 | ⬜ Planned | Digital Forensics |
| Phase 18 | ⬜ Planned | Velociraptor Deployment |
| Phase 19 | ⬜ Planned | Purple Team Operations |
| Phase 20 | ⬜ Planned | Security Operations |
| Phase 21 | ⬜ Planned | Integration Validation |
| Phase 22 | ⬜ Planned | Omada Network Upgrade |
| Phase 23 | ⬜ Planned | Cloud Laboratory |
| Phase 24 | ⬜ Planned | VPS VPN Infrastructure |
| Phase 25 | ⬜ Planned | Media Services Platform |

---

# Current milestone

Phase 6 completed the production NET-WATCH deployment with device discovery, profile controls, Pi-hole enforcement, Wazuh visibility, private HTTPS access, and systemd-managed operation.

Phase 7 completed the telemetry backbone. Zeek now provides rich network metadata; Prometheus, node_exporter, and cAdvisor provide host and container metrics; Grafana consolidates operational dashboards; and Graylog provides searchable aggregation for non-Wazuh logs.

Phase 8 completed the endpoint-engineering baseline across the laptop, legacy workstation, phone, and tablet. The work includes host hardening, secure connectivity, Wazuh and Sysmon validation, mobile security revalidation, malware remediation, and a clean restore-tested migration source.

Phase 8.5 is the next planned workstream. It will migrate the approved Windows 10 source to a TPM-backed, BitLocker-protected Windows 11 Pro workstation and retire the legacy system. Phase 9 has not started.

---

# Status Indicators

| Icon | Meaning |
|------|---------|
| ⬜ | Planned |
| 🟨 | In Progress |
| 🟦 | Testing |
| 🟩 | Complete |
| 🟥 | Requires Rework |

---

# Continuous Improvement

The roadmap is a living document.

As the project evolves, additional engineering improvements may be introduced where they strengthen the architecture, security posture, or operational capabilities. Any changes should preserve the overall architectural vision and be documented through the repository's decision records.

---

# Long-Term Vision

The Cyber Operations Center Engineering Program is intended to demonstrate a complete engineering lifecycle—from planning and architecture through deployment, validation, operations, and continuous improvement.

The completed environment will serve as a platform for expanding knowledge in:

- Security Operations
- Detection Engineering
- Threat Hunting
- Digital Forensics
- Incident Response
- Automation
- Infrastructure Engineering
- Network Security
- Cloud Security
- Purple Team Operations

This repository documents not only what was built, but why it was built, how it was implemented, and what was learned throughout the process.
