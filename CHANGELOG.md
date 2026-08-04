# Changelog

All notable changes to the **Cyber Operations Center Engineering Program** are documented in this file.

The project follows the principles of keeping changes transparent, traceable, and well documented throughout the engineering lifecycle.

---

## Unreleased

### Added

- Phase 5 in-progress implementation and sanitized validation records
- Mount-safe rsync mirrors and encrypted Restic snapshots with retention and integrity checking
- Authenticated Samba backup target restricted to trusted LAN and VPN sources
- Wazuh backup-health rules validated for both success and failure outcomes
- Scheduled Windows 10 Core, Downloads, and powered-off VirtualBox backups
- Encrypted server-side snapshots and restore testing for the Windows backup mirror
- Draft Docker service-health, Dockge deployment, and bounded container-log inspection runbooks for the completed Phase 3 platform
- Draft firewall rollback and Wazuh alert-triage runbooks for controls implemented in Phase 4

### Changed

- Advanced Phase 5 from planned to in progress after server-side recovery validation
- Completed Windows 10 desktop scheduling, direct restore, encrypted snapshot, encrypted restore, and monitoring validation; Windows 11 laptop coverage remains pending
- Corrected the backup-monitoring design to match pre-decoded syslog program names rather than the unrelated process-monitoring parent rule
- Linked implemented Phase 3–4 capabilities to standalone governed procedures
- Kept each new runbook at Draft until its dedicated positive, failure, and rollback validation gate passes
- Clarified the distinction between a completed capability and a validated operational procedure

### Security

- Preserved restrictive ownership on the Wazuh credential archive instead of elevating backup automation to root
- Limited Samba to authenticated access from trusted network sources
- Prevented overlapping Windows jobs and blocked VirtualBox copies while a VM is running
- Excluded live addresses, filesystem UUIDs, disk serials, repository identifiers, secrets, raw backups, and unredacted screenshots from Phase 5 public evidence
- Limited public procedures to sanitized examples and approved asset identifiers
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
