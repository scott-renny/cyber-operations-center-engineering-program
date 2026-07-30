# Severity and Priority Standard

**Status:** Approved  
**Owner:** COC Program  
**Review cadence:** Annual and after material incidents

## Purpose

Define consistent severity for security events, incidents, operational failures, and vulnerabilities. Severity reflects impact and urgency; it is not a measure of effort.

## Severity levels

| Level | Meaning | Representative conditions | Initial response target |
|---|---|---|---|
| SEV-1 Critical | Active or imminent material harm | confirmed compromise of privileged identity, destructive activity, major data exposure, loss of critical security visibility during an incident | Immediate |
| SEV-2 High | Serious impact or credible containment risk | confirmed endpoint compromise, high-confidence lateral movement, major control failure, repeated failed containment | Within 1 hour |
| SEV-3 Medium | Limited impact requiring investigation | suspicious activity with incomplete evidence, isolated control degradation, contained malware, material vulnerability without active exploitation | Same business day |
| SEV-4 Low | Minor or informational condition | low-confidence alert, policy deviation without observed impact, routine hardening opportunity | Planned queue |
| SEV-5 Informational | No incident impact | expected test activity, benign observation, false positive, documentation-only finding | Record and close or track |

Targets are operational objectives, not contractual service-level agreements.

## Classification factors

Assess:

- confidentiality, integrity, and availability impact;
- affected asset criticality and scope;
- privilege level and persistence;
- evidence confidence;
- active exploitation or spread;
- safety, legal, privacy, and recovery implications;
- visibility gaps that could hide greater impact.

When uncertain, assign the higher reasonable severity until evidence supports reduction.

## Priority and escalation

Priority may be raised when a lower-severity issue blocks a critical project phase, threatens evidence preservation, or has a narrow remediation window. Record all changes to severity or priority with time, owner, evidence, and rationale.

SEV-1 and SEV-2 conditions require immediate containment planning and explicit ownership. Any condition involving real personal data, uncontrolled cost, unsafe testing, or loss of authorized scope triggers the applicable stop condition.

## Closure

A case may close only when disposition, evidence, containment or recovery state, remaining risk, follow-up owner, and lessons learned are recorded. False positives remain documented outcomes.

## Related controls

- [Data Governance](DATA-GOVERNANCE.md)
- [Documentation Standards](../DOCUMENTATION-STANDARDS.md)
- [Security Principles](../SECURITY-PRINCIPLES.md)
- [Operational Governance Mapping](OPERATIONAL-GOVERNANCE-MAPPING.md)
