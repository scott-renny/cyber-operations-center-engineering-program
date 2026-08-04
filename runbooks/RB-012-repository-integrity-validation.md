# Runbook: Repository Integrity Validation

**Document ID:** RB-012  
**Status:** Draft  
**Owner:** COC Operations  
**Related phase:** 5  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose

Confirm that the encrypted backup repository is readable, internally consistent, and capable of supporting recovery without changing protected data.

## Trigger and scope

- Trigger: scheduled integrity review, backup warning, storage event, before major change, or after suspected compromise.
- Authorized systems: the Phase 5 backup repository and representative snapshots.
- Exclusions: retention pruning, repair, re-encryption, or destructive recovery without a separate approved change.
- Required access: least-privilege repository read/check access.

## Prerequisites

- Record the validation ID, repository identifier, and expected recovery points.
- Confirm stable power, storage, and connectivity.
- Preserve current repository and job metadata.
- Keep locations, credentials, and encryption material private.

## Procedure

1. Confirm the repository is the approved target and no destructive maintenance is scheduled.
2. Review capacity, filesystem, mount, and recent hardware or transport warnings.
3. List expected recent recovery points.
4. Run the backup tool's non-destructive metadata and integrity checks.
5. Select a representative recovery point and restore a small item to an isolated path.
6. Compare size and cryptographic hash where suitable.
7. Confirm monitoring records the validation activity without exposing content.
8. Record checked scope, duration, findings, and any areas not covered.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Expected recovery point is missing | Use RB-011 and assess recovery-objective impact |
| Integrity error is reported | Stop repository writes and activate PB-004 |
| Storage or transport errors recur | Escalate to infrastructure recovery and preserve evidence |
| Representative restore differs | Treat as integrity failure; do not overwrite the source |
| Check cannot cover the full repository | Record the limitation and schedule a bounded full check |

## Validation

- Expected effective state: checks pass and a representative restore matches.
- Positive test: non-destructive check plus isolated restore comparison.
- Negative test: invalid or unauthorized repository target is rejected before access.
- Evidence record: check summary, snapshot identifier, comparison result, and sanitized validation record.
- Last successful validation: Phase 5 repository inspection was completed; this standalone procedure remains unvalidated.

## Rollback and recovery

- Rollback trigger: check produces repository changes, performance threatens operations, or errors increase.
- Recovery steps: stop the check, preserve logs and metadata, return jobs to the last known-safe state, and escalate.
- Restored-state verification: repository remains readable and no unexpected mutation occurred.

## Stop conditions

Stop on scope uncertainty, suspected compromise, unsafe write activity, exposed secret material, storage instability, or risk to the last recovery point.

## Closure

- Success criteria: integrity state and restore result are recorded with owned findings.
- Remaining risk: document unchecked data, aging media, or single-repository dependency.
- Follow-up owner: COC Operations.
- Documentation to update: validation record and risk register.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Operations | Initial draft integrity procedure |
