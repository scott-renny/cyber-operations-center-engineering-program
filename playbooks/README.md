# Playbook Index

Playbooks coordinate decisions and actions for security incidents. A playbook may move from **Planned** to **Draft** when sufficient supporting capabilities exist and the response content has been written. Promotion to **Lab Validated** requires the stated tabletop or controlled exercise, recovery proof, and sanitized evidence.

## Status model

| Status | Meaning |
|---|---|
| Planned | Required response capability is not yet implemented |
| Draft | Response content exists but the complete playbook has not passed its exercise |
| Lab Validated | Playbook passed its controlled exercise with evidence |
| Operational | Approved for repeated COC incident use |
| Retired | Superseded or no longer applicable |

## Playbooks

| ID | Playbook | Target phase | Status | Validation gate |
|---|---|---:|---|---|
| PB-001 | [DNS Abuse or Service Disruption](PB-001-dns-abuse-or-service-disruption.md) | 4, 6, 7 | Draft | supported DNS scenario detected, contained, recovered, and reviewed |
| PB-002 | [Denial-of-Service Response](PB-002-denial-of-service-response.md) | 4, 7 | Draft | safe simulation, containment rollback, and recovery completed |
| PB-003 | [Ransomware Response](PB-003-ransomware-response.md) | 5, 7, 8, 17 | Draft | tabletop completed now; technical validation after endpoint and forensic capability |
| PB-004 | [Backup Repository Compromise](PB-004-backup-repository-compromise.md) | 5 | Draft | isolation and clean recovery exercised against controlled data |
| PB-005 | Endpoint Compromise | 8 | Planned | endpoint contained, investigated, and restored |
| PB-006 | Malware Response | 8 | Planned | controlled sample or simulator handled safely |
| PB-007 | Account Compromise | 10 | Planned | synthetic identity incident contained |
| PB-008 | Active Directory Compromise | 10 | Planned | disposable-lab exercise completed |
| PB-009 | Threat-Intelligence Escalation | 13 | Planned | indicator enrichment and disposition tested |
| PB-010 | Case Escalation and Coordination | 14 | Planned | synthetic TheHive case completed |
| PB-011 | SOAR Failure and Manual Override | 15 | Planned | orchestration failure safely handled |
| PB-012 | Forensic Investigation | 17 | Planned | evidence acquisition and custody validated |
| PB-013 | Cloud Account Compromise | 23 | Planned | isolated cloud-lab exercise completed |
| PB-014 | VPN Credential Exposure | 24 | Planned | revocation and replacement tested |

## Current validation priorities

1. Conduct a tabletop for PB-003 using the validated Phase 5 restore capability while documenting endpoint and forensic gaps.
2. Exercise PB-004 with controlled repository data, credential revocation, and clean recovery.
3. Run a safe DNS disruption scenario for PB-001 and use RB-015 for recovery.
4. Run a bounded availability simulation for PB-002 after approving containment and rollback controls.

## Fedora workstation procedure integration

Phase 8.5 platform mechanics are maintained in the [Cerberus Operations Runbooks](https://github.com/scott-renny/project-cerberus-build/tree/main/docs/operations). PB-003 and PB-004 govern incident decisions; the Cerberus procedures govern Fedora-specific containment, telemetry recovery, selective restoration, trusted rebuild, graphics recovery, and security-key recovery.

Those linked procedures remain Planned until Cerberus exists and their validation gates pass. A cross-repository link does not promote either document's status.

Draft status means that the response path is documented, not that the complete incident scenario has been proven.

Use the [Playbook Template](../templates/PLAYBOOK-TEMPLATE.md). Severity assignments follow the [Severity Standard](../docs/SEVERITY-STANDARD.md).
