# ADR-004: Pi-hole group-API kill switch instead of global disable

- **Status:** Accepted
- **Date:** 2026-07-27
- **Owner:** COC Program Owner
- **Related phase(s):** Phases 4 and 6
- **Related risk(s):** R-023

## Context

NET-WATCH needs targeted DNS-layer access control. Globally disabling Pi-hole affects unrelated household devices and removes broader DNS security visibility.

## Decision

Change group assignments through the Pi-hole API for the intended profile/device rather than globally disabling DNS filtering.

## Alternatives Considered

Global Pi-hole disable; firewall-only blocking; per-device manual administration.

## Rationale

Scoped control limits blast radius, preserves service for unrelated devices, and creates a more auditable operational action.

## Security Implications

API credentials are restricted; group membership is validated before and after changes; manual recovery and expiration are required.

## Consequences

Dependent on Pi-hole/API availability and accurate device identity; DNS-only control is not a complete network isolation control.

## Validation

The related phase must link implementation evidence, test results, rollback/recovery validation, and any remaining risk before it is marked complete.

## Review Date or Trigger

Review when the related architecture materially changes, a control fails, or a new alternative changes the decision basis.
