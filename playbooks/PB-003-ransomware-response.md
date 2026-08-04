# Playbook: Ransomware Response

**Document ID:** PB-003  
**Status:** Draft  
**Owner:** COC Incident Response  
**Related phases:** 5, 7, 8, and 17  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose and activation criteria

Coordinate response to suspected encryption, destructive file changes, ransom artifacts, or credible ransomware telemetry while protecting recovery points and evidence.

## Scope and authority

- Authorized assets: COC systems and approved endpoints, backup repository, monitoring platforms, and incident records.
- Decision owner: COC Incident Lead.
- Containment authority: immediate network isolation of a confirmed affected endpoint is permitted; destructive actions and broad credential resets require explicit coordination.
- External notification constraints: legal, privacy, law-enforcement, insurer, or public communication requires the appropriate owner; no ransom engagement is authorized by this document.

## Initial assessment

- Create a case and preserve original alerts and available telemetry.
- Assign the higher reasonable severity; confirmed destructive encryption is normally SEV-1 or SEV-2.
- Record affected assets, identities, shares, time window, evidence confidence, backup exposure, and visibility gaps.
- Determine whether real personal data or other notification obligations may be involved.

## Response phases

### Identification

- Confirm encryption or destructive behavior using safe observations; do not execute suspected samples.
- Review Wazuh, Zeek, Graylog, system, application, and backup telemetry.
- Identify earliest known activity, affected identities, reachable shares, and potential patient zero.
- Verify the last known-good recovery points without mounting or modifying affected data.
- Escalate immediately on privileged identity use, repository access, multiple hosts, or loss of security visibility.

### Containment

- Isolate affected endpoints and restrict compromised identities using approved controls.
- Stop propagation to shares and management interfaces with narrow reversible controls.
- Protect backup storage from further writes if repository compromise is plausible.
- Preserve volatile and disk evidence where capability and authority exist; do not delay urgent containment when harm is continuing.

### Eradication

- Rebuild affected endpoints from a trusted baseline when integrity cannot be established.
- Remove persistence and vulnerable entry points.
- Rotate exposed credentials, keys, tokens, and service accounts in dependency order.
- Validate that recovery points do not contain the active compromise.

### Recovery

- Apply RB-012 before selecting recovery data.
- Use RB-013 for selective recovery or RB-014 for staged platform recovery.
- Restore into isolated locations, scan and validate, then return services gradually.
- Apply RB-010 and monitor for renewed encryption, suspicious authentication, and beaconing.

## Decision matrix

| Condition | Action | Owner |
|---|---|---|
| Confirmed active encryption | Assign SEV-1/2, isolate affected systems, and protect backups | Incident Lead |
| Backup repository shows integrity or access anomalies | Activate PB-004 and stop repository writes | Backup owner |
| Only a harmless simulator or approved test is confirmed | Stop test, validate cleanup, and close as SEV-5 with evidence | Exercise owner |
| No trusted recovery point exists | Preserve all versions and escalate recovery decision | Decision owner |
| Evidence capability is unavailable | Record the gap and prioritize safe containment and recovery | Incident Lead |

## Communications

- Maintain an incident timeline with all containment and recovery decisions.
- Use confirmed facts and clearly label hypotheses.
- Restrict ransom content, personal data, credentials, system identifiers, and raw evidence.
- Route legal, privacy, insurer, law-enforcement, and public decisions to their designated owners.

## Closure

- Final disposition, affected scope, entry path, containment, eradication, and recovery are recorded.
- Evidence manifest and credential-rotation records are complete.
- Restored systems pass integrity, security, backup, and telemetry validation.
- Remaining risks and corrective actions have owners.
- Tabletop plus controlled restore evidence are required before Lab Validated status.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Incident Response | Initial draft grounded in the validated recovery foundation |
