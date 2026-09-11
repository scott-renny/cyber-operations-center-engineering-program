# Phase 9 — File Access & Sync (Nextcloud Platform)

**Status: COMPLETE**  
**Completed: September 10, 2026 EDT (UTC−04:00) / September 11, 2026 UTC**

## Purpose and implemented architecture

Provide private file access and synchronization on Atlas using Nextcloud 34.0.3. Windows clients connect over Tailscale, resolve the private canonical hostname through the private DNS path, and use HTTPS through Caddy. The Apache application is published only on loopback; PostgreSQL 17 and Redis 7 support the application, with a separate Nextcloud cron container.

The canonical hostname is the consistent client entry point. Caddy internal-CA trust and private DNS are client prerequisites. This does not imply public Internet exposure. Existing access paths and rollback blocks remain until a concrete, validated reason supports changing them.

## Completion and validation record

This sanitized closeout records the owner's completed Phase 9 acceptance session, including supplied command output and the final browser-access confirmation. These are prior acceptance results, not a claim that the closeout editor repeated live tests.

| Acceptance area | Recorded result |
|---|---|
| Application | Nextcloud 34.0.3 installed; maintenance off; no database upgrade required |
| Private access | Tailscale and canonical HTTPS access working |
| Windows clients | Windows 11 laptop configured, including Virtual Files; Windows 10 PC confirmed complete |
| Identity and notifications | 2FA and outbound email working |
| File monitoring | Wazuh FIM proven with a real alert |
| Malware scanning | ClamAV integration proven with EICAR |
| Recovery | Dedicated encrypted Restic backup and database restore proven |
| Repository health | Restic integrity check returned no errors; retention/prune tested |
| Persistence | App, cron, PostgreSQL, Redis, Tailscale, Caddy, ClamAV and backup timers recovered after reboot |
| User acceptance | Canonical site opened after reboot, authenticated, with files accessible |

## Backup operations

The dedicated Nextcloud backup covers application data and configuration, custom apps and themes, deployment files and protected secrets, plus a PostgreSQL dump. Secrets and raw backup contents remain private.

| Schedule (UTC) | Operation |
|---|---|
| Daily 02:30 | Nextcloud backup |
| Daily 04:30 | Retention/prune: 7 daily, 4 weekly, 3 monthly |
| Sunday 05:30 | Restic repository integrity check |

All three systemd timers are enabled and use persistent scheduling for missed runs. Keep the dedicated Nextcloud lifecycle separate from the existing home-backup schedule. A successful backup alone is insufficient; preserve restore validation as an operational requirement.

## Accepted scope and follow-up

Galaxy S25 and Galaxy Tab A11 Nextcloud onboarding are deliberately deferred, not failed acceptance items and not Phase 9 blockers. Their existing endpoint baseline completion remains intact. Phase 8.5 remains independently blocked on Cerberus hardware. Phase 10 remains planned until explicitly activated.

Live Caddy and portal closeout must compare against the actual deployed files before any edit. The Phase 2 portal/config in this repository is historical evidence, not a current deployment source. Preserve working services and rollback blocks; validate any candidate Caddy configuration before a reload and verify existing routes afterward. Live inspection/deployment is not asserted by this record.

## Lessons and troubleshooting

Use one canonical hostname across clients. For access failures, check Tailscale connectivity, private DNS, certificate trust, then Caddy and application health. For backup failures, inspect the dedicated systemd job and protected logs; do not weaken log or secret permissions. Scope optional device onboarding separately so it does not reopen completed work.

See the [program roadmap](../../ROADMAP.md) and [architecture](../../ARCHITECTURE.md).
