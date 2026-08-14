# Playbook: Backup Repository Compromise

**Document ID:** PB-004  
**Status:** Draft  
**Owner:** COC Incident Response  
**Related phases:** 5 and 8.5  
**Version:** 0.2  
**Last reviewed:** 2026-08-14  
**Next review:** 2026-11-14

## Purpose and activation criteria

Coordinate investigation, containment, and clean recovery when backup data, repository metadata, credentials, retention, or integrity may have been altered or exposed.

## Scope and authority

- Authorized assets: Phase 5 backup jobs, encrypted repository, protected systems, monitoring, recovery records, and the Fedora Cerberus backup job after Phase 8.5 onboarding.
- Decision owner: COC Incident Lead.
- Containment authority: the backup owner may stop repository writes to preserve recovery options; deletion, repair, or reinitialization requires explicit approval.
- External notification constraints: keep repository locations, contents, credentials, keys, and recovery inventory private.

## Initial assessment

- Create a case and preserve the original alert or integrity result.
- Assign at least SEV-2 when repository trust or recent recovery points are materially uncertain.
- Record affected repository, jobs, identities, time window, last trusted recovery point, and available independent copies.
- Determine whether credential exposure, destructive access, or personal-data exposure is possible.

## Response phases

### Identification

- Preserve job output, access records, repository metadata, and monitoring evidence.
- Review recent administrative access, configuration changes, retention actions, and integrity results.
- Compare expected and actual recovery points.
- Validate storage and transport health to distinguish compromise from corruption.
- Do not run repair or pruning before evidence and recovery options are preserved.

### Containment

- Stop scheduled and manual writes when continued access could destroy evidence or good recovery points.
- Revoke or restrict suspected credentials through the secrets-management process.
- Isolate the repository or affected host with reversible controls while retaining authorized evidence access.
- Protect independent or offline copies from the same credentials and management path.

### Eradication

- Remove unauthorized access, persistence, or unsafe automation.
- Rebuild the backup control plane from a trusted baseline when integrity is uncertain.
- Rotate credentials and encryption material only through a documented sequence that preserves access to required historical backups.
- Establish a clean destination if the existing repository cannot be trusted.

### Recovery

- Run RB-012 against candidate trusted copies.
- Restore representative data to an isolated destination and compare with trusted source or records.
- Re-establish jobs with least privilege and monitor the first successful cycles.
- Confirm backup-age, Wazuh, and collector telemetry.
- When Cerberus is affected, use its [Backup, Encrypted Recovery, and Rebuild](https://github.com/scott-renny/project-cerberus-build/blob/main/docs/operations/backup-encrypted-recovery-and-rebuild.md) procedure for isolated restoration or trusted rebuild.

## Decision matrix

| Condition | Action | Owner |
|---|---|---|
| Integrity error with no access anomaly | Preserve state, investigate storage/corruption, and keep writes stopped | Backup owner |
| Unauthorized access or deletion is confirmed | Assign SEV-1/2, revoke access, protect independent copies | Incident Lead |
| Encryption key or credential exposure is suspected | Rotate under the secrets standard with historical-access plan | Secrets owner |
| Repository cannot be trusted | Build a clean destination and recover from an independent trusted copy | Decision owner |
| No independent trusted copy exists | Preserve all evidence and escalate business/recovery decision | Incident Lead |

## Communications

- Record detection, write suspension, credential action, trusted-copy selection, restoration, and closure timestamps.
- Report recovery confidence explicitly; do not describe an unchecked snapshot as clean.
- Prohibit disclosure of locations, inventory, credentials, keys, personal data, or raw repository evidence.

## Closure

- Final disposition distinguishes compromise, corruption, configuration error, and false positive.
- Evidence manifest, credential actions, and trusted-copy rationale are complete.
- A clean repository and representative restore are validated.
- Remaining recovery-point gaps and architectural risks have owners.
- Isolation and clean recovery must be exercised before Lab Validated status.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.2 | 2026-08-14 | COC Incident Response | Added Fedora Cerberus backup scope and governed recovery cross-reference |
| 0.1 | 2026-08-04 | COC Incident Response | Initial draft backup-compromise playbook |
