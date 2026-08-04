# Changelog

All notable changes to the **Cyber Operations Center Engineering Program** are documented in this file.

The project follows the principles of keeping changes transparent, traceable, and well documented throughout the engineering lifecycle.

---

## Version 1.8.0 - Phase 7 Telemetry Backbone (2026-08-04)

### Added

- Phase 7 telemetry-backbone completion record
- Zeek connection, DNS, and TLS metadata alongside Suricata
- Prometheus collection from node_exporter and cAdvisor
- Grafana Node Exporter Full and cAdvisor dashboards
- Custom Pi-hole, Wazuh alert-volume, backup-age, and collector-health metrics
- COC Operations Overview Grafana dashboard
- Graylog 7, MongoDB, and a dedicated Graylog Data Node
- Dedicated COC General Logs index set and Syslog UDP input
- Persistent NET-WATCH journal forwarding into Graylog
- Private Caddy HTTPS endpoints and portal tiles for the observability services

### Changed

- Advanced the current milestone to Phase 8 — Endpoint Engineering
- Replaced phase-number-focused portal labels with operational service categories
- Bound native observability and search services locally where practical
- Isolated Graylog search-backend ports from Wazuh
- Configured single-node Graylog index sets with one primary shard and zero replicas
- Promoted backup success, DNS statistics, and Wazuh alert volume into visible operational metrics

### Security

- Preserved Caddy as the private HTTPS management plane
- Limited management access to approved LAN and VPN networks
- Kept Pi-hole credentials in a protected Docker secret
- Ran the custom metrics collector as a constrained systemd oneshot service
- Used atomic Prometheus textfile metric publication
- Added no new detection or automated-response logic during the telemetry phase
- Excluded credentials, live addresses, private certificates, device identifiers, and raw logs from public documentation

---

## Version 1.7.0 - Phase 6 NET-WATCH (2026-08-03)

### Added

- Phase 6 NET-WATCH completion record
- Production device discovery, classification, assignment, and profile management
- Per-profile schedules, daily budgets, manual kill switches, and DNS content policies
- Pi-hole v6 group-based enforcement using a dedicated safety control group and managed deny-all rule
- Wazuh alert visibility with MITRE ATT&CK context
- Private Caddy HTTPS access, local DNS, Gunicorn, systemd, and health diagnostics

### Changed

- Advanced the current milestone to Phase 7 — Telemetry Platform
- Replaced development-server operation with a hardened Gunicorn service
- Preserved the existing Caddy management plane instead of introducing a competing Nginx listener
- Enabled Pi-hole as the network DNS service and connected NET-WATCH to per-profile enforcement
- Added assigned/unassigned and device-type filtering plus expanded device icons

### Security

- Kept the API bound to localhost behind private HTTPS
- Protected runtime settings in a root-managed environment file
- Scoped DNS blocking to explicit Pi-hole profile groups instead of globally disabling Pi-hole
- Added reconciliation diagnostics, safe failure behavior, and checks for missing, disabled, default, or foreign groups
- Excluded credentials, device identifiers, addresses, and private certificate material from public documentation

---

## Version 1.6.0 - Phase 5 Backup and Recovery (2026-08-01)

### Added

- Phase 5 backup-and-recovery completion record
- Automated file protection and encrypted snapshot retention
- Restore verification and documented recovery procedures
- Backup monitoring and security-event visibility

### Changed

- Advanced the current milestone to Phase 6 — NET-WATCH
- Promoted recovery testing from an assumed capability to a validated engineering requirement

### Security

- Kept backup credentials and recovery secrets outside the public repository
- Documented sanitization requirements for backup evidence and restore records

---

## Unreleased

### Added

- Draft backup-failure, repository-integrity, file-restore, full-system-restore, NET-WATCH health, logging-pipeline, and end-to-end telemetry runbooks for completed Phases 5–7
- Draft DNS disruption, denial-of-service, ransomware, and backup-repository-compromise playbooks with explicit exercise gates
- Prioritized validation queues for the runbook and playbook libraries
- Draft Docker service-health, Dockge deployment, and bounded container-log inspection runbooks for the completed Phase 3 platform
- Managed Windows laptop onboarding validation for local DNS and dedicated Ed25519 SSH access
- Draft firewall rollback and Wazuh alert-triage runbooks for controls implemented in Phase 4

### Changed

