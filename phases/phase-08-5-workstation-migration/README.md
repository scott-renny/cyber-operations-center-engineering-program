# Phase 8.5 — Windows 11 Pro Workstation Migration

> **Status:** Planned  
> **Predecessor:** [Phase 8 — Endpoint Engineering](../phase-08-endpoint-engineering/README.md)  
> **Successor:** Phase 9 — Nextcloud Platform

## Purpose

Migrate from the temporary Windows 10 workstation to a supported Windows 11 Pro workstation without weakening the clean, restore-tested state established in Phase 8.

## Entry gate

- Phase 8 completion approved
- Approved clean migration snapshot available
- Representative restore test passed
- Historical snapshots containing unsafe downloads clearly tagged
- Required software, accounts, and data inventory reviewed
- Replacement hardware supports TPM 2.0 and Secure Boot

## Planned sequence

1. Build Windows 11 Pro from trusted media.
2. Apply firmware, driver, Windows, Defender, and application updates.
3. Validate TPM 2.0 and Secure Boot.
4. Enable TPM-backed BitLocker and escrow recovery material outside the repository.
5. Apply endpoint hardening before restoring data.
6. Restore only from the approved Phase 8 source.
7. Scan restored content and validate representative files and applications.
8. Install Sysmon and enroll a permanent Wazuh identity.
9. Build only connectivity profiles required by the workstation use case.
10. Re-enroll hardware security keys deliberately and test recovery paths.
11. Revoke temporary Windows 10 registrations.
12. Sanitize and retire Windows 10 only after migration acceptance.

## Stop conditions

Stop if the approved snapshot cannot be restored, validation fails, malware is detected, BitLocker recovery material is not safely recorded, telemetry is absent, or required applications cannot be validated.

## Completion criteria

- Windows 11 Pro current and supported
- TPM 2.0, Secure Boot, and BitLocker validated
- Restored data scanned and sampled successfully
- Required applications and workflows tested
- Permanent monitoring identity active
- Hardware-key and recovery paths tested
- Temporary registrations revoked
- Legacy storage sanitized with recorded disposition
- Phase 8.5 completion report published
