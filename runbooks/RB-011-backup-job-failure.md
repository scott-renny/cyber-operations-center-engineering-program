# Runbook: Backup Job Failure

**Document ID:** RB-011  
**Status:** Draft  
**Owner:** COC Operations  
**Related phase:** 5  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose

Diagnose a failed or stale backup, safely restore scheduled protection, and prove that the new recovery point is usable.

## Trigger and scope

- Trigger: failed job, stale backup-age metric, missing snapshot, repository warning, or Wazuh backup event.
- Authorized systems: Phase 5 backup jobs, protected data sets, encrypted repository, and monitoring integration.
- Exclusions: deletion or pruning outside the approved retention policy.
- Required access: backup operator access and read access to monitoring.

## Prerequisites

- Open a change or incident record.
- Preserve the failure output and last successful snapshot metadata.
- Confirm destination capacity, credentials availability, and repository accessibility.
- Do not expose repository location, credentials, encryption material, or protected content.

## Procedure

1. Confirm the affected job, schedule, protected set, and last known-successful recovery point.
2. Check host and destination capacity, reachability, time, and mount state.
3. Review bounded job and monitoring logs for the first failure.
4. Verify credential availability without printing or rotating secrets.
5. Run a non-destructive repository integrity check appropriate to the backup tool.
6. Correct the narrowest confirmed cause.
7. Re-run the failed job once under observation.
8. Confirm a new snapshot or recovery point exists.
9. Restore one representative item to an isolated location and compare it with the source.
10. Confirm backup-age and monitoring telemetry return to expected state.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Last usable recovery point exceeds the recovery objective | Assign at least SEV-2 and notify the service owner |
| Repository integrity check fails | Stop writes and use the repository-compromise playbook |
| Credentials appear exposed | Revoke or rotate under the secrets standard before retry |
| Destination capacity is insufficient | Stop retries and open a capacity change |
| Second observed attempt fails | Escalate; do not create a retry loop |

## Validation

- Expected effective state: a current recovery point exists and a representative restore passes comparison.
- Positive test: observed backup plus isolated restore.
- Negative test: a controlled invalid destination or missing prerequisite is detected before data is written.
- Evidence record: job result, snapshot metadata, integrity result, restore comparison, and monitoring state.
- Last successful validation: Phase 5 capability validation completed; this failure procedure remains unvalidated.

## Rollback and recovery

- Rollback trigger: repository warnings, unexpected overwrite, growing data loss, or credential uncertainty.
- Recovery steps: stop the job, preserve repository state, restore the previous configuration, and retain the last known-good recovery point.
- Restored-state verification: repository remains readable and a known-good snapshot can be listed and restored.

## Stop conditions

Stop on scope loss, evidence risk, suspected repository compromise, unsafe overwrite, uncontrolled storage use, exposed secrets, or loss of the last recovery point.

## Closure

- Success criteria: root cause recorded, job succeeds, restore is verified, and monitoring is current.
- Remaining risk: record recovery-point gap and any unresolved capacity or single-destination dependency.
- Follow-up owner: COC Operations.
- Documentation to update: change/incident record, risk register, and backup evidence.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Operations | Initial draft based on Phase 5 recovery acceptance criteria |
