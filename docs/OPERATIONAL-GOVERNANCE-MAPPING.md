# Operational Governance Mapping

**Program:** Cyber Operations Center (COC) Engineering Program
**Status:** Approved Phase 0 control map
**Review cadence:** Quarterly and after major incidents, architecture changes, or material control failures

## Purpose

This document connects the COC governance layer to the existing **Runbooks, Playbooks & Campaign Sequences** operating manual. Governance documents define mandatory outcomes and boundaries; operational documents define the steps used to achieve them.

## Document hierarchy

1. Program governance and security principles
2. Architecture Decision Records and risk decisions
3. Technical and documentation standards
4. Runbooks for repeatable operations
5. Playbooks for incident response
6. Campaign sequences for authorized adversary emulation
7. Case, change, test, and evidence records

A lower-level document may not override a higher-level control. Conflicts must be resolved through a change record, risk review, and—when architectural—a new or superseding ADR.

## Control mapping

| Operational requirement | Governance owner | Required record |
|---|---|---|
| Explicit authorization and scope before testing | SECURITY-PRINCIPLES; PORTFOLIO-POLICY | Engagement record |
| Stop on scope loss, telemetry loss, real data, unsafe conditions, uncontrolled cost, or uncertain cleanup | SECURITY-PRINCIPLES; RISK-REGISTER | Campaign log and stop decision |
| Case ID, owner, severity, status, timestamps, assets, scope, evidence, decisions, recovery, lessons | DOCUMENTATION-STANDARDS; DATA-GOVERNANCE | Incident case |
| UTC telemetry and local time with offset in reports | DOCUMENTATION-STANDARDS | Case/change/test record |
| Preserve false positives as documented outcomes | DATA-GOVERNANCE | Closed case record |
| Record purpose, risk, backup, test, verification, and rollback for changes | CONTRIBUTING; DOCUMENTATION-STANDARDS | Change record |
| Stage detection, firewall, automation, and patch changes | SECURITY-PRINCIPLES; RISK-REGISTER | Test and validation evidence |
| Preserve original alerts and relevant logs | DATA-GOVERNANCE | Evidence manifest |
| Hash forensic evidence and preserve chain of custody | DATA-GOVERNANCE | Chain-of-custody log |
| Rotate keys after exposure and revoke superseded credentials | SECRETS-MANAGEMENT | Rotation record |
| Record visibility gaps and suspend unsupported coverage claims | RISK-REGISTER; DATA-GOVERNANCE | Visibility-risk entry |
| Retain cleanup, credential-revocation, and restored-state proof after campaigns | PORTFOLIO-POLICY; DATA-GOVERNANCE | Campaign closure record |

## Operational document review

Each runbook, playbook, and campaign sequence must include or inherit:

- owner and trigger;
- authorized scope;
- required evidence;
- decision and escalation points;
- safety or stop conditions;
- rollback or recovery steps;
- closure criteria;
- remaining risk and follow-up ownership;
- review date and version.

## Compliance rule

A procedure is not approved for COC use when it lacks an accountable owner, validation evidence, safe rollback or containment, sanitized publication handling, or a documented exception in the risk register.
