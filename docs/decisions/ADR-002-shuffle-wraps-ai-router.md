# ADR-002: Shuffle wraps the AI router rather than replacing it

- **Status:** Accepted
- **Date:** 2026-07-27
- **Owner:** COC Program Owner
- **Related phase(s):** Phase 15
- **Related risk(s):** R-022

## Context

The COC requires orchestration, approvals, case integration, and auditable response while retaining the specialized routing/classification logic of the existing AI router.

## Decision

Use Shuffle as the orchestration and governance layer around the AI router. Shuffle coordinates triggers, approvals, integrations, audit records, and rollback; the router remains a bounded decision-support component.

## Alternatives Considered

Replace the router with Shuffle; run both independently; build a new orchestration platform.

## Rationale

Wrapping preserves specialized logic while adding visible workflow control and avoids an unnecessary rewrite.

## Security Implications

AI output is untrusted input. High-impact actions require scoped credentials, validation, human approval where appropriate, audit logs, and manual override.

## Consequences

Additional integration complexity, but clearer separation of responsibilities and safer automation.

## Validation

The related phase must link implementation evidence, test results, rollback/recovery validation, and any remaining risk before it is marked complete.

## Review Date or Trigger

Review when the related architecture materially changes, a control fails, or a new alternative changes the decision basis.
