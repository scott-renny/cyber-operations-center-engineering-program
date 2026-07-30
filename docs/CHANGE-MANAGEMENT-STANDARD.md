# Change Management Standard

**Status:** Approved  
**Owner:** COC Program  
**Review cadence:** Annual and after failed or emergency changes

## Purpose

Ensure infrastructure, security, automation, detection, and documentation changes are authorized, testable, reversible, and traceable.

## Required change record

Record:

- change identifier, owner, date, and affected scope;
- purpose and expected outcome;
- risk, dependencies, and security impact;
- backup or recovery preparation;
- implementation plan;
- validation plan and success criteria;
- rollback trigger and exact recovery steps;
- evidence and final result;
- remaining risk and follow-up owner.

## Change classes

| Class | Use |
|---|---|
| Standard | Low-risk, repeatable, previously validated procedure |
| Normal | Planned change requiring explicit review and validation |
| Emergency | Time-sensitive containment or recovery action |

Emergency changes may shorten approval, but never eliminate scope, evidence, validation, recovery, or retrospective review.

## Execution rules

- Preserve administrative access before changing authentication, networking, firewall, or remote-management controls.
- Validate syntax before reload or restart when tooling exists.
- Stage high-impact changes in an isolated or reversible environment.
- Stop when scope, telemetry, safety, cost control, or rollback capability is lost.
- Do not combine unrelated changes when separate validation is practical.

## Closure

A change closes only after effective-state verification, evidence capture, documentation updates, and ownership of residual work. Failed and rolled-back changes remain part of the engineering record.

## Related controls

- [Contributing](../CONTRIBUTING.md)
- [Documentation Standards](../DOCUMENTATION-STANDARDS.md)
- [Risk Register](../RISK-REGISTER.md)
