# ADR-006: Core network and security services remain merged

- **Status:** Accepted
- **Date:** 2026-07-27
- **Owner:** COC Program Owner
- **Related phase(s):** Phase 4
- **Related risk(s):** R-026, R-009, R-023

## Context

Pi-hole DHCP/DNS, Suricata rules, VLAN references, Wazuh ingestion, and network controls were built and debugged as an interdependent unit.

## Decision

Keep Core Network Services and the Core Security Stack within one Phase 4 implementation boundary, while documenting component-level dependencies and validation separately.

## Alternatives Considered

Split into separate sequential phases; deploy security tooling before network services; deploy network services without integrated telemetry.

## Rationale

The real operational dependency chain is more important than clean category grouping. Joint validation proves that network changes produce expected security telemetry.

## Security Implications

Changes require staged tests, rollback, telemetry validation, and explicit identification of blast radius.

## Consequences

Phase 4 is larger and needs clear sub-milestones, but avoids artificial handoffs and incomplete end-to-end validation.

## Validation

The related phase must link implementation evidence, test results, rollback/recovery validation, and any remaining risk before it is marked complete.

## Review Date or Trigger

Review when the related architecture materially changes, a control fails, or a new alternative changes the decision basis.
