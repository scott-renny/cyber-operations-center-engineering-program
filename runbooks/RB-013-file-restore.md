# Runbook: File Restore

**Document ID:** RB-013  
**Status:** Draft  
**Owner:** COC Operations  
**Related phase:** 5  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose

Restore selected files from an approved recovery point to an isolated destination, validate them, and return them to service without overwriting good data unintentionally.

## Trigger and scope

- Trigger: approved recovery request, validation exercise, or incident recovery.
- Authorized systems: files protected by the Phase 5 backup workflow.
- Exclusions: full-system recovery and restoration of evidence into its original path before validation.
- Required access: backup operator and destination-owner approval.

## Prerequisites

- Record requester, source, desired timestamp, destination, and approval.
- Confirm the target recovery point predates the loss or corruption.
- Confirm adequate destination capacity and malware-scanning capability where appropriate.
- Preserve the current destination before replacement.

## Procedure

1. Verify the requested file set, owner, recovery point, and business purpose.
2. List candidate recovery points and select the narrowest valid one.
3. Restore to a new isolated path, never directly over the active copy.
4. Record restored metadata and compute hashes where appropriate.
5. Compare restored content, size, permissions, and expected ownership with a trusted reference.
6. Scan or inspect the restored data when compromise is possible.
7. Obtain owner confirmation before replacing or merging active content.
8. Preserve the superseded active copy until acceptance.
9. Confirm the application or user can read the restored data.
10. Record disposition and retention of temporary copies.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| No valid pre-incident recovery point exists | Escalate and preserve all available versions |
| Restored content fails validation | Try an earlier recovery point; do not promote the file |
| Malware or suspicious content is found | Isolate and activate the applicable incident playbook |
| Permissions or ownership are unclear | Stop and obtain the service owner's decision |
| Request includes evidence | Apply evidence-handling and chain-of-custody controls |

## Validation

- Expected effective state: approved files are restored, validated, and usable.
- Positive test: isolated restore and hash or content comparison.
- Negative test: direct overwrite without approval is blocked.
- Evidence record: request, recovery point, validation result, owner acceptance, and cleanup.
- Last successful validation: representative Phase 5 restore completed; this standalone procedure remains unvalidated.

## Rollback and recovery

- Rollback trigger: restored data causes errors, is incomplete, or is later found unsafe.
- Recovery steps: remove the promoted copy from service, reinstate the preserved prior copy, and reassess recovery points.
- Restored-state verification: service returns to the pre-restore state and temporary data is accounted for.

## Stop conditions

Stop on uncertain authority, unsafe content, evidence-integrity risk, unexpected overwrite, exposed secrets, or loss of the prior active copy.

## Closure

- Success criteria: owner accepts the restored data and all temporary copies have a recorded disposition.
- Remaining risk: document missing history, partial restore, or unresolved corruption.
- Follow-up owner: COC Operations and the data owner.
- Documentation to update: recovery record and related incident/change record.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Operations | Initial draft selective-restore procedure |
