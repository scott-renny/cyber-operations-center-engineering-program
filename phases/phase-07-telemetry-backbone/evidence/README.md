# Phase 7 Validation Evidence

> **Status:** Sanitized for public release  
> **Captured:** 2026-08-04

This directory contains selected final-state evidence for the Phase 7 telemetry-backbone implementation. Setup wizards, duplicate views, raw terminal output, and screenshots containing unnecessary message-level detail were intentionally excluded.

## Evidence index

| Evidence | Validation |
|---|---|
| [Operations portal](01-operations-portal.png) | Core services and observability tiles are presented as live operational services |
| [Node Exporter dashboard](02-node-exporter-dashboard.png) | Grafana displays populated host CPU, memory, storage, network, and uptime metrics |
| [cAdvisor dashboard](03-cadvisor-dashboard.png) | Grafana displays live host and per-container resource metrics |
| [COC Operations Overview](04-coc-operations-overview.png) | Custom Pi-hole, Wazuh-volume, and telemetry-collector panels are populated |
| [Backup health](05-backup-health.png) | Restic and Windows backup ages are visible and remain within the defined healthy threshold |
| [Graylog input](06-graylog-input.png) | One COC Syslog UDP input is running with no input failures |

## Sanitization review

Before publication, the selected screenshots were reviewed for:

- credentials and authentication tokens;
- private keys and certificate material;
- live routable addresses;
- device identifiers and client-specific addressing;
- raw security-event payloads;
- unnecessary personal or browser information; and
- unrelated desktop or application content.

No credentials, private keys, private certificate material, live routable addresses, or client device identifiers are present in this evidence set. Generic listener values, loopback references, service ports, product names, and the program's already-documented lab hostname are retained where they provide meaningful technical context.

## Publication limits

These screenshots demonstrate service state and telemetry flow. They are not configuration backups and do not contain the secrets or complete operational values required to reproduce or access the environment.
