# Playbook Index

Playbooks coordinate decisions and actions for security incidents. A playbook remains **Planned** until the necessary telemetry, containment, recovery, and case-management capabilities exist and a controlled exercise has passed.

| Playbook | Target phase | Status | Validation gate |
|---|---:|---|---|
| DNS Abuse or Service Disruption | 4 | Planned | supported scenario detected and contained |
| Denial-of-Service Response | 4 | Planned | safe simulation and recovery completed |
| Ransomware Response | 5 | Planned | tabletop plus restore evidence completed |
| Backup Repository Compromise | 5 | Planned | isolation and clean recovery tested |
| Endpoint Compromise | 8 | Planned | endpoint contained, investigated, and restored |
| Malware Response | 8 | Planned | controlled sample or simulator handled safely |
| Account Compromise | 10 | Planned | synthetic identity incident contained |
| Active Directory Compromise | 10 | Planned | disposable-lab exercise completed |
| Threat-Intelligence Escalation | 13 | Planned | indicator enrichment and disposition tested |
| Case Escalation and Coordination | 14 | Planned | synthetic TheHive case completed |
| SOAR Failure and Manual Override | 15 | Planned | orchestration failure safely handled |
| Forensic Investigation | 17 | Planned | evidence acquisition and custody validated |
| Cloud Account Compromise | 23 | Planned | isolated cloud-lab exercise completed |
| VPN Credential Exposure | 24 | Planned | revocation and replacement tested |

Use the [Playbook Template](../templates/PLAYBOOK-TEMPLATE.md). Severity assignments follow the [Severity Standard](../docs/SEVERITY-STANDARD.md).
