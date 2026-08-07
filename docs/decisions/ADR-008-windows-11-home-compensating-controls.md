# ADR-008: Use compensating controls on Windows 11 Home

- **Status:** Accepted
- **Date:** 2026-08-07
- **Owner:** COC Program Owner
- **Related phase(s):** Phase 8
- **Related asset(s):** COC-LT-01

## Context

COC-LT-01 runs Windows 11 Home, which lacks parts of the centrally managed enterprise policy surface available in higher editions and managed environments.

## Decision

Accept Windows 11 Home for this phase and apply a documented compensating baseline: TPM 2.0, Secure Boot, Windows Hello, Defender, Tamper Protection, Smart App Control, Controlled Folder Access, Windows Firewall, WireGuard network controls, Wazuh monitoring, and browser hardening.

## Alternatives Considered

Upgrade the operating-system edition immediately; defer endpoint use; accept the platform without additional controls; apply layered compensating controls.

## Rationale

The implemented controls materially reduce risk without overstating Home-edition capability. Wazuh and repeatable validation add visibility where centralized enforcement is limited.

## Security Implications

Configuration drift is more likely without a full enterprise management plane. Control state must be periodically reviewed, and exceptions require explicit documentation.

## Consequences

Some enterprise hardening recommendations cannot be represented as enforced. A future edition upgrade or endpoint-management phase may replace parts of this decision.

## Validation

Confirm each named control independently and validate Wazuh visibility. Record unavailable controls as limitations rather than completed work.

## Review Date or Trigger

Review when the Windows edition changes, centralized endpoint management is introduced, or the compensating baseline fails validation.
