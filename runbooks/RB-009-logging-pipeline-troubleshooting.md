# Runbook: Logging Pipeline Troubleshooting

**Document ID:** RB-009  
**Status:** Draft  
**Owner:** COC Operations  
**Related phases:** 4, 6, and 7  
**Version:** 0.1  
**Last reviewed:** 2026-08-04  
**Next review:** 2026-11-04

## Purpose

Restore expected log flow while preserving evidence and avoiding duplicate, dropped, or misrouted events.

## Trigger and scope

- Trigger: a source stops reporting, ingestion lag rises, searches return incomplete results, or a collector reports failure.
- Authorized systems: NET-WATCH journal forwarding, Graylog, Wazuh, Zeek, Suricata, and their local collectors.
- Exclusions: destructive index repair, retention changes, and deletion of raw evidence without an approved change record.
- Required access: read access to dashboards and logs; privileged service access only for the affected stage.

## Prerequisites

- Open a change or incident record and record the last known-good event time.
- Preserve representative source and destination evidence before restarting services.
- Confirm storage capacity, system time, and a current recovery point.
- Use only sanitized asset identifiers in public evidence.

## Procedure

1. Define the affected source, expected destination, event type, and time window.
2. Confirm whether the source is producing new events.
3. Check the local collector or forwarder state and its recent bounded logs.
4. Verify listener state, bind address, protocol, and the intended local firewall path.
5. Confirm the destination is accepting events and that the expected input or index is active.
6. Inject or generate one approved benign test event.
7. Trace the test event from source, through the transport, to the searchable destination.
8. Correct only the first failed stage. Prefer a controlled service restart before configuration change.
9. Repeat the test and document event timestamps, lag, and any duplicates.
10. Monitor the pipeline through two expected collection intervals before closure.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Source does not produce events | Escalate to the source-service owner |
| Collector fails after one controlled restart | Preserve logs and open a change for configuration repair |
| Destination storage is constrained | Stop ingestion changes and escalate as SEV-2 or SEV-3 based on visibility impact |
| Multiple security sources are unavailable | Treat as a security-visibility incident and assign the higher reasonable severity |
| Test event reaches the wrong index | Stop and correct routing before resuming normal operation |

## Validation

- Expected effective state: new source events are searchable in the intended platform with acceptable lag.
- Positive test: one benign event is traced end to end.
- Negative test: one intentionally invalid or unreachable test input is rejected and recorded without affecting production flow.
- Evidence record: service state, bounded logs, input state, query result, and timestamps.
- Last successful validation: not yet completed for this standalone procedure.

## Rollback and recovery

- Rollback trigger: higher event loss, duplicates, unsafe resource use, or loss of another pipeline.
- Recovery steps: restore the last known-good configuration, restart only affected components, and re-run the benign trace.
- Restored-state verification: normal events and the controlled test appear once in the correct destination.

## Stop conditions

Stop on scope loss, telemetry loss outside the affected pipeline, unsafe impact, real data exposure, uncontrolled storage growth, uncertain cleanup, or loss of recovery capability.

## Closure

- Success criteria: the failed stage is identified, corrected, and observed through two intervals.
- Remaining risk: document any unmonitored source, unbounded lag, or single point of failure.
- Follow-up owner: COC Operations.
- Documentation to update: affected phase record, risk register, and this runbook when the procedure changes.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-08-04 | COC Operations | Initial draft grounded in implemented logging paths |
