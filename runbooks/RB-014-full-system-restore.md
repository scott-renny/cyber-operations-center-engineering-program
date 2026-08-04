# Runbook: Full-System Restore

**Document ID:** RB-014  
**Status:** Draft  
**Owner:** COC Operations  
**Related phase:** 5  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose

Coordinate a staged recovery of the COC host or service platform from validated recovery points while preserving evidence and preventing an unsafe return to service.

## Trigger and scope

- Trigger: unrecoverable host failure, destructive corruption, approved disaster-recovery exercise, or incident recovery decision.
- Authorized systems: the Phase 5 protected COC configuration and operational data.
- Exclusions: unapproved destructive rebuilds and restoration onto an untrusted platform.
- Required access: COC decision owner, infrastructure administrator, and backup operator.

## Prerequisites

- Assign severity, incident/change ID, decision owner, and recovery lead.
- Preserve forensic evidence when compromise is possible.
- Confirm trusted installation media, target hardware, recovery points, credentials, and network isolation.
- Define recovery objectives, service order, rollback point, and communication cadence.

## Procedure

1. Confirm restoration is authorized and that repair in place is not safer.
2. Isolate the failed or suspected system while preserving required evidence.
3. Validate target hardware, storage health, time, and trusted baseline media.
4. Rebuild or prepare the base operating system using the approved foundation and hardening records.
5. Restore platform configuration before application data.
6. Restore services in dependency order: network and access controls, container platform, core security services, backup monitoring, NET-WATCH, then telemetry.
7. Validate each stage before continuing and keep external exposure blocked.
8. Restore protected operational data from the approved recovery point.
9. Rotate credentials and keys when compromise or exposure cannot be excluded.
10. Run service-health, firewall, backup, and end-to-end telemetry validations.
11. Reconnect only approved networks and monitor through the defined recovery period.
12. Obtain decision-owner acceptance before incident closure.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Recovery point may contain compromise | Use an earlier point and require security review |
| Trusted baseline cannot be established | Stop; do not restore sensitive data |
| Critical validation fails | Hold at the current stage and roll back the affected service |
| Recovery objective will be missed | Escalate severity and communicate revised expectations |
| Evidence preservation conflicts with recovery | Decision owner and evidence custodian document the tradeoff |

## Validation

- Expected effective state: required services operate securely from a trusted baseline with current monitoring and backups.
- Positive test: staged lab recovery through essential service validation.
- Negative test: a recovery point with failed integrity or missing approval is rejected.
- Evidence record: stage checklist, recovery-point identifiers, validations, decisions, and restored-state proof.
- Last successful validation: staged standalone full-system recovery has not yet been completed.

## Rollback and recovery

- Rollback trigger: trust cannot be established, validation fails materially, or restoration expands impact.
- Recovery steps: isolate the target, preserve current state, revert the failed stage, and reassess the recovery point or baseline.
- Restored-state verification: no unsafe target is exposed and the last trusted recovery option remains available.

## Stop conditions

Stop on scope loss, uncertain trust, evidence loss, unsafe connectivity, exposed secrets, uncontrolled impact, or loss of the last recovery option.

## Closure

- Success criteria: decision owner accepts service state, validations pass, monitoring and backups are current, and remaining risk is owned.
- Remaining risk: document data gap, reduced redundancy, deferred services, and heightened monitoring period.
- Follow-up owner: COC Operations.
- Documentation to update: incident review, architecture/phase records, risk register, and this runbook.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Operations | Initial draft staged recovery procedure |
