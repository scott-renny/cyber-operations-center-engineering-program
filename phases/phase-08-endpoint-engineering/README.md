# Phase 8 — Endpoint Engineering

> **Status:** Complete  
> **Completion date:** 2026-08-13  
> **Next workstream:** [Phase 8.5 — Windows 11 Pro Workstation Migration](../phase-08-5-workstation-migration/README.md)  
> **Phase 9:** Not started

## Purpose

Establish, validate, and document defense-in-depth security baselines for the program's user endpoints without overstating controls a platform cannot support.

## Workstream status

| Workstream | Status | Documentation |
|---|---|---|
| COC-LT-01 | Complete | [Laptop record](COC-LT-01/README.md) |
| COC-WS-01 | Complete with encryption exception | [Windows 10 record](COC-WS-01/README.md) |
| Galaxy S25 | Complete; identity-key follow-up deferred | [Phone record](GALAXY-S25/README.md) |
| Galaxy Tab A11 | Complete; NFC capability not asserted | [Tablet record](GALAXY-TAB-A11/README.md) |

Mobile labels are descriptive portfolio labels, not authoritative private inventory identifiers. Addresses, serial numbers, keys, account identifiers, recovery material, and raw screenshots remain outside this repository.

## Phase outcomes

- COC-LT-01 retained its validated Windows 11 Home, WireGuard, Wazuh, browser, and hardware-key baseline.
- COC-WS-01 received a full pre-migration hardening pass, Sysmon, Wazuh, malware remediation, and restore-tested backup approval.
- Phone and tablet baselines were operator-validated for updates, secure locking, Samsung and Android protections, permissions, recovery, and protected connectivity.
- Platform differences and deferred identity work are documented explicitly.
- Phase 8.5 remains separate so the old workstation is a known-good, recoverable migration source.

## Documentation

- [COC-LT-01 completion](COC-LT-01/PHASE-08-COMPLETION.md)
- [COC-WS-01 overview](COC-WS-01/README.md)
- [Galaxy S25 overview](GALAXY-S25/README.md)
- [Galaxy Tab A11 overview](GALAXY-TAB-A11/README.md)
- [Phase 8 completion report](PHASE-08-COMPLETION.md)
- [Phase 8.5 migration plan](../phase-08-5-workstation-migration/README.md)

## Related decisions

- [ADR-007 — Require VPN-only remote administration](../../docs/decisions/ADR-007-vpn-only-remote-administration.md)
- [ADR-008 — Windows 11 Home compensating controls](../../docs/decisions/ADR-008-windows-11-home-compensating-controls.md)
- [ADR-009 — Workstation-associated hardware security keys](../../docs/decisions/ADR-009-workstation-associated-hardware-security-keys.md)
- [ADR-010 — Defer Windows 10 encryption](../../docs/decisions/ADR-010-defer-win10-encryption-to-replacement.md)

## Known limitations and deferred work

- COC-WS-01 has no TPM and remains unencrypted under a time-bounded exception.
- Controlled Folder Access remains in Audit mode on COC-WS-01; PowerShell was not broadly allow-listed.
- Additional FIDO2 enrollment and account-by-account inventory work are deferred.
- Tablet NFC availability and NFC security-key use are not claimed.
- Centralized endpoint management is a later capability.
