# Runbook: Alert Triage

**Document ID:** RB-006  
**Status:** Draft  
**Owner:** COC Program Owner  
**Related phase:** Phase 4 — Core Network and Security Services  
**Version:** 0.1  
**Last reviewed:** 2026-07-31  
**Next review trigger:** Completion of two controlled alert investigations

## Purpose

Assess a Wazuh security alert consistently, determine whether it is a true positive, document the evidence, and route confirmed activity to the appropriate response path.

## Trigger and scope

- **Trigger:** high-priority Wazuh alert or operator-selected alert requiring investigation;
- **Authorized systems:** COC-owned assets and telemetry implemented through the current phase;
- **Exclusions:** third-party systems, unsupported attribution, and Suricata runtime telemetry while the sensor remains disabled;
- **Required access:** Wazuh dashboard and approved read access to relevant source logs.

## Prerequisites

- Wazuh services and relevant log source confirmed healthy;
- server and analyst clocks understood;
- severity standard available;
- case or triage record opened;
- affected asset and telemetry source identified;
- raw evidence retained privately before sanitization.

## Procedure

1. Record the alert ID, UTC time, rule, level, source, affected asset, and initial severity.
2. Preserve the original alert and enough surrounding telemetry to reconstruct the event.
3. Confirm that the alert source is currently implemented and healthy.
4. Compare the alert with the source log, system state, or known test action.
5. Establish the relevant time window and search for related events on the same asset or identity.
6. Check for known maintenance, approved testing, baseline behavior, and documented false-positive conditions.
7. Classify the alert as true positive, benign true positive, false positive, or inconclusive.
8. For a true or inconclusive security event, identify immediate containment needs and activate the applicable playbook when available.
9. For a false positive, document the reason and whether detection tuning is warranted.
10. Record evidence, visibility gaps, decision, owner, and follow-up.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Active compromise or destructive behavior suspected | Escalate severity and contain within current authority |
| Alert source is unhealthy or missing | Record a visibility gap and troubleshoot collection before dismissing |
| Known controlled test matches exactly | Record as benign true positive and retain validation evidence |
| Evidence conflicts or is incomplete | Keep the disposition inconclusive and expand bounded collection |
| Alert depends on Suricata runtime data | Do not claim coverage; sensor remains intentionally disabled |

## Validation

- **Expected effective state:** analyst can trace alert to source evidence and make a supported disposition;
- **Positive test:** controlled event generates an alert and is correctly classified;
- **Negative or failure test:** benign comparison event is not incorrectly escalated;
- **Evidence record:** alert-triage validation record;
- **Last successful validation:** EICAR produced a ClamAV-to-Wazuh level-8 alert in Phase 4; the two-alert validation gate remains incomplete.

## Rollback and recovery

This procedure is read-only unless a separate containment action is approved. Any temporary diagnostic changes must be reverted and validated under the Change Management Standard.

## Stop conditions

Stop automated or intrusive follow-up on scope ambiguity, telemetry loss, suspected real compromise beyond current authority, unsafe containment impact, or exposure of private household data.

## Closure

- Disposition supported by evidence;
- severity and ownership recorded;
- true positive handed to an applicable response path;
- false-positive reasoning and tuning need documented;
- evidence sanitized before any public use;
- unresolved visibility gap assigned.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-07-31 | COC Program Owner | Initial draft based on Phase 4 Wazuh and ClamAV validation |
