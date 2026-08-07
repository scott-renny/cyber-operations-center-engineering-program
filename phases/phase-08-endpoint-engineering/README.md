# Phase 8 — Endpoint Engineering

> **Status:** Complete for COC-LT-01  
> **Completed:** 2026-08-07  
> **Scope:** COC-LT-01 only  
> **Next phase:** Phase 9 — Nextcloud Platform

## Purpose

Establish and validate a defense-in-depth endpoint baseline for COC-LT-01, a roaming Windows 11 Home laptop used to administer and observe the Cyber Operations Center.

## Completed capabilities

- Hardware-backed platform security through verified TPM 2.0 and Secure Boot
- Microsoft Defender, Tamper Protection, Smart App Control, Controlled Folder Access, and Windows Firewall review
- Windows Hello PIN backed by the local TPM
- WireGuard split-tunnel and full-tunnel profiles, including an untrusted-network kill switch and controlled DNS
- Wazuh endpoint enrollment, file-integrity monitoring, real-time event validation, Security Configuration Assessment, and MITRE ATT&CK context
- Firefox privacy and security hardening with uBlock Origin, Cookie AutoDelete, and Bitwarden
- Hardware security-key protection completed for Microsoft and Bitwarden
- Removal of unnecessary public HTTP/HTTPS exposure, leaving WireGuard as the remote-access boundary

## Documentation

- [COC-LT-01 overview](COC-LT-01/README.md)
- [Endpoint hardening](COC-LT-01/01-endpoint-hardening.md)
- [WireGuard](COC-LT-01/02-wireguard.md)
- [Windows security](COC-LT-01/03-windows-security.md)
- [Wazuh agent](COC-LT-01/04-wazuh-agent.md)
- [Browser hardening](COC-LT-01/05-browser-hardening.md)
- [Identity security](COC-LT-01/06-identity-security.md)
- [Firewall changes](COC-LT-01/07-firewall.md)
- [Validation results](COC-LT-01/08-validation.md)
- [Completion report](COC-LT-01/PHASE-08-COMPLETION.md)

## Related decisions

- [ADR-007 — Require VPN-only remote administration](../../docs/decisions/ADR-007-vpn-only-remote-administration.md)
- [ADR-008 — Use compensating controls on Windows 11 Home](../../docs/decisions/ADR-008-windows-11-home-compensating-controls.md)
- [ADR-009 — Use workstation-associated hardware security keys](../../docs/decisions/ADR-009-workstation-associated-hardware-security-keys.md)

## Scope boundary

This record describes only completed Phase 8 work on COC-LT-01. It does not represent other endpoints as hardened. GitHub, Google, AWS, Amazon, the secondary hardware key, Sysmon, custom detection rules, and endpoint-management work remain deferred.
