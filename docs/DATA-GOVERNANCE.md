# Data Governance Policy

**Owner:** COC Program Owner
**Classification:** Public policy; implementation details may be internal
**Review cadence:** Quarterly and after material changes to telemetry, storage, or publication practices

## 1. Purpose and scope

This policy governs data collected, processed, retained, shared, sanitized, and deleted by the Cyber Operations Center Engineering Program. It covers authentication, endpoint, network, DNS, vulnerability, asset, case-management, threat-intelligence, automation, backup, and forensic data.

## 2. Core rules

- Collect only data required for an approved operational, security, learning, validation, or evidence purpose.
- Record UTC in telemetry. Human-readable reports also record local time and UTC offset.
- Restrict access by least privilege and operational need.
- Preserve original evidence; analyze working copies where practical.
- Never publish secrets, live tokens, private keys, recovery codes, personal communications, family activity, public IP addresses, internal addressing that increases risk, device identifiers, or unredacted personal data.
- A false positive is retained as a documented case outcome, not silently deleted.
- A legal, safety, active-incident, or evidence hold overrides normal deletion.

## 3. Classification

| Class | Examples | Default handling |
|---|---|---|
| Public | Sanitized diagrams, policies, synthetic examples | May be committed after review |
| Internal | Architecture detail, inventories, non-sensitive configurations | Keep private unless sanitized |
| Confidential | Raw logs, DNS history, endpoint telemetry, case records, backup metadata | Restricted and encrypted |
| Restricted | Passwords, tokens, keys, recovery data, forensic images, personal content | Minimum access; never publish |

## 4. Data register

| Category | Purpose | Primary store | Access | Default retention | Protection | Deletion / disposition | Publication rule |
|---|---|---|---|---|---|---|---|
| Authentication events | Detect misuse and support investigations | Wazuh/SIEM | COC operator | 90 days searchable; up to 180 days archived when capacity permits | Access control, encrypted transport, protected storage | Retention job; incident hold exceptions | Redact users, IPs, domains, IDs, timestamps where identifying |
| Sysmon and endpoint telemetry | Detection, hunting, troubleshooting | Wazuh/endpoint platform | COC operator | 90 days searchable; 180 days for selected security events | Agent authentication, TLS, restricted dashboards | Retention job and agent offboarding | Use synthetic or heavily redacted excerpts |
| DNS activity | Troubleshooting and DNS-layer detection/control | Pi-hole and approved log pipeline | COC operator; household access not permitted | 30 days by default | Restricted UI/API, protected backups | Pi-hole retention controls and verified purge | Never publish household browsing history; use placeholders |
| Network IDS/flow data | Detect scanning, exploitation, beaconing, exfiltration | Suricata/Zeek/SIEM | COC operator | 90 days; longer only for cases | Segmented sensors, TLS where supported, access control | Lifecycle/retention policy | Redact internal/public IPs, MACs, domains and payload content |
| NET-WATCH/device discovery | Asset visibility and policy enforcement | NET-WATCH/NetBox | COC operator; approved family-facing views only | Current state plus 90 days of operational history | Authentication, restricted API, least privilege | Remove retired-device operational history after review | Replace names, MACs, IPs and household mappings |
| Vulnerability and patch data | Prioritize remediation and track exceptions | Management platform/risk register | COC operator | Current state plus 1 year of closure history | Restricted dashboards and exports | Delete stale raw exports; retain decisions | Publish only sanitized findings and remediation lessons |
| Threat intelligence | Enrich detections and conduct sweeps | MISP/approved feeds | COC operator | According to source terms; local sightings 1 year | Source validation and access control | Expire stale indicators; preserve case-linked indicators | Respect licenses and traffic-light restrictions |
| Incident and change cases | Accountability, response, audit, lessons learned | TheHive or equivalent | COC operator | 2 years; longer for major cases | Role-based access, backups, integrity checks | Approved disposal after holds expire | Publish sanitized case studies only |
| Forensic evidence | Investigation and chain of custody | Encrypted evidence store | Named custodian only | Case-based: review at closure, normally 1 year after closure | Encryption, hashes, write protection where practical, custody log | Verified secure deletion with disposition record | Never publish raw evidence; use synthetic excerpts |
| Backups | Recovery and resilience | Approved backup repository | Backup operator | Daily 30 days; monthly 12 months unless phase-specific RPO/RTO requires more | Encryption, restricted credentials, integrity tests | Automated expiry plus disposal verification | Do not publish inventories, paths, keys, or recovery material |
| Automation/SOAR records | Audit automated actions and overrides | SOAR/case platform | COC operator | 1 year | Signed/authenticated integrations and restricted logs | Retention policy | Redact tokens, endpoints and personal identifiers |
| Asset inventory | Lifecycle, ownership, trust, compliance | NetBox/inventory file | COC operator | Device life plus 1 year disposition record | Restricted fields and backups | Minimize after disposal; retain sanitization proof | Publish only generalized/sanitized inventory |

Retention periods are initial standards and may be shortened when capacity, privacy, licensing, or risk requires it. Any extension must have a documented purpose.

## 5. Evidence handling

Every collected evidence item receives a case ID, source, collector, collection time, timezone, cryptographic hash where applicable, storage location, access history, and disposition. Original evidence is not modified. Transfers are logged. Forensic collection follows the Digital Forensics Collection and Evidence Retention & Disposal runbooks.

## 6. Sanitization gate

Before GitHub, LinkedIn, screenshots, demonstrations, or shared reports:

1. Work from a copy.
2. Remove secrets and authentication artifacts.
3. Replace infrastructure identifiers with consistent placeholders such as `[SERVER-IP]`, `[HOSTNAME]`, and `[DOMAIN]`.
4. Remove personal names, email addresses, browsing activity, message content, device serials/MACs, case IDs, and metadata that can identify household members.
5. Crop browser chrome, bookmarks, notifications, file paths, and unrelated applications.
6. Reinspect the final exported artifact at full resolution.
7. Record reviewer, date, source, redactions, and release destination.

## 7. Incident and breach handling

Suspected unauthorized access, disclosure, loss, or corruption is handled through the appropriate playbook. Deletion stops until scope and evidence requirements are known. Compromised credentials are rotated under the Secrets and Key Management Standard.