- Added stable document IDs across the full runbook and playbook roadmaps
- Advanced implemented Phase 5–7 procedures from Planned to Draft without overstating standalone validation
- Clarified that completed phase capability evidence does not automatically promote a standalone procedure or incident playbook
- Linked implemented Phase 3–4 capabilities to standalone governed procedures
- Recorded explicit OpenSSH client identity mapping for the managed laptop's non-default key filename
- Kept each new runbook at Draft until its dedicated positive, failure, and rollback validation gate passes
- Clarified the distinction between a completed capability and a validated operational procedure

### Security

- Limited public procedures to sanitized examples and approved asset identifiers
- Withheld laptop addresses, public-key material, source ports, and raw authentication logs from published evidence
- Kept live addresses, credentials, secrets, repository details, and private operational values outside the public documents

---

## Version 1.5.0 - Phase 4 Core Network and Security Services (2026-07-31)

### Added

- Phase 4 implementation and completion record
- Sanitized validation evidence for addressing, WireGuard, Wazuh, Pi-hole, ClamAV, UFW, and service health
- WireGuard remote-access VPN with mobile-peer validation
- Wazuh all-in-one monitoring and local security telemetry
- Pi-hole DNS filtering for controlled workstation and VPN pilots
- ClamAV malware detection with a scheduled targeted scan
- Prepared Suricata rules and Wazuh EVE JSON integration

### Changed

- Advanced the current milestone to Phase 5 — Backup and Recovery
- Restricted SSH, Caddy, Dockge, Wazuh, and Pi-hole access to trusted LAN and VPN sources
- Replaced stale local name-resolution overrides with Pi-hole local DNS
- Documented Project Olympus as the controlled path for wired Ethernet, VLANs, DHCP migration, and household-wide DNS

### Security

- Disabled UPnP, WPS, DMZ, guest networking, smart-device networking, and dynamic DNS
- Enabled router SPI, anti-DoS protection, high firewall policy, and WAN ping discard
- Removed stale port forwarding and retained only the WireGuard UDP rule
- Validated ClamAV-to-Wazuh malware alerting with the harmless EICAR test
- Kept Suricata inactive after Wi-Fi capture disrupted connectivity
- Excluded credentials, keys, endpoints, live addresses, MAC addresses, and raw screenshots from the public record

---

## Version 1.4.1 - Operational Documentation Foundation (2026-07-30)

### Added

- Standalone severity, evidence-handling, change-management, and adversary-emulation standards
- Governed runbook, playbook, and campaign indexes with phase-based validation gates
- Operational-document migration and status-promotion rules
- Reusable runbook, playbook, campaign, incident-case, evidence-log, validation-record, Rules of Engagement, and post-incident-review templates

### Changed

- Expanded the repository documentation index and structure
- Distinguished planned procedures from lab-validated and operational procedures
- Mapped future operational documents to the phases that provide their required capabilities

### Security

- Required explicit authorization and stop conditions for adversary emulation
- Required evidence integrity, custody, sanitization, and publication review
- Prevented untested procedures and campaigns from being represented as validated
- Required rollback, recovery, and residual-risk ownership for operational changes

---

## Version 1.4.0 - Phase 3 Container Platform and Service Management (2026-07-30)

### Added

- Phase 3 implementation and completion record
- Sanitized validation evidence for Docker, Compose, Dockge, Caddy, UFW, and log rotation
- Reusable frontend/backend network example
- Sanitized Docker daemon log-rotation configuration
- Sanitized Caddy reverse-proxy example for Dockge
- Container naming, labeling, and Compose secrets standards

### Changed

- Advanced the current milestone to Phase 4 — Core Network and Security Services
- Updated the architecture with the implemented container management plane
- Marked Phase 3 complete in the engineering roadmap
- Bound Dockge's native HTTP listener to localhost
- Routed Dockge access through the existing private Caddy HTTPS gateway

### Security

- Limited the Dockge HTTPS endpoint to the trusted LAN
- Treated Docker group membership and Docker socket access as privileged administration
- Applied bounded container log retention to reduce disk-exhaustion risk
- Defined an internal backend network for private-only container communication
- Kept Swarm disabled to avoid mixing orchestration models solely for secret storage
- Excluded credentials, secrets, live addresses, certificate details, image digests, and raw screenshots from the public record

---

## Version 1.3.0 - Phase 2 Base Hardening and Operations Portal (2026-07-30)

### Added

