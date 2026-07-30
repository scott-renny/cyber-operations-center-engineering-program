# Operational Document Migration Map

**Status:** Active  
**Purpose:** Track movement from legacy or conceptual material into governed COC operational documents.

## Migration rules

1. Preserve the original privately when it contains operational detail or evidence.
2. Classify the document as runbook, playbook, campaign, standard, template, or record.
3. Assign a target COC phase and accountable owner.
4. Apply the current template and governance controls.
5. Mark the public document `Planned` unless controlled validation evidence exists.
6. Sanitize the public copy.
7. Record validation, promotion, supersession, or retirement.

## Mapping

| Source concept | Governed destination | Initial status |
|---|---|---|
| Repeatable administrative procedure | `runbooks/` | Planned |
| Incident coordination procedure | `playbooks/` | Planned |
| Authorized adversary-emulation sequence | `campaigns/` | Planned |
| Case or investigation worksheet | Incident Case Template | Template |
| Test notes | Validation Record Template | Template |
| Evidence spreadsheet or notes | Evidence Log Template | Template |
| Engagement scope | Rules of Engagement Template | Template |
| Retrospective notes | Post-Incident Review Template | Template |
| Policy-like operating rule | `docs/` standard | Approved after governance review |

## Promotion gate

A technical document moves from Planned or Draft to Lab Validated only when:

- the corresponding capability exists;
- prerequisites and scope were confirmed;
- the procedure was executed in a controlled environment;
- success, failure, rollback, and closure criteria were evaluated;
- evidence was retained and a sanitized record prepared;
- remaining risk and follow-up ownership were recorded.

Document status never advances based only on writing completeness.
