# Changelog

All notable changes to the **Cyber Operations Center Engineering Program** are documented in this file.

The project follows the principles of keeping changes transparent, traceable, and well documented throughout the engineering lifecycle.

---

## Unreleased

No unreleased changes currently recorded.

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
