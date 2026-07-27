# ADR-001: Full wipe and clean-slate rebuild

- **Status:** Accepted
- **Date:** 2026-07-27
- **Owner:** COC Program Owner
- **Related phase(s):** Phase 1
- **Related risk(s):** R-021

## Context

The existing environment accumulated implementation gaps, undocumented dependencies, inconsistent configuration, and portfolio evidence that could not reliably prove the final state.

## Decision

Rebuild the COC environment from a documented baseline rather than incrementally patching the existing deployment. Preserve only reviewed exports, inventories, screenshots, lessons, and backups required for reconstruction or historical evidence.

## Alternatives Considered

Incremental repair; parallel greenfield environment; leave the current system unchanged.

## Rationale

A clean baseline improves trust in validation, removes configuration drift, and makes every subsequent state traceable. The destructive nature of the decision is controlled through a Phase 1 pre-wipe gate.

## Security Implications

Before wiping: inventory assets and services, export configurations, capture evidence, test backups, record required secrets without publishing them, and verify recovery paths.

## Consequences

Higher upfront effort and temporary loss of availability; substantially stronger documentation, repeatability, and long-term maintainability.

## Validation

The related phase must link implementation evidence, test results, rollback/recovery validation, and any remaining risk before it is marked complete.

## Review Date or Trigger

Review when the related architecture materially changes, a control fails, or a new alternative changes the decision basis.
