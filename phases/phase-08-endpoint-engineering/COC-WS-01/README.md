# COC-WS-01 — Windows 10 Pre-Migration Hardening

> **Status:** Complete with documented exception  
> **Completion date:** 2026-08-13  
> **Platform:** Windows 10 Pro 22H2  
> **Lifecycle:** Temporary migration source; retirement planned in Phase 8.5

## Purpose

Place the legacy workstation in a known-good, monitored, recoverable state before the Fedora Workstation migration begins.

## Completed controls

- Current Windows 10 Extended Security Updates and Microsoft Defender intelligence
- Secure Boot enabled
- Defender real-time, behavior, IOAV, cloud, tamper, PUA, and network protections
- Windows Firewall enabled for Domain, Private, and Public profiles
- UAC secure-desktop prompting and a 15-minute inactivity lock
- SMB1, insecure SMB guest access, and Windows PowerShell 2 disabled
- Remote Desktop disabled; Remote Registry disabled; no exposed WinRM listener
- Unneeded guest account disabled and password requirement corrected for the primary local account
- Privacy and cross-device activity settings reduced
- Sysmon installed with a validated configuration
- Wazuh agent enrolled and forwarding Sysmon events
- Full antimalware remediation and clean rescans
- Encrypted, versioned, restore-tested migration snapshot approved

## Documented exceptions

### No TPM and no full-disk encryption

The legacy motherboard does not expose a TPM. The operating-system volume remains unencrypted. Enabling password-only BitLocker immediately before retirement would add recovery and migration risk without providing the intended hardware-backed trust boundary.

The exception is time-bounded to Phase 8.5 and uses physical control, current host protections, centralized monitoring, a clean encrypted recovery copy, and prompt retirement as compensating controls. ADR-010 recorded the original deferral and is now superseded by [ADR-011](../../../docs/decisions/ADR-011-use-fedora-for-primary-workstation.md), which selects Fedora Workstation and LUKS2-backed encryption for the replacement.

### Controlled Folder Access in Audit mode

Audit data showed legitimate PowerShell-based engineering automation writing to protected document paths. Controlled Folder Access therefore remains in Audit mode until the workflows can be narrowed or restructured. PowerShell was not broadly trusted because that would weaken ransomware protection.

## Documentation

- [Platform hardening](01-platform-hardening.md)
- [Monitoring](02-monitoring.md)
- [Backup and malware remediation](03-backup-and-malware-remediation.md)
- [Validation](04-validation.md)
- [Completion report](PHASE-08-COMPLETION.md)
