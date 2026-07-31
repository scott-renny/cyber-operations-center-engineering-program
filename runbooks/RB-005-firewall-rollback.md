# Runbook: Firewall Rollback

**Document ID:** RB-005  
**Status:** Draft  
**Owner:** COC Program Owner  
**Related phase:** Phase 4 — Core Network and Security Services  
**Version:** 0.1  
**Last reviewed:** 2026-07-31  
**Next review trigger:** First dedicated rollback validation

## Purpose

Reverse an approved UFW rule change safely when it causes unexpected loss of access, excessive exposure, or service impact.

## Trigger and scope

- **Trigger:** failed firewall validation, lost service access, unintended exposure, or explicit rollback decision;
- **Authorized systems:** UFW policy on Atlas;
- **Exclusions:** router, provider, container-internal, or future Project Olympus controls not governed by UFW;
- **Required access:** privileged local or remote administration with a proven recovery path.

## Prerequisites

- Current firewall state and proposed change recorded;
- exact pre-change rule state preserved privately;
- local console or independent second administrative session available;
- affected LAN and VPN paths identified;
- rollback command prepared before applying the original change;
- functional tests and stop conditions defined.

## Procedure

1. Record the change ID, UTC time, symptom, affected service, and access path.
2. Use the preserved administrative session or local console; do not disconnect the only working path.
3. Confirm the effective UFW state and identify the specific changed rule.
4. Reverse only the failed rule or restore the last approved bounded rule set.
5. Validate UFW syntax and effective state.
6. Test the intended service from an approved LAN source.
7. Test the intended service through WireGuard when that path is in scope.
8. Confirm unauthorized or out-of-scope sources remain blocked.
9. Verify SSH, Caddy, Dockge, Wazuh, Pi-hole, and WireGuard access only where applicable to the change.
10. Record the rollback result and decide whether the original change requires redesign.

Representative read-only check:

```bash
sudo ufw status numbered
```

Exact rules and operational addresses remain in the private change record.

## Decision and escalation points

| Condition | Decision or escalation |
|---|---|
| Only remote access is lost | Use local console; avoid repeated blind rule changes |
| Rollback restores access but broadens exposure | Apply a temporary bounded rule and open corrective work |
| UFW state is correct but service remains unavailable | Investigate bind address, reverse proxy, container publishing, and service health |
| WireGuard entry path is affected | Preserve LAN/local administration and validate the VPN service separately |
| Current state cannot be reconstructed | Stop and rebuild from the approved private baseline |

## Validation

- **Expected effective state:** authorized management access works and out-of-scope access remains blocked;
- **Positive test:** approved rule change can be reversed without losing the recovery session;
- **Negative or failure test:** unauthorized source remains denied after rollback;
- **Evidence record:** Phase 4 validation plus dedicated rollback record;
- **Last successful validation:** Phase 4 firewall changes were staged and access preserved; a dedicated runbook test remains pending.

## Rollback and recovery

This runbook is itself the rollback procedure. If the attempted rollback worsens state, stop, use local console access, and restore the approved private UFW baseline.

## Stop conditions

Stop on loss of all administrative access, uncertainty about the active rule set, unexpected public exposure, impact outside Atlas, or absence of a local recovery path.

## Closure

- Authorized and denied paths tested;
- temporary broad access removed;
- failed change and restored state documented;
- residual exposure assigned;
- baseline and architecture documentation updated if needed.

## Revision history

| Version | Date | Author | Change |
|---|---|---|---|
| 0.1 | 2026-07-31 | COC Program Owner | Initial draft based on Phase 4 firewall implementation |

