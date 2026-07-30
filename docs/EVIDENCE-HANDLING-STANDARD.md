# Evidence Handling Standard

**Status:** Approved  
**Owner:** COC Program  
**Review cadence:** Annual and after evidence-handling failures

## Purpose

Define minimum handling requirements for operational, incident, forensic, validation, and portfolio evidence.

## Requirements

Every evidence item must record:

- case, change, test, or campaign identifier;
- collector and collection time;
- source asset or system using an approved sanitized identifier;
- description and purpose;
- original filename or evidence identifier;
- integrity hash when the evidence may support an investigation;
- storage location and access classification;
- transformations, exports, or redactions;
- retention and disposition decision.

Original evidence is preserved read-only when practical. Analysis occurs on a working copy. Forensic acquisition requires chain-of-custody records and cryptographic hashes.

## Time standard

Telemetry uses UTC wherever supported. Reports may include local time only with the UTC offset. Time-source problems and clock drift are recorded as evidence limitations.

## Public release

Before publication:

- remove credentials, tokens, cookies, keys, private certificates, and recovery material;
- remove live addresses, serials, MAC addresses, personal data, and unnecessary usernames;
- review screenshots for reflective or background disclosure;
- replace exact operational commands and thresholds with safe examples when disclosure would weaken security;
- retain the publication decision and reviewer.

Sanitization never alters the private original. Public copies must be clearly distinguishable.

## Integrity and custody

Use SHA-256 or a stronger approved hash for forensic or high-value evidence. Record every custody transfer, export, re-hash, and final disposition. A broken chain of custody must be disclosed; it must not be silently reconstructed.

## Retention

Retention follows [Data Governance](DATA-GOVERNANCE.md). Legal, privacy, platform, and storage constraints override convenience. Evidence no longer required is securely disposed of and the decision is recorded.

## Related templates

- [Evidence Log](../templates/EVIDENCE-LOG-TEMPLATE.md)
- [Incident Case](../templates/INCIDENT-CASE-TEMPLATE.md)
- [Validation Record](../templates/VALIDATION-RECORD-TEMPLATE.md)
