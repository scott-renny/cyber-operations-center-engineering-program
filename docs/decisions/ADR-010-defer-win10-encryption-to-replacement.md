# ADR-010: Defer Windows 10 encryption to the replacement workstation

- **Status:** Superseded by [ADR-011](ADR-011-use-fedora-for-primary-workstation.md)
- **Date:** 2026-08-13
- **Owner:** COC Program Owner
- **Related phase(s):** Phase 8 and Phase 8.5
- **Related asset(s):** COC-WS-01

## Context

The legacy Windows 10 workstation does not expose a TPM. Its operating-system volume is unencrypted, but the system is a short-lived migration source scheduled for replacement by Windows 11 Pro. Enabling password-only BitLocker immediately before migration would introduce recovery and availability risk without establishing the intended hardware-backed trust boundary.

## Decision

Do not enable password-only BitLocker on the legacy workstation. Time-bound the exception through Phase 8.5. Require the replacement Windows 11 Pro workstation to validate TPM 2.0, Secure Boot, and TPM-backed BitLocker before production use.

## Alternatives Considered

Continue without an explicit exception; enable password-only BitLocker; add a discrete TPM if supported; or defer encryption to the supported replacement with compensating controls.

## Rationale

The selected approach protects migration reliability while making residual risk visible. The recovery source is encrypted, restore-tested, scanned, and independently monitored. The legacy workstation will not remain a permanent endpoint.

## Security Implications

Data on the powered-off legacy operating-system drive is not protected by full-disk encryption. Physical custody, limited remaining service life, current host protections, centralized telemetry, a clean encrypted backup, and prompt post-migration sanitization are required compensating controls.

## Consequences

Phase 8 can close with a documented exception. Phase 8.5 cannot close until TPM-backed BitLocker and recovery procedures are validated and legacy storage is sanitized.

## Validation

Verify that Windows reports no TPM and that Secure Boot is enabled. Verify the approved encrypted migration snapshot with a representative restore and clean malware scans. Record BitLocker validation and legacy-media disposition in Phase 8.5.

## Supersession

The encryption deferral and temporary Windows 10 compensating controls remain valid, but the Windows 11 Pro and BitLocker destination was replaced by the Fedora Workstation and LUKS2 decision in ADR-011.

## Review Date or Trigger

Review immediately if migration is delayed materially, physical custody changes, the legacy system is lost, the approved backup becomes unavailable, or the device must remain in service beyond Phase 8.5.
