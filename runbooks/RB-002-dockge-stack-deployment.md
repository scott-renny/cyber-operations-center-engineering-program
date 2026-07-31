# Runbook: Dockge Stack Deployment

**Document ID:** RB-002  
**Status:** Draft  
**Owner:** COC Program Owner  
**Related phase:** Phase 3 — Container Platform and Service Management  
**Version:** 0.1  
**Last reviewed:** 2026-07-31  
**Next review trigger:** First disposable stack deployment and removal test

## Purpose

Deploy or update an approved Docker Compose stack through the Dockge management plane while preserving secrets, network boundaries, logging limits, and rollback capability.

## Trigger and scope

- **Trigger:** approved new stack, configuration update, or controlled redeployment;
- **Authorized systems:** COC-owned Compose stacks managed by Dockge;
- **Exclusions:** unreviewed images, embedded secrets, shared networks without an architecture decision, and destructive volume replacement;
- **Required access:** Dockge and Docker administrative access.

## Prerequisites

- Approved change record with owner, scope, test, and rollback plan;
- trusted image source and explicit version decision;
- Compose definition reviewed for syntax and minimum privileges;
- frontend/backend network placement reviewed;
- secrets stored outside version control with restricted permissions;
- persistent paths and backup requirements identified;
- expected health and functional tests defined.

## Procedure

1. Record the change ID, UTC start time, stack name, image versions, and expected outcome.
2. Review the Compose definition for privileged mode, host networking, host mounts, published ports, capabilities, and Docker-socket access.
3. Confirm that only required services join the frontend network and private dependencies remain on the internal backend network.
4. Confirm that supported secrets use file-based secret references rather than committed values.
5. Validate the Compose definition before deployment.
6. Preserve the current approved definition and record the running image versions.
7. Deploy or update the stack through Dockge.
8. Confirm expected containers are running and health checks stabilize.
9. Verify bind addresses, published ports, network membership, mounts, and bounded logging.
10. Test the service through its intended private HTTPS or application path.
11. Review recent logs using [RB-003 — Container Log Inspection](RB-003-container-log-inspection.md).
12. Close the change only after effective-state validation.

Representative validation:

```bash
docker compose config --quiet
docker compose ps
docker inspect <container>
docker logs --since 15m <container>
```

Repository paths, credentials, and environment-specific values remain in the private operational record.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Compose validation fails | Do not deploy; correct the definition |
| Image source or version is uncertain | Stop until provenance and version are approved |
| Secret appears in configuration or logs | Stop, remove exposure, and rotate if necessary |
| Health check remains unhealthy | Roll back to the preserved definition |
| Deployment requires broader network exposure | Require security review and documented approval |

## Validation

- **Expected effective state:** stack is healthy, reachable only through approved paths, and uses approved networks, storage, logging, and secrets conventions;
- **Positive test:** disposable stack deploys and passes health checks;
- **Negative or failure test:** invalid definition is rejected before deployment;
- **Evidence record:** Phase 3 validation record plus deployment validation;
- **Last successful validation:** Dockge itself was deployed and validated in Phase 3; a complete disposable deployment-stop-remove cycle remains pending.

## Rollback and recovery

- Restore the preserved Compose definition and approved image versions.
- Avoid deleting persistent volumes during rollback.
- Recreate only the affected containers.
- Verify data access, service health, network exposure, and logs after rollback.

## Stop conditions

Stop on secret exposure, unexpected public binding, unapproved privilege, missing persistent data, uncertain image provenance, loss of rollback capability, or impact outside the approved stack.

## Closure

- Stack and health state confirmed;
- network and bind exposure verified;
- secrets absent from public records and logs;
- rollback material retained;
- change record and documentation updated.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-07-31 | COC Program Owner | Initial draft based on the completed Phase 3 platform |

