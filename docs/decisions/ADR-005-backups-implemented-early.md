# ADR-005: Backups implemented early

- **Status:** Accepted
- **Date:** 2026-07-27
- **Owner:** COC Program Owner
- **Related phase(s):** Phase 5
- **Related risk(s):** R-024, R-025

## Context

Strict functional grouping placed mature backup work later, but configuration and evidence could be lost throughout earlier phases.

## Decision

Establish backup and restore capability early, before the environment accumulates irreplaceable configuration, telemetry, and documentation.

## Alternatives Considered

Wait until a later resilience phase; rely on Git only; take ad hoc manual copies.

## Rationale

Recovery must exist before major destructive or complex changes. This reduces cumulative program risk even if it changes the thematic ordering.

## Security Implications

Backup credentials and repositories are restricted, integrity is monitored, and restores—not only backup jobs—are tested.

## Consequences

Adds early setup work and storage use; reduces catastrophic-loss risk and supports the Phase 1 wipe gate.

## Validation

The related phase must link implementation evidence, test results, rollback/recovery validation, and any remaining risk before it is marked complete.

## Review Date or Trigger

Review when the related architecture materially changes, a control fails, or a new alternative changes the decision basis.
