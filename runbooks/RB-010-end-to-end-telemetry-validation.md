# Runbook: End-to-End Telemetry Validation

**Document ID:** RB-010  
**Status:** Draft  
**Owner:** COC Operations  
**Related phases:** 4 and 7  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose

Prove that representative network, host, container, backup, DNS, security-volume, and application telemetry reaches its intended collection and presentation layer.

## Trigger and scope

- Trigger: after a telemetry change, before a phase gate, after an outage, or during the quarterly control review.
- Authorized systems: Zeek, Suricata/Wazuh, Prometheus, node_exporter, cAdvisor, the COC custom collector, Grafana, Graylog, and NET-WATCH forwarding.
- Exclusions: claims of complete switched-LAN coverage and any unapproved offensive traffic.
- Required access: read access to all telemetry platforms and permission to generate benign test events.

## Prerequisites

- Record an approved test window and case or validation ID.
- Confirm time synchronization and note local offset and UTC.
- Confirm available storage and current service health.
- Prepare benign test events that contain no secrets or personal data.

## Procedure

1. Record baseline health for all collectors, targets, inputs, and dashboards.
2. Generate an approved DNS lookup and HTTPS connection visible to the server-side sensor.
3. Confirm Zeek connection, DNS, and TLS metadata for the test window.
4. Confirm the relevant Suricata/Wazuh path remains healthy without asserting an alert if no signature should fire.
5. Verify Prometheus targets for Prometheus, node_exporter, and cAdvisor report up.
6. Confirm host and container metrics are fresh in Grafana.
7. Confirm Pi-hole statistics, Wazuh alert volume, backup age, and collector-health metrics are fresh.
8. Generate one benign NET-WATCH application event.
9. Confirm the event is searchable in the COC General Logs index in Graylog.
10. Verify the private HTTPS endpoints for Grafana, Graylog, and Prometheus.
11. Record coverage gaps, event times, collection lag, and the final disposition.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| One source is stale | Use RB-009 and assign SEV-3 unless impact requires elevation |
| Multiple security sources are stale | Assign SEV-2 and preserve the last available evidence |
| Wireless sensor cannot observe expected switched traffic | Record the known visibility limitation; do not claim coverage |
| Custom collector reports failure | Isolate the failing sub-collector and preserve last-good metrics |
| Primary Graylog shard is unavailable | Stop validation and recover the search service before proceeding |

## Validation

- Expected effective state: every in-scope path has fresh, attributable data at its intended destination.
- Positive test: approved DNS/HTTPS and NET-WATCH events are traced successfully.
- Negative test: an intentionally out-of-scope coverage assertion is rejected and documented as a visibility gap.
- Evidence record: target health, bounded queries, dashboard timestamps, and validation record.
- Last successful validation: Phase 7 capability validation completed; this standalone runbook remains unvalidated.

## Rollback and recovery

- Rollback trigger: a test degrades production telemetry or causes uncontrolled volume.
- Recovery steps: stop test generation, restore the last known-good configuration, and use RB-009 for the affected path.
- Restored-state verification: normal collection resumes and no test source continues emitting.

## Stop conditions

Stop on scope loss, broad telemetry loss, unsafe impact, real data, uncontrolled volume or cost, uncertain cleanup, or loss of recovery capability.

## Closure

- Success criteria: each in-scope telemetry path is proven or recorded as an owned gap.
- Remaining risk: retain the wireless-capture and single-node search limitations until architecture changes.
- Follow-up owner: COC Operations.
- Documentation to update: validation record, risk register, and phase evidence index.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Operations | Initial draft for the Phase 7 telemetry backbone |
