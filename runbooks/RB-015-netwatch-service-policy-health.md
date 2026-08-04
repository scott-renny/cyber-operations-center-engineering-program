# Runbook: NET-WATCH Service and Policy Health

**Document ID:** RB-015  
**Status:** Draft  
**Owner:** COC Operations  
**Related phase:** 6  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose

Verify NET-WATCH availability and confirm that profile-based Pi-hole policy is reconciled safely without globally disabling DNS filtering.

## Trigger and scope

- Trigger: dashboard health failure, unexpected profile access, reconciliation warning, service change, or scheduled review.
- Authorized systems: NET-WATCH API and dashboard, Gunicorn/systemd service, Caddy endpoint, Pi-hole v6 groups and the dedicated managed control rule.
- Exclusions: the Pi-hole default group, foreign rules, and global filtering disablement.
- Required access: NET-WATCH operations and least-privilege Pi-hole administration.

## Prerequisites

- Record expected profile, schedule, budget, manual-switch, group, and rule state.
- Confirm private management access and a current configuration recovery point.
- Preserve reconciliation warnings before making changes.
- Do not publish device identifiers, addresses, credentials, or certificate material.

## Procedure

1. Confirm the NET-WATCH systemd/Gunicorn service and localhost API health.
2. Confirm the private Caddy HTTPS endpoint responds.
3. Review recent bounded service logs and Graylog events.
4. Confirm Pi-hole is available and filtering remains enabled.
5. Verify the dedicated control group is empty and the managed deny-all rule is present.
6. Confirm no default, disabled, missing, or foreign group is targeted.
7. Compare desired profile state with actual Pi-hole group associations.
8. Exercise one approved test profile through allowed and blocked states.
9. Confirm schedule, budget, and manual kill switch produce the expected profile-only policy.
10. Return the profile to its approved baseline and verify warning-free reconciliation.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Default or foreign group would be modified | Stop immediately and preserve current DNS state |
| Control group contains clients | Stop reconciliation and remove ambiguity through an approved change |
| Pi-hole is unavailable | Treat as a DNS availability incident and use PB-001 |
| Reconciliation remains unsafe | Disable NET-WATCH policy mutation through the approved recovery method, not global Pi-hole filtering |
| Dashboard authentication boundary has changed | Require security review before continued use |

## Validation

- Expected effective state: NET-WATCH is healthy and only the intended profile state changes.
- Positive test: approved profile transitions between allowed and blocked and returns to baseline.
- Negative test: unsafe default, missing, disabled, or foreign group target is rejected.
- Evidence record: service health, desired/actual state, warning state, and sanitized test record.
- Last successful validation: Phase 6 capability validation completed; this standalone runbook remains unvalidated.

## Rollback and recovery

- Rollback trigger: unintended client impact, unsafe group selection, DNS outage, or policy drift.
- Recovery steps: stop further reconciliation, restore last known-good group associations, confirm filtering remains enabled, and restart only the affected service if required.
- Restored-state verification: intended clients resolve DNS, unaffected profiles remain unchanged, and reconciliation is warning free.

## Stop conditions

Stop on scope loss, default-group risk, broad DNS impact, exposed credentials, telemetry loss, uncertain cleanup, or loss of configuration recovery.

## Closure

- Success criteria: API, HTTPS, Pi-hole, and profile policy are healthy and baseline state is restored.
- Remaining risk: record the single-Pi-hole availability dependency and any authentication exception.
- Follow-up owner: COC Operations.
- Documentation to update: Phase 6 record, risk register, NET-WATCH source documentation, and this runbook.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Operations | Initial draft NET-WATCH health procedure |
