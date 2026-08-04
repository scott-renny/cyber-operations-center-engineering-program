# Playbook: DNS Abuse or Service Disruption

**Document ID:** PB-001  
**Status:** Draft  
**Owner:** COC Incident Response  
**Related phases:** 4, 6, and 7  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose and activation criteria

Coordinate investigation and recovery when DNS filtering, resolution, or profile policy is unavailable, manipulated, bypassed, or producing material client impact.

## Scope and authority

- Authorized assets: COC Pi-hole, NET-WATCH, approved clients, Wazuh, Zeek, Prometheus/Grafana, and Graylog.
- Decision owner: COC Incident Lead.
- Containment authority: COC Operations may isolate affected clients or stop unsafe NET-WATCH reconciliation; broad DNS policy changes require the decision owner.
- External notification constraints: do not publish client identifiers, queries, addresses, credentials, or private topology.

## Initial assessment

- Create a case ID and preserve the original alert and relevant telemetry.
- Assign severity using the Severity Standard.
- Record affected clients, profiles, timeframe, failure mode, and known visibility gaps.
- Distinguish availability failure, policy error, suspected abuse, and expected blocking.

## Response phases

### Identification

- Confirm Pi-hole service and filtering state, NET-WATCH health, and the private management endpoint.
- Review Zeek DNS metadata, Wazuh alerts, Pi-hole metrics, NET-WATCH events, and recent approved changes.
- Test resolution from one affected and one known-good client.
- Check whether the issue is profile-specific or broad.
- Treat default-group changes, foreign rule mutation, unexplained forwarding, or hostile query patterns as escalation indicators.

### Containment

- Stop unsafe NET-WATCH reconciliation if desired and actual policy cannot be aligned safely.
- Isolate a suspected client using approved network controls when evidence supports it.
- Preserve filtering; do not use Pi-hole global disablement as routine containment.
- If availability requires temporary resolver fallback, obtain decision-owner approval and record reduced filtering and monitoring.

### Eradication

- Remove unauthorized DNS settings, rules, clients, or profile associations through an approved change.
- Correct the narrowest failed service or configuration.
- Rotate exposed credentials and review persistence when unauthorized administration is suspected.

### Recovery

- Apply RB-015 to restore service and profile-policy health.
- Apply RB-010 to validate DNS telemetry and supporting monitoring.
- Return clients in stages and monitor query patterns and service health through the defined recovery window.

## Decision matrix

| Condition | Action | Owner |
|---|---|---|
| Broad DNS outage with no compromise evidence | Restore availability, retain filtering where possible, and assign SEV-2 or SEV-3 by impact | COC Operations |
| Unauthorized rule, client, or resolver change | Preserve evidence, contain administrative access, and assign at least SEV-2 | Incident Lead |
| One profile is incorrectly blocked | Stop profile mutation, restore last-good association, and validate unaffected profiles | COC Operations |
| Suspicious client queries with healthy DNS service | Isolate the client when authorized and open the relevant compromise playbook | Incident Lead |
| Default group or global filtering is at risk | Stop all policy changes and recover from known-good configuration | COC Operations |

## Communications

- Record initial detection, severity, containment, service restoration, and closure timestamps.
- Provide internal updates at severity-appropriate intervals.
- State confirmed impact and known gaps; do not imply full switched-LAN visibility.
- Prohibit disclosure of queries, client identities, addresses, credentials, and private endpoints.

## Closure

- Final disposition and root cause are recorded.
- Evidence manifest includes relevant alerts, DNS metadata, changes, and validations.
- DNS service, filtering, profile state, and telemetry are validated.
- Remaining single-resolver risk and corrective actions have owners.
- A tabletop and controlled technical exercise are required before promotion to Lab Validated.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Incident Response | Initial draft using implemented DNS and telemetry capabilities |
