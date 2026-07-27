# ADR-003: Software segmentation before Omada hardware

- **Status:** Accepted
- **Date:** 2026-07-27
- **Owner:** COC Program Owner
- **Related phase(s):** Phases 4 and 22
- **Related risk(s):** R-009

## Context

Managed Omada VLAN hardware is planned but not yet available. Waiting would block early service deployment and security learning.

## Decision

Use documented host firewalls, service binding, access lists, and logical trust zones now; migrate enforcement to Omada VLANs in Phase 22.

## Alternatives Considered

Wait for hardware; deploy unmanaged flat network; purchase alternate hardware.

## Rationale

Allows progress at zero immediate cost while preserving a migration path and acknowledging weaker isolation.

## Security Implications

Software controls do not equal hardware-enforced segmentation. Sensitive and intentionally vulnerable systems require additional isolation and monitoring.

## Consequences

Controls must be reviewed during migration; temporary rules may create technical debt.

## Validation

The related phase must link implementation evidence, test results, rollback/recovery validation, and any remaining risk before it is marked complete.

## Review Date or Trigger

Review when the related architecture materially changes, a control fails, or a new alternative changes the decision basis.
