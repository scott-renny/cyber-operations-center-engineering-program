# Architecture Decision Records

ADRs preserve the context and reasoning for consequential COC architecture choices.

## Status values

Proposed, Accepted, Superseded, Deprecated, Rejected.

## Rules

- Create an ADR when credible alternatives exist and the decision affects architecture, security, operations, cost, recovery, or future phases.
- Do not use ADRs for routine commands or reversible local preferences.
- Accepted ADRs are immutable except for typo/link corrections. Changed decisions receive a new ADR that supersedes the old one.
- Link related risks, phases, validation, and operational procedures.

## Index

- [ADR-001 — Full wipe and clean-slate rebuild](ADR-001-full-wipe-clean-slate-rebuild.md)
- [ADR-002 — Shuffle wraps the AI router](ADR-002-shuffle-wraps-ai-router.md)
- [ADR-003 — Software segmentation before Omada hardware](ADR-003-software-segmentation-before-omada.md)
- [ADR-004 — Pi-hole group-API kill switch](ADR-004-pihole-group-api-kill-switch.md)
- [ADR-005 — Backups implemented early](ADR-005-backups-implemented-early.md)
- [ADR-006 — Core network and security services remain merged](ADR-006-core-network-security-merged.md)
- [ADR-007 — Require VPN-only remote administration](ADR-007-vpn-only-remote-administration.md)
- [ADR-008 — Use compensating controls on Windows 11 Home](ADR-008-windows-11-home-compensating-controls.md)
- [ADR-009 — Use workstation-associated hardware security keys](ADR-009-workstation-associated-hardware-security-keys.md)
- [ADR-010 — Defer Windows 10 encryption to the replacement workstation](ADR-010-defer-win10-encryption-to-replacement.md) — Superseded by ADR-011
- [ADR-011 — Use Fedora Workstation for the replacement workstation](ADR-011-use-fedora-for-primary-workstation.md)
