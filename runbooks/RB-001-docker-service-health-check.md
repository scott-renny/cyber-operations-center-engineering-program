# Runbook: Docker Service Health Check

**Document ID:** RB-001  
**Status:** Draft  
**Owner:** COC Program Owner  
**Related phase:** Phase 3 — Container Platform and Service Management  
**Version:** 0.1  
**Last reviewed:** 2026-07-31  
**Next review trigger:** First controlled daemon-failure and recovery test

## Purpose

Determine whether Docker and the approved COC containers are operating correctly, identify the failing layer, and restore service without unnecessary changes or data loss.

## Trigger and scope

- **Trigger:** unavailable containerized service, unhealthy container, Docker alert, or scheduled platform check;
- **Authorized systems:** Docker Engine and approved COC stacks on Atlas;
- **Exclusions:** deleting volumes, images, or persistent data as a first response;
- **Required access:** approved Docker administrator access.

## Prerequisites

- Confirm the affected service and observed symptom.
- Preserve a working administrative session and local recovery path.
- Open a change or incident record when service impact is material.
- Identify dependent services before restarting Docker.
- Confirm that no backup, restore, or evidence-collection job will be interrupted.

## Procedure

1. Record the UTC start time, affected service, and user-visible impact.
2. Check host resource health, including storage, memory, and load.
3. Check whether the Docker service is active and enabled.
4. Confirm that the Docker client can communicate with the daemon.
5. List running and stopped containers and note unhealthy or restarting states.
6. Inspect the affected stack through Dockge or Docker Compose.
7. Review bounded recent logs for the affected container and Docker service.
8. Check container exit state, health-check output, network attachment, mounts, and restart count.
9. Restart only the affected container or stack when the fault is isolated.
10. Restart the Docker service only when the daemon itself is the confirmed fault and the impact is approved.
11. Validate the service through its intended HTTPS or application path.
12. Record the cause, action, result, remaining risk, and required follow-up.

Representative read-only checks:

```bash
sudo systemctl is-active docker
sudo systemctl is-enabled docker
docker info
docker ps --all
docker compose ps
```

Use the private operational record for stack locations and environment-specific identifiers.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Host storage is full | Stop restart attempts; preserve logs and address capacity safely |
| Docker daemon is healthy but one container fails | Limit recovery to the affected stack |
| Multiple stacks fail together | Investigate daemon, storage, networking, and shared dependencies |
| Persistent data or mounts are missing | Stop; do not recreate or delete volumes without recovery review |
| Docker socket or administrative access may be compromised | Treat as a privileged host incident |

## Validation

- **Expected effective state:** Docker is active, expected containers are stable, and the affected service passes its functional check;
- **Positive test:** healthy-state checks correctly identify all required components;
- **Negative or failure test:** controlled daemon interruption is detected and safely recovered;
- **Evidence record:** Phase 3 validation record plus runbook-specific validation;
- **Last successful validation:** Healthy-state checks completed in Phase 3; failure-and-recovery test remains pending.

## Rollback and recovery

- **Rollback trigger:** restart increases impact, changes expected state, or exposes a data problem;
- **Recovery steps:** stop further changes, return the affected stack to its last approved definition, and use the applicable backup or rebuild path when available;
- **Restored-state verification:** service health, HTTPS access, container stability, and logs return to the approved baseline.

## Stop conditions

Stop on unexplained data loss, missing volumes, suspected compromise, uncontrolled restart loops, loss of administrative access, or lack of an approved recovery path.

## Closure

- Effective service state confirmed;
- root cause or owned investigation recorded;
- temporary changes removed;
- monitoring reviewed;
- evidence and documentation updated.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-07-31 | COC Program Owner | Initial draft based on the completed Phase 3 platform |

