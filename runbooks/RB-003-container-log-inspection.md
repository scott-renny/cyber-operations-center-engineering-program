# Runbook: Container Log Inspection

**Document ID:** RB-003  
**Status:** Draft  
**Owner:** COC Program Owner  
**Related phase:** Phase 3 — Container Platform and Service Management  
**Version:** 0.1  
**Last reviewed:** 2026-07-31  
**Next review trigger:** First controlled event traced through container logs

## Purpose

Collect and review the minimum container log data needed to diagnose an operational or security event without exposing secrets or exhausting host storage.

## Trigger and scope

- **Trigger:** unhealthy service, alert, failed deployment, application error, or approved troubleshooting request;
- **Authorized systems:** approved COC containers and Docker service logs;
- **Exclusions:** unrelated household data, unrestricted full-history exports, and public posting of raw logs;
- **Required access:** read access to Docker and the relevant case or change record.

## Prerequisites

- Affected service, timeframe, and question defined;
- host time and timezone understood;
- evidence or change record opened when the result may support an incident;
- sufficient storage for any bounded export;
- sanitization requirements understood.

## Procedure

1. Record the UTC timeframe, affected container, and investigation objective.
2. Confirm container state, start time, image, restart count, and health-check state.
3. Review recent logs using the narrowest practical time window.
4. Expand the window only when the initial evidence requires it.
5. Compare application logs with Docker service and host journal events when the failure may be outside the container.
6. Record relevant event timestamps and identifiers in the private record.
7. Export only the bounded evidence required for the case or change.
8. Hash retained evidence when integrity matters.
9. Sanitize usernames, addresses, tokens, cookies, private filenames, and unrelated data before publication.
10. Record the finding, limitation, and next diagnostic action.

Representative bounded checks:

```bash
docker ps --all
docker inspect <container>
docker logs --since 30m --timestamps <container>
sudo journalctl -u docker --since "<approved-time>"
```

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Logs contain credentials or tokens | Restrict evidence, remove exposure, and rotate affected material |
| Container repeatedly restarts | Correlate exit state, health checks, host resources, and dependencies |
| Required period has rotated out | Record the visibility gap; do not reconstruct unsupported events |
| Log growth threatens storage | Preserve minimum evidence and address the source before expanding collection |
| Evidence suggests compromise | Open or update the appropriate incident case |

## Validation

- **Expected effective state:** a known event can be located with correct timestamps and without excessive collection;
- **Positive test:** controlled application event is traced through bounded logs;
- **Negative or failure test:** unrelated older data is excluded by the collection window;
- **Evidence record:** runbook validation record;
- **Last successful validation:** Docker log policy was validated in Phase 3; event-tracing validation remains pending.

## Rollback and recovery

This procedure is read-only by default. If temporary diagnostic logging is enabled under a separate change, return it to the approved level and verify normal storage growth.

## Stop conditions

Stop on secret exposure, collection outside authorized scope, storage exhaustion risk, unexpected personal data, or inability to preserve required evidence integrity.

## Closure

- Investigation question answered or visibility gap recorded;
- evidence retained and hashed where required;
- public copy sanitized;
- temporary logging removed;
- follow-up owner assigned.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-07-31 | COC Program Owner | Initial draft based on the completed Phase 3 logging baseline |

