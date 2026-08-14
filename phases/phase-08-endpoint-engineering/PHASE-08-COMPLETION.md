# Phase 8 Completion Report — Endpoint Engineering

> **Status:** Complete  
> **Completion date:** 2026-08-13  
> **Follow-on:** Phase 8.5 — Fedora Workstation Migration

## Executive summary

Phase 8 established documented security baselines across the laptop, legacy workstation, mobile phone, and tablet. Controls were adapted to each platform. Validation combined native protections, secure connectivity, centralized telemetry, malware remediation, recovery testing, and explicit exception management.

## Completed workstreams

- [COC-LT-01](COC-LT-01/PHASE-08-COMPLETION.md) — Windows 11 Home laptop, dual WireGuard profiles, Wazuh, browser hardening, and initial hardware-key enrollment
- [COC-WS-01](COC-WS-01/PHASE-08-COMPLETION.md) — Windows 10 pre-migration baseline, Sysmon, Wazuh, remediation, and approved recovery source
- [Galaxy S25](GALAXY-S25/README.md) — Samsung and Android mobile baseline with protected connectivity
- [Galaxy Tab A11](GALAXY-TAB-A11/README.md) — Samsung and Android tablet baseline with tablet-specific recovery controls

## Lessons learned

- Audit modes expose compatibility impact before enforcement.
- Generic interpreters must not be broadly allow-listed to suppress Controlled Folder Access noise.
- Malware findings must be removed from both source endpoints and backup staging.
- Clean scans are stronger when paired with a new snapshot and an actual restore comparison.
- Historical snapshots containing unsafe files require explicit restore warnings.
- Enrollment services should be open only during enrollment.
- Platform differences require compensating controls and accurate completion criteria.
- Security-key enrollment needs an inventory and tested recovery plan; it should not be rushed.

## Residual risk

- The Windows 10 workstation remains unencrypted until retirement.
- Centralized enforcement varies across Windows editions and mobile platforms.
- Some controls depend on connectivity through the approved VPN.
- Additional FIDO2 enrollment and tablet NFC determination remain deferred.
- Mobile evidence is summarized to protect device and account details.

## Completion decision

Phase 8 is complete. [Phase 8.5](../phase-08-5-workstation-migration/README.md) is the next controlled workstream and is not included in this claim. Phase 9 remains not started.
