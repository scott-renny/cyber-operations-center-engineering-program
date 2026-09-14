# Cyber Operations Center Engineering Program

![Status](https://img.shields.io/badge/status-active%20development-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Platform](https://img.shields.io/badge/platform-Linux%20Mint%20%7C%20Ubuntu%20Server%20%7C%20Windows-blue)

> **Version:** 2.0.3  
> **Status:** Active development  
> **License:** MIT  
> **Maintainer:** Scott Renny

## Overview

This repository documents the design, implementation, validation, and operation of an enterprise-inspired Cyber Operations Center. It is a long-term engineering program rather than a collection of disconnected labs: each phase records its objectives, requirements, implementation, evidence, operational considerations, and lessons learned.

The program covers infrastructure and network security, monitoring and telemetry, endpoint engineering, detection engineering, incident response, automation, digital forensics, threat intelligence, identity, and cloud security.

## Current milestone

**Phase 10 — Identity Services is IN PROGRESS.**

The current identity baseline uses Windows Server 2025 on `DC01` with the `corp.lab.test` forest/domain. AD DS and DNS are operational and validated, including repaired AD-integrated DNS zones and working domain-controller locator records. The lab now has a protected OU and security-group structure, representative users, AGDLP-style administrative nesting, separate everyday/admin/Tier-0 identities, strengthened password and lockout settings, a working KDS/gMSA foundation, and a deliberately isolated legacy service identity for later Kerberoasting detection practice.

The next Phase 10 work is GPO-based privileged-logon control and hardening, followed by the Windows 11 domain client, Kali attacker VM, Wazuh/Sysmon identity telemetry, controlled attack exercises, incident-response documentation, and Greenbone/OpenVAS vulnerability-management practice.

**Phase 9 — File Access & Sync (Nextcloud Platform) is COMPLETE — September 10, 2026 EDT / September 11 UTC.**

Nextcloud 34.0.3 file access and sync is complete on Atlas, with Tailscale private access through a canonical HTTPS hostname and Caddy, tested Restic backup and database restore, Wazuh FIM alert validation, EICAR-tested ClamAV, working 2FA and outbound email, configured Windows 11 and Windows 10 clients, and successful reboot persistence. Galaxy S25 and Tab A11 Nextcloud onboarding are intentionally deferred and are not Phase 9 blockers.

**[Phase 8.5 — Linux Mint Cinnamon Workstation Migration](phases/phase-08-5-workstation-migration/README.md)** remains open but blocked until [Project Cerberus](https://github.com/scott-renny/project-cerberus-build) is funded and physically built. Phase 8.5 is a parallel hardware-dependent workstream rather than a sequential gate, so later independent phases may proceed while 8.5 remains visibly blocked.

## Program status

| Workstream | Status |
|---|---|
| Program governance and documentation framework | Complete |
| Foundation and base hardening | Complete |
| Container platform | Complete |
| Core network and security services | Complete |
| Backup and recovery | Complete |
| NET-WATCH network visibility | Complete |
| Telemetry backbone | Complete |
| Endpoint engineering | Complete |
| Linux Mint Cinnamon workstation migration | Blocked — awaiting Cerberus hardware |
| Nextcloud file access & sync | Complete |
| Identity services / Active Directory lab | In progress |
| Detection engineering | Planned |
| Incident response | Planned |
| Cloud integration | Planned |

Detailed status and sequencing are maintained in [ROADMAP.md](ROADMAP.md).

## Architecture

The documented environment combines:

- Ubuntu Server, Docker, Docker Compose, Tailscale/private access, and segmented networking
- Grafana, Prometheus, and NET-WATCH for monitoring and observability
- Wazuh, Zeek, Suricata, and Graylog for security operations
- Windows Server 2025 AD DS/DNS and an isolated identity attack lab for Phase 10
- Planned capabilities including MISP, TheHive, Cortex, Velociraptor, broader identity hardening, and cloud expansion

Technology names describe the planned program architecture and do not imply completed implementation unless a phase record and validation evidence support that status. See [ARCHITECTURE.md](ARCHITECTURE.md) for the high-level design.

## Documentation map

### Program governance

- [Roadmap](ROADMAP.md)
- [Architecture](ARCHITECTURE.md)
- [Security principles](SECURITY-PRINCIPLES.md)
- [Documentation standards](DOCUMENTATION-STANDARDS.md)
- [Risk register](RISK-REGISTER.md)
- [Data governance](docs/DATA-GOVERNANCE.md)
- [Device inventory](docs/DEVICE-INVENTORY.md)
- [Secrets management](docs/SECRETS-MANAGEMENT.md)
- [Portfolio policy](docs/PORTFOLIO-POLICY.md)
- [Architecture decision records](docs/decisions/README.md)

### Operational standards and resources

- [Operational governance mapping](docs/OPERATIONAL-GOVERNANCE-MAPPING.md)
- [Severity standard](docs/SEVERITY-STANDARD.md)
- [Evidence handling standard](docs/EVIDENCE-HANDLING-STANDARD.md)
- [Change management standard](docs/CHANGE-MANAGEMENT-STANDARD.md)
- [Adversary-emulation standard](docs/ADVERSARY-EMULATION-STANDARD.md)
- [Runbooks](runbooks/README.md)
- [Playbooks](playbooks/README.md)
- [Campaigns](campaigns/README.md)
- [Operational templates](templates/README.md)

### Implementation records

- [Phase 10 — Identity Services: IN PROGRESS](phases/phase-10-identity-services/README.md)
- [Phase 9 — File Access & Sync: COMPLETE](phases/phase-09-nextcloud/README.md)
- [Phase 0 — Program Governance](phases/phase-00-program-governance/README.md)
- [Phase 1 — Foundation](phases/phase-01-foundation/README.md)
- [Phase 2 — Base Hardening](phases/phase-02-base-hardening/README.md)
- [Phase 3 — Container Platform](phases/phase-03-container-platform/README.md)
- [Phase 4 — Core Network Security](phases/phase-04-core-network-security/README.md)
- [Phase 5 — Backup and Recovery](phases/phase-05-backup-recovery/README.md)
- [Phase 6 — NET-WATCH](phases/phase-06-netwatch/README.md)
- [Phase 7 — Telemetry Backbone](phases/phase-07-telemetry-backbone/README.md)
- [Phase 8 — Endpoint Engineering](phases/phase-08-endpoint-engineering/README.md)
- [Phase 8.5 — Workstation Migration](phases/phase-08-5-workstation-migration/README.md)

## Engineering principles

The program emphasizes security by design, defense in depth, least privilege, observability, repeatable validation, resilience, automation, and documentation as a first-class engineering deliverable.

A phase is complete only when its implementation, security review, validation evidence, and operational knowledge are documented.

## Related cloud engineering

The [Cloud Engineering Portfolio](https://github.com/scott-renny/cloud-engineering-portfolio) records completed AWS Budgets, EC2 lifecycle, Bedrock evaluation, and [Family IT Help Desk v0.1](https://github.com/scott-renny/cloud-engineering-portfolio/tree/main/aws/projects/family-it-helpdesk). These are standalone cloud outcomes; COC cloud telemetry and Ares integration remain planned. They do not change COC phase acceptance or mark cloud integration complete.

## Contributing and license

See [CONTRIBUTING.md](CONTRIBUTING.md) for change guidelines and [CHANGELOG.md](CHANGELOG.md) for version history. This project is licensed under the [MIT License](LICENSE).
