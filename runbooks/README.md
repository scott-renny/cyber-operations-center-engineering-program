# Runbook Index

This directory defines repeatable operational procedures for the COC Engineering Program. New entries begin **Planned**. When the underlying capability exists and procedure content has been written, the document may move to **Draft**. Promotion to **Lab Validated** requires a controlled procedure test, rollback or recovery testing where applicable, and sanitized evidence.

## Status model

| Status | Meaning |
|---|---|
| Planned | Capability or procedure is not yet implemented |
| Draft | Procedure content exists but has not passed a standalone lab test |
| Lab Validated | Procedure passed a controlled test with evidence |
| Operational | Approved for repeated COC use |
| Retired | Superseded or no longer applicable |

## Runbooks

| ID | Runbook | Target phase | Status | Validation gate |
|---|---|---:|---|---|
| RB-001 | [Docker Service Health Check](RB-001-docker-service-health-check.md) | 3 | Draft | daemon failure and recovery tested |
| RB-002 | [Dockge Stack Deployment](RB-002-dockge-stack-deployment.md) | 3 | Draft | disposable stack deployed, stopped, and removed |
| RB-003 | [Container Log Inspection](RB-003-container-log-inspection.md) | 3 | Draft | known event traced through bounded logs |
| RB-004 | Container Image Update and Rollback | 3 | Planned | update and rollback performed without data loss |
| RB-005 | [Firewall Rollback](RB-005-firewall-rollback.md) | 4 | Draft | rule change reversed with access preserved |
| RB-006 | [Alert Triage](RB-006-alert-triage.md) | 4 | Draft | two controlled alerts investigated |
| RB-007 | [Wazuh Agent Troubleshooting — Cerberus](https://github.com/scott-renny/project-cerberus-build/blob/main/docs/operations/wazuh-agent-health.md) | 4, 8.5 | Planned | agent failure, re-enrollment, telemetry recovery, and enrollment closure tested |
| RB-008 | Suricata Sensor Health | 4 | Planned | sensor interruption detected and restored |
| RB-009 | [Logging Pipeline Troubleshooting](RB-009-logging-pipeline-troubleshooting.md) | 4, 6, 7 | Draft | failed stage isolated, recovered, and traced end to end |
| RB-010 | [End-to-End Telemetry Validation](RB-010-end-to-end-telemetry-validation.md) | 4, 7 | Draft | representative events traced across all implemented paths |
| RB-011 | [Backup Job Failure](RB-011-backup-job-failure.md) | 5 | Draft | failed job corrected, rerun, and restore verified |
| RB-012 | [Repository Integrity Validation](RB-012-repository-integrity-validation.md) | 5 | Draft | integrity check and representative restore completed |
| RB-013 | [File Restore](RB-013-file-restore.md) | 5 | Draft | isolated restore and comparison passed |
| RB-014 | [Full-System Restore](RB-014-full-system-restore.md) | 5 | Draft | staged recovery completed from a trusted baseline |
| RB-015 | [NET-WATCH Service and Policy Health](RB-015-netwatch-service-policy-health.md) | 6 | Draft | safe profile transition and rollback tested |
| RB-016 | [Endpoint Isolation — Cerberus](https://github.com/scott-renny/project-cerberus-build/blob/main/docs/operations/endpoint-isolation-and-reconnection.md) | 8, 8.5 | Planned | isolation, evidence preservation, and monitored reconnection tested |
| RB-017 | Endpoint Live Triage | 8 | Planned | controlled acquisition completed |
| RB-018 | [Endpoint Rebuild — Cerberus](https://github.com/scott-renny/project-cerberus-build/blob/main/docs/operations/backup-encrypted-recovery-and-rebuild.md) | 8, 8.5 | Planned | verified-media rebuild, selective restore, telemetry, and backup validation completed |
| RB-019 | AD Account Containment | 10 | Planned | disablement and recovery safely tested |
| RB-020 | Privileged Membership Review | 10 | Planned | synthetic excess privilege identified |
| RB-021 | Service-Account Rotation | 10 | Planned | rotation completed without outage |
| RB-022 | AD Persistence Hunt | 10 | Planned | controlled artifact detected and removed |
| RB-023 | TheHive Case Creation | 14 | Planned | synthetic case completed end to end |
| RB-024 | SOAR Manual Override | 15 | Planned | failed workflow handled manually |
| RB-025 | Forensic Acquisition | 17 | Planned | acquisition and custody record completed |
| RB-026 | COC Disaster Recovery | 21 | Planned | staged multi-service platform restoration completed |
| RB-027 | WireGuard Key Rotation | 24 | Planned | old peer key proven unusable |

## Cerberus supporting procedures

The [Cerberus Operations Runbooks](https://github.com/scott-renny/project-cerberus-build/tree/main/docs/operations) additionally govern Fedora updates and rollback, NVIDIA/display recovery, and hardware security-key recovery. These are supporting platform procedures rather than duplicate COC document IDs.

## Current validation priorities

1. RB-011, RB-012, and RB-013 — convert the completed Phase 5 capability evidence into standalone validation records.
2. RB-015 — exercise safe NET-WATCH profile-policy transition and rollback without affecting other profiles.
3. RB-009 and RB-010 — run a controlled failure/recovery and full telemetry trace.
4. RB-014 — schedule a staged recovery exercise after the selective recovery procedures pass.

A completed phase proves the underlying capability; it does not automatically validate every standalone operating procedure.

Use the [Runbook Template](../templates/RUNBOOK-TEMPLATE.md) for new procedures.
