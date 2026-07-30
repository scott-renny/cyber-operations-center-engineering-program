# Adversary-Emulation Standard

**Status:** Approved  
**Owner:** COC Program  
**Review cadence:** Before every campaign and annually

## Purpose

Define mandatory authorization, safety, evidence, and closure controls for adversary-emulation activity.

## Authorization

No campaign begins without a signed or explicitly approved Rules of Engagement record defining:

- owner and participants;
- authorized systems, accounts, networks, techniques, and time window;
- prohibited targets and actions;
- expected telemetry;
- communication and escalation paths;
- stop authority;
- cleanup, recovery, and credential-revocation requirements.

Authorization applies only to assets controlled by the participant or explicitly permitted by the asset owner.

## Mandatory stop conditions

Stop immediately on:

- loss or ambiguity of scope;
- unexpected real data or third-party systems;
- safety risk or uncontrolled service impact;
- telemetry loss that prevents safe observation;
- uncontrolled cost or resource consumption;
- evidence of a real compromise;
- failed containment or uncertain cleanup;
- instruction from the designated stop authority.

Record the stop decision, preserve evidence, and move to containment or recovery.

## Execution

Campaigns use the least disruptive technique capable of validating the objective. Destructive, persistence, credential-access, denial-of-service, and cloud-cost-generating actions require specific authorization and isolated targets.

Every action must map to an objective and, where applicable, MITRE ATT&CK. Record timestamps, commands or tool actions in the private log, expected detections, actual detections, safety observations, and deviations.

## Closure

A campaign is not complete until:

- test artifacts and persistence are removed;
- temporary accounts, tokens, keys, and rules are revoked;
- affected systems are restored and verified;
- detections and visibility gaps are recorded;
- evidence is retained and public copies sanitized;
- lessons learned and backlog owners are assigned.

## Publication

Public campaign material uses generic assets, safe examples, sanitized evidence, and no reusable offensive secrets or environment-specific attack paths. Planned campaigns are never represented as executed.

## Related templates

- [Campaign Template](../templates/CAMPAIGN-TEMPLATE.md)
- [Rules of Engagement](../templates/RULES-OF-ENGAGEMENT-TEMPLATE.md)
- [Validation Record](../templates/VALIDATION-RECORD-TEMPLATE.md)
