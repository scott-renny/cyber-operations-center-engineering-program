# Runbook Index

This directory defines repeatable operational procedures for the COC Engineering Program. New entries begin **Planned**. When the underlying capability exists and procedure content has been written, the document may move to **Draft**. Promotion to **Lab Validated** requires a controlled procedure test, rollback or recovery testing where applicable, and sanitized evidence.

## Status model

| Status | Meaning |
|---|---|
| Planned | Capability or procedure is not yet implemented |
| Draft | Procedure content exists but has not passed a lab test |
| Lab Validated | Procedure passed a controlled test with evidence |
| Operational | Approved for repeated COC use |
| Retired | Superseded or no longer applicable |

## Runbooks

| Runbook | Target phase | Status | Validation gate |
|---|---:|---|---|
| [Docker Service Health Check](RB-001-docker-service-health-check.md) | 3 | Draft | daemon failure and recovery tested |
| [Dockge Stack Deployment](RB-002-dockge-stack-deployment.md) | 3 | Draft | disposable stack deployed, stopped, and removed |
| [Container Log Inspection](RB-003-container-log-inspection.md) | 3 | Draft | known event traced through bounded logs |
| Container Image Update and Rollback | 3 | Planned | update and rollback performed without data loss |
| [Firewall Rollback](RB-005-firewall-rollback.md) | 4 | Draft | rule change reversed with access preserved |
| [Alert Triage](RB-006-alert-triage.md) | 4 | Draft | two controlled alerts investigated |
| Wazuh Agent Troubleshooting | 4 | Planned | agent failure and recovery tested |
| Suricata Sensor Health | 4 | Planned | sensor interruption detected and restored |
| Logging Pipeline Troubleshooting | 4 | Planned | broken stage isolated and recovered |
| End-to-End Telemetry Validation | 4 | Planned | controlled event traced from source to case |
| Backup Job Failure | 5 | Planned | failed job detected, corrected, and rerun |
| Repository Integrity Validation | 5 | Planned | integrity check completed |
| File Restore | 5 | Planned | isolated restore and hash comparison passed |
| Full-System Restore | 5 | Planned | staged recovery completed |
| Endpoint Isolation | 8 | Planned | isolation and reversal tested |
| Endpoint Live Triage | 8 | Planned | controlled acquisition completed |
| Endpoint Rebuild | 8 | Planned | rebuild and security validation completed |
| AD Account Containment | 10 | Planned | disablement and recovery safely tested |
| Privileged Membership Review | 10 | Planned | synthetic excess privilege identified |
| Service-Account Rotation | 10 | Planned | rotation completed without outage |
| AD Persistence Hunt | 10 | Planned | controlled artifact detected and removed |
| TheHive Case Creation | 14 | Planned | synthetic case completed end to end |
| SOAR Manual Override | 15 | Planned | failed workflow handled manually |
| Forensic Acquisition | 17 | Planned | acquisition and custody record completed |
| WireGuard Key Rotation | 24 | Planned | old peer key proven unusable |
| COC Disaster Recovery | 21 | Planned | staged platform restoration completed |

Use the [Runbook Template](../templates/RUNBOOK-TEMPLATE.md) for new procedures.
