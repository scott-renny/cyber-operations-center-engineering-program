# Phase 6 — NET-WATCH

> **Status:** Complete  
> **Completed:** 2026-08-03  
> **Next phase:** Phase 7 — Telemetry Platform

## Purpose

Deploy the maintained NET-WATCH platform as the network-visibility and profile-based DNS access-control layer for the Cyber Operations Center.

## Completed capabilities

- Continuous discovery of real LAN devices
- Device naming, device-type classification, and profile assignment
- Assigned/unassigned and device-type views
- Profile schedules and daily usage budgets
- Manual profile kill switches
- Pi-hole v6 group-based enforcement
- Per-profile content-filtering policies
- Wazuh alert display with MITRE ATT&CK context
- Private HTTPS delivery through the existing Caddy management plane
- Gunicorn API service managed by systemd
- Protected runtime configuration and health diagnostics
- Local timezone configuration and network DNS integration

## Architecture

```text
Managed devices
      |
Network discovery
      |
NET-WATCH API (Gunicorn, localhost only)
      |-- Pi-hole v6 group policy
      |-- Wazuh alert data
      |-- vnStat bandwidth data
      |
Caddy private HTTPS
      |
NET-WATCH dashboard
```

## Pi-hole enforcement design

NET-WATCH does not use Pi-hole's global disable function. It keeps filtering active and changes only the groups assigned to managed profiles.

A dedicated empty control group anchors the NET-WATCH-managed deny-all expression. When a profile is outside its schedule, has exhausted its budget, or is manually blocked, that profile's Pi-hole group is associated with the managed rule. Reconciliation checks keep desired and actual Pi-hole state aligned.

Safety checks reject unsafe targets such as the default group, missing or disabled groups, foreign managed rules, and a control group containing clients.

## Validation summary

The completed deployment was validated by:

- confirming API and HTTPS health;
- discovering and classifying real devices;
- assigning devices to the Matthew and Sophia profiles;
- exercising profile schedules and budgets;
- confirming profile-specific Pi-hole enforcement;
- confirming safe reconciliation with no warnings;
- displaying Wazuh alerts and MITRE ATT&CK context; and
- confirming service operation under systemd and Gunicorn.

## Security considerations

- The API listens only on localhost and is published through private HTTPS.
- Runtime secrets are stored outside the repository in a protected environment file.
- Public documentation excludes passwords, API credentials, device identifiers, addresses, and certificate material.
- Dashboard authentication may be disabled only while access remains limited to the trusted management network; it must be enabled before exposure to less-trusted segments.
- A single Pi-hole host remains a DNS availability dependency until a second independent resolver is deployed.

## Operational outcome

Phase 6 provides a working network operations dashboard with integrated discovery, DNS policy enforcement, usage controls, and SIEM visibility. The platform is stable and will remain in service until its next planned version update.

## Source repository

The maintained application and deployment assets are available in [scott-renny/netwatch](https://github.com/scott-renny/netwatch).
