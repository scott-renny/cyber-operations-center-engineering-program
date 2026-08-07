# Phase 8 — Endpoint Engineering

> **Status:** In Progress  
> **Current completed workstream:** COC-LT-01  
> **Phase completion date:** Not yet complete  
> **Next phase:** Phase 9 — Nextcloud Platform (not started)

## Purpose

Establish and validate defense-in-depth security baselines for the program's user endpoints. Phase 8 is complete only after the Windows 10 PC, mobile phone, and tablet workstreams join the completed COC-LT-01 workstream.

## Workstream status

| Workstream | Status | Documentation |
|---|---|---|
| COC-LT-01 | Complete | [Completed laptop record](COC-LT-01/README.md) |
| Windows 10 PC | Planned | Implementation, validation, and asset-specific documentation pending |
| Mobile phone | Planned | Implementation, validation, and asset-specific documentation pending |
| Tablet | Planned | Implementation, validation, and asset-specific documentation pending |

Asset identifiers for the remaining devices will be added only after they are confirmed. No control is considered implemented on those devices until it has been applied and validated.

## Completed COC-LT-01 capabilities

- Hardware-backed platform security through verified TPM 2.0 and Secure Boot
- Microsoft Defender, Tamper Protection, Smart App Control, Controlled Folder Access, and Windows Firewall review
- Windows Hello PIN backed by the local TPM
- WireGuard split-tunnel and full-tunnel profiles, including an untrusted-network kill switch and controlled DNS
- Wazuh endpoint enrollment, file-integrity monitoring, real-time event validation, Security Configuration Assessment, and MITRE ATT&CK context
- Firefox privacy and security hardening with uBlock Origin, Cookie AutoDelete, and Bitwarden
- Hardware security-key protection completed for Microsoft and Bitwarden
- Removal of unnecessary public HTTP/HTTPS exposure, leaving WireGuard as the remote-access boundary

## COC-LT-01 documentation

- [COC-LT-01 overview](COC-LT-01/README.md)
- [Endpoint hardening](COC-LT-01/01-endpoint-hardening.md)
- [WireGuard](COC-LT-01/02-wireguard.md)
- [Windows security](COC-LT-01/03-windows-security.md)
- [Wazuh agent](COC-LT-01/04-wazuh-agent.md)
- [Browser hardening](COC-LT-01/05-browser-hardening.md)
- [Identity security](COC-LT-01/06-identity-security.md)
- [Firewall changes](COC-LT-01/07-firewall.md)
- [Validation results](COC-LT-01/08-validation.md)
- [COC-LT-01 completion report](COC-LT-01/PHASE-08-COMPLETION.md)

## Remaining Phase 8 work

Each remaining workstream requires an approved scope, implementation record, security review, validation results, limitations, and sanitized evidence before it can be marked complete:

- Windows 10 PC
- Mobile phone
- Tablet
- Phase-wide completion review after all endpoint workstreams are complete

## Related decisions

- [ADR-007 — Require VPN-only remote administration](../../docs/decisions/ADR-007-vpn-only-remote-administration.md)
- [ADR-008 — Use compensating controls on Windows 11 Home](../../docs/decisions/ADR-008-windows-11-home-compensating-controls.md)
- [ADR-009 — Use workstation-associated hardware security keys](../../docs/decisions/ADR-009-workstation-associated-hardware-security-keys.md)

## Scope boundary

The current implementation record applies only to COC-LT-01. It does not represent the Windows 10 PC, mobile phone, tablet, or any other endpoint as hardened. GitHub, Google, AWS, Amazon, the secondary hardware key, Sysmon, custom detection rules, and endpoint-management work also remain deferred.