- Phase 2 implementation and completion record
- Sanitized validation evidence for SSH, UFW, Fail2Ban, AppArmor, Auditd, updates, and Caddy
- Private Caddy HTTPS operations portal
- Sanitized Caddy and asset-registry configuration examples
- Standardized asset IDs for the server, workstation, and planned laptop

### Changed

- Advanced the current milestone to Phase 3 — Container Platform
- Updated the repository structure and documentation index for Phase 2
- Replaced SSH password administration with Ed25519 key authentication
- Applied all pending operating-system and security updates

### Security

- Disabled SSH password authentication, keyboard-interactive authentication, and root login
- Applied a persistent default-deny inbound UFW policy
- Enabled a one-hour Fail2Ban SSH ban policy
- Enabled Auditd and validated AppArmor enforcement state
- Kept the operational asset registry outside the public web root
- Verified the local Caddy CA fingerprint before current-user trust installation
- Excluded live addresses, private keys, certificate fingerprints, and raw screenshots from the public record

---

## Version 1.2.0 - Phase 1 Foundation (2026-07-27)

### Added

- Phase 1 full-wipe and clean-slate rebuild completion record
- Sanitized Phase 1 validation evidence
- Documented Ubuntu Server 24.04.4 LTS baseline for Atlas (`coc-srv-01`)
- Broadcom BCM4352 wireless-driver recovery and troubleshooting record
- OpenSSH installation and remote-access validation
- Laptop lid, idle, suspend, hibernate, and hybrid-sleep controls

### Changed

- Marked Phase 1 complete in the engineering roadmap
- Advanced the current milestone to Phase 2 — Base Hardening
- Corrected the prior-environment timeline from one year to several months
- Retained the minimized Ubuntu Server profile as the approved baseline

### Security

- Kept the external backup HDD physically outside the destructive wipe scope
- Sanitized live IP addresses, MAC addresses, identifiers, serials, credentials, and reflective screenshots from public evidence
- Recorded SSH password authentication as a temporary bootstrap condition pending Phase 2 key-based hardening
- Documented public DNS fallback and delayed Pi-hole cutback as controlled deferred work

---

## Version 1.1.0 - Phase 0 Governance Foundation (2026-07-27)

### Added

- Data governance and public sanitization policy
- Device inventory schema
- Secrets, certificate, and key management standard
- Operational governance mapping for runbooks, playbooks, and campaign sequences
- ADR framework and ADR-001 through ADR-006
- Formal Phase 0 completion and Phase 1 entry gate

### Changed

- Centralized known technical, operational, privacy, evidence, and recovery risks
- Promoted runbook/playbook operating rules into enforceable program governance

### Security

- Established classification, retention, evidence integrity, secret rotation, redaction, authorized-testing, and stop-condition requirements

---

## Version 1.0.0 - Repository Foundation

### Added

- Initial repository structure
- Program README
- Engineering roadmap
- System architecture documentation
- Security engineering principles
- Documentation standards
- Contribution guidelines
- Changelog

---

## Future Releases

Future updates will document significant engineering milestones, including but not limited to:

- New infrastructure deployments
- Security improvements
- Detection engineering enhancements
- Automation capabilities
- Network architecture changes
- Incident response improvements
- Documentation updates
- Breaking changes
- Major refactoring efforts

---

## Changelog Guidelines

Entries should describe **what changed** and **why it changed**, not simply list modified files.

Significant updates should be grouped into categories such as:

### Added

New features, infrastructure, or documentation.

### Changed

Updates to existing functionality, architecture, or documentation.

### Improved

Enhancements that increase reliability, performance, security, or usability.

### Fixed

Corrections to documentation, configuration, deployment, or functionality.

### Removed

Features, services, or documentation that have been intentionally retired.

### Security

Security improvements, hardening measures, vulnerability mitigations, or policy changes.

---

## Versioning Strategy

This repository uses semantic versioning for significant milestones.

- **Major** – Architectural redesigns or major capability expansions.
- **Minor** – New phases, services, or significant features.
- **Patch** – Documentation corrections, bug fixes, and minor improvements.

Example:

- 1.0.0
- 1.1.0
- 1.2.0
- 2.0.0

---

## Engineering Philosophy

A complete changelog provides historical context for the evolution of the Cyber Operations Center Engineering Program.

Maintaining an accurate record of changes supports:

- Traceability
- Documentation quality
- Operational awareness
- Knowledge transfer
- Continuous improvement

Every significant change should leave a documented history.
