# Campaign Index

Campaign sequences are authorized adversary-emulation exercises. Every campaign is **Planned** until the Rules of Engagement, test environment, telemetry, stop conditions, cleanup plan, and validation record are approved.

| Campaign | Earliest phase | Status | Required gate |
|---|---:|---|---|
| Container Misconfiguration Validation | 4 | Planned | disposable target and Docker telemetry available |
| Network Detection Validation | 4 | Planned | sensors healthy and baseline recorded |
| Backup Resilience Exercise | 5 | Planned | clean recovery path available |
| Endpoint Detection Validation | 8 | Planned | managed disposable endpoint available |
| Identity Attack-Path Exercise | 10 | Planned | disposable AD lab and recovery plan available |
| Detection-Engineering Regression | 11 | Planned | versioned detections and replay data available |
| Threat-Intelligence Enrichment Exercise | 13 | Planned | MISP workflow available |
| Incident-Response Coordination Exercise | 14 | Planned | case-management workflow available |
| SOAR Failure Injection | 15 | Planned | manual override and rollback available |
| Forensic Readiness Exercise | 17 | Planned | acquisition tooling and custody process available |
| Purple-Team Campaign | 19 | Planned | approved detection objectives and cleanup plan |
| Cloud Control Validation | 23 | Planned | isolated account and cost limits available |

Use the [Campaign Template](../templates/CAMPAIGN-TEMPLATE.md) and [Rules of Engagement Template](../templates/RULES-OF-ENGAGEMENT-TEMPLATE.md). All activity follows the [Adversary-Emulation Standard](../docs/ADVERSARY-EMULATION-STANDARD.md).
