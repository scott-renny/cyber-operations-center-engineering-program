# Phase 7 — Telemetry Backbone

> **Status:** Complete  
> **Completed:** 2026-08-04  
> **Next phase:** Phase 8 — Endpoint Engineering

## Purpose

Establish the observability and telemetry layer beneath the existing Cyber Operations Center stack without introducing new detection logic. Phase 7 adds rich network metadata, infrastructure and container metrics, general-purpose log aggregation, and consolidated operational dashboards for later detection, case-management, SOAR, and forensic phases.

## Completed capabilities

- Zeek network metadata collection alongside Suricata
- Live connection, DNS, and TLS metadata
- Prometheus time-series collection
- Host metrics through node_exporter
- Per-container metrics through cAdvisor
- Grafana dashboards for host and container health
- Custom Prometheus metrics for Pi-hole, Wazuh alert volume, backup recency, and collector health
- Custom Grafana COC Operations Overview dashboard
- Graylog 7 centralized collection for non-Wazuh logs
- Dedicated Graylog Data Node and MongoDB services
- Isolated Graylog search-backend ports to avoid conflict with Wazuh
- Dedicated COC General Logs index set with single-node shard and replica settings
- Persistent NET-WATCH journal forwarding into Graylog
- Private Caddy HTTPS endpoints for Grafana, Graylog, and Prometheus
- Updated COC portal service tiles and operational status labels

## Architecture

```text
Network traffic
      |-- Suricata -> signature alerts -> Wazuh
      |-- Zeek -> connection, DNS, and TLS metadata

Ubuntu host
      |-- node_exporter -> Prometheus
      |-- Docker/cAdvisor -> Prometheus
      |-- COC custom collector -> Prometheus
      |                         |-- Pi-hole statistics
      |                         |-- Wazuh alert volume
      |                         |-- backup success age
      |                         `-- collector health
      |
      `-- systemd journal -> NET-WATCH forwarder -> Graylog

Prometheus -> Grafana dashboards
Graylog -> searchable non-Wazuh log archive
Caddy -> private HTTPS management endpoints
```

## Zeek implementation

Zeek operates as the metadata complement to Suricata. Suricata continues identifying known threat patterns, while Zeek records structured connection history for retrospective investigation.

The standalone Zeek sensor was validated with populated connection records containing real DNS and TLS traffic. The monitored wireless interface provides visibility into server-related traffic and traffic that traverses services hosted on the server, including DNS requests to Pi-hole.

## Prometheus and Grafana implementation

Prometheus scrapes three validated targets:

- Prometheus
- node_exporter
- cAdvisor

All targets report `UP`. Prometheus and its exporters remain bound to local interfaces where practical and are published only through the private Caddy management plane.

Grafana includes:

- Node Exporter Full for host CPU, memory, storage, and network visibility
- cAdvisor container overview for per-container resource usage
- COC Operations Overview for Pi-hole, Wazuh, backup, and collector telemetry

The custom collector publishes warning-free Prometheus textfile metrics once per minute. Collector health is visible directly in Grafana.

## Graylog implementation

Graylog provides searchable aggregation for operational logs that do not belong in Wazuh's security-correlation workflow.

The completed deployment includes:

- MongoDB bound locally;
- a Graylog Data Node with search ports isolated from Wazuh;
- a Graylog server behind private Caddy HTTPS;
- a dedicated COC General Logs index set;
- one running Syslog UDP input;
- persistent NET-WATCH journal forwarding; and
- confirmed searchable NET-WATCH application events.

Both public index sets use one primary shard and zero replicas, which is appropriate for the current single-data-node lab.

## Validation summary

Phase 7 was validated by:

- confirming adequate root and backup-disk capacity;
- confirming Zeek remained running after deployment;
- generating and observing live Zeek connection records;
- confirming Prometheus, node_exporter, and cAdvisor service health;
- confirming all Prometheus scrape targets reported `UP`;
- validating the custom metrics file with `promtool`;
- confirming the Pi-hole, Wazuh, and backup collectors each reported success;
- confirming Grafana database health and populated dashboards;
- confirming MongoDB, Graylog Data Node, Graylog server, and the NET-WATCH forwarder were active;
- confirming one Graylog Syslog UDP input was running without input failures;
- searching continuously ingested NET-WATCH messages in Graylog;
- validating the Caddy configuration; and
- confirming the private Grafana, Graylog, and Prometheus HTTPS endpoints responded correctly.

## Validation evidence

Selected sanitized screenshots are indexed in the [Phase 7 validation evidence](evidence/README.md) directory.

## Security considerations

- Native Grafana, Graylog, Prometheus, MongoDB, exporter, and search-backend listeners are restricted to localhost where practical.
- Caddy is the controlled private HTTPS entry point.
- Firewall access is limited to approved management networks.
- Graylog search ports are isolated from Wazuh's existing search backend.
- Pi-hole authentication material remains in a protected Docker secret and is read only by the root-run metrics collector.
- The metrics collector writes atomically to the node_exporter textfile directory.
- Public documentation excludes credentials, live addresses, device identifiers, private certificates, raw logs, and secret values.
- No new detection or automated-response logic was introduced during this phase.

## Known limitations and deferred work

- A wireless capture interface cannot provide complete switched-LAN visibility. Broader packet visibility requires a wired sensor, mirrored switch port, TAP, or equivalent network redesign.
- The single-node Graylog search cluster can report yellow when a managed or older replica shard cannot be assigned. All primary shards remain active, and ingestion and search are operational.
- The attack-origin Geomap remains deferred until the later geo-feed and attack-map implementation phase supplies a validated data source.
- Prometheus's native interface is intentionally a query and target-inspection surface; Grafana remains the dashboard layer.

## Operational outcome

Phase 7 establishes a working telemetry backbone beneath the Cyber Operations Center. Rich network metadata, host and container metrics, security-volume summaries, backup health, DNS statistics, and non-Wazuh application logs now flow into their appropriate platforms.

The environment is ready to support the endpoint-engineering phase and later detection, case-management, SOAR, and forensic workflows.
