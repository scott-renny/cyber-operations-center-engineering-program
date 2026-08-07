# ADR-009: Use workstation-associated hardware security keys

- **Status:** Accepted
- **Date:** 2026-08-07
- **Owner:** COC Program Owner
- **Related phase(s):** Phase 8
- **Related asset(s):** COC-LT-01

## Context

High-value accounts require phishing-resistant authentication. Routine dependence on a single shared key across workstations creates operational coupling, while enrolling only one key creates a recovery weakness.

## Decision

Associate an approved primary hardware security key with each workstation for routine use. Permit high-value accounts to enroll multiple approved workstation-associated keys for resilience. Record assignment and enrollment status without storing secrets.

## Alternatives Considered

Use one shared hardware key for every workstation; use only authenticator applications; maintain one key with no redundant factor; use workstation-associated primary keys with controlled multi-key enrollment.

## Rationale

The selected approach combines phishing resistance, workstation independence, and recoverability. It also produces a clear inventory model as the environment grows.

## Security Implications

Key PINs, recovery codes, and account identifiers must remain outside the public repository. A lost or suspect key requires prompt revocation and inventory review. Existing recovery methods remain until redundant access is verified.

## Consequences

Each critical service requires deliberate enrollment, testing, lifecycle tracking, and periodic review. Phase 8 completed Microsoft and Bitwarden enrollment for the COC-LT-01 key; all other services and the secondary key remain deferred.

## Validation

After each enrollment, use a private session to prove that authentication requires the intended physical key. Test a secondary approved path before removing an existing recovery method.

## Review Date or Trigger

Review after key loss, suspected compromise, workstation retirement, account-recovery failure, or a material change in passkey support.
