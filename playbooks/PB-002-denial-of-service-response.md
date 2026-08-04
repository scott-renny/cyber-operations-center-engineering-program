# Playbook: Denial-of-Service Response

**Document ID:** PB-002  
**Status:** Draft  
**Owner:** COC Incident Response  
**Related phases:** 4 and 7  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose and activation criteria

Coordinate response to suspected resource exhaustion, connection flooding, service saturation, or network denial affecting COC availability.

## Scope and authority

- Authorized assets: COC host, private services, network controls, Zeek, Suricata/Wazuh, Prometheus/Grafana, and Graylog.
- Decision owner: COC Incident Lead.
- Containment authority: emergency isolation of an affected internal source is allowed when required to prevent continuing harm; firewall or upstream changes follow change control.
- External notification constraints: no attribution or public claim without verified evidence.

## Initial assessment

- Create a case, preserve the initiating alert, and assign severity.
- Record affected services, start time, client scope, resource pressure, and whether management access remains available.
- Determine whether the event is malicious, accidental, a failed change, or normal load.

## Response phases

### Identification

- Review host, container, network, and service metrics around the onset.
- Use Zeek and Suricata/Wazuh to identify connection patterns and candidate sources within actual sensor visibility.
- Review Graylog and application logs for error rate, timeouts, and dependency failure.
- Compare with recent deployments, scans, backup activity, and maintenance.
- Escalate on sustained critical-service loss, loss of security visibility, or uncontrolled spread.

### Containment

- Stop approved test or maintenance traffic immediately.
- Isolate a confirmed internal source using the narrowest reversible control.
- Apply bounded rate, service, or firewall controls only with a rollback plan and preserved management access.
- Avoid broad blocks based on unverified source attribution.

### Eradication

- Remove the generating fault, compromised client, unsafe job, or misconfiguration.
- Patch or reconfigure the exploited service when evidence supports the cause.
- Preserve relevant logs and configuration before replacement.

### Recovery

- Restore services in dependency order and remove temporary controls gradually.
- Use RB-010 to validate telemetry and platform health.
- Monitor load, errors, connections, and security visibility through the recovery window.

## Decision matrix

| Condition | Action | Owner |
|---|---|---|
| Approved test or maintenance caused load | Stop activity, validate recovery, record SEV-5 or SEV-4 | Activity owner |
| One internal source causes sustained impact | Isolate source and investigate compromise or malfunction | Incident Lead |
| Public or upstream saturation exceeds local control | Preserve evidence, maintain internal safety, and escalate to provider/network owner | Decision owner |
| Security telemetry fails during the event | Raise severity and prioritize visibility restoration | Incident Lead |
| Containment risks loss of management access | Stage an alternate access path or stop the change | COC Operations |

## Communications

- Record detection, severity, containment, service recovery, and closure timestamps.
- Report observed impact, not assumed attack volume or attribution.
- Keep sensitive topology, addresses, firewall details, and raw logs private.

## Closure

- Final disposition distinguishes attack, misconfiguration, expected test, and false positive.
- Evidence manifest and temporary-control removals are complete.
- Service health and telemetry are stable through the monitoring window.
- Corrective actions and remaining capacity or visibility risks have owners.
- A safe simulation and recovery exercise are required before Lab Validated status.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Incident Response | Initial draft DoS response playbook |
