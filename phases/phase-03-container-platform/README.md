# Phase 3 — Container Platform and Service Management

**Status:** Complete  
**Completion date:** 2026-07-30  
**Budget:** $0  
**Asset ID:** `coc-srv-01`  
**Friendly name:** Atlas

## Goal

Establish a consistent, secured container platform for later services by deploying Docker Engine, Docker Compose, Dockge, container-networking conventions, naming and labeling standards, bounded container logs, and a Compose-compatible secrets policy.

## Scope

Phase 3 covered:

- Docker Engine and Docker Compose installation from Docker's official Ubuntu repository;
- non-root Docker CLI access for the administrative account;
- successful execution of Docker's `hello-world` validation container;
- Dockge deployment with persistent application and stack directories;
- HTTPS access to Dockge through the existing Caddy gateway;
- localhost-only binding for Dockge's native HTTP port;
- a LAN-restricted UFW rule for the Caddy Dockge endpoint;
- per-stack `frontend` and internal `backend` network conventions;
- lowercase kebab-case container naming and operational labels;
- host-wide Docker log rotation; and
- a Docker Compose secrets standard for applications that support file-based secrets.

Docker Swarm was not initialized. Dockge manages ordinary Compose stacks, and enabling Swarm solely for secrets would introduce a second deployment model without a current operational requirement.

## Architecture

```text
Administrative workstation
        │
        │ trusted local HTTPS
        ▼
┌──────────────────────────────────────────────┐
│ coc-srv-01                                   │
│                                              │
│ Caddy :8443                                  │
│   └── reverse proxy ──► 127.0.0.1:5001      │
│                         Dockge               │
│                           │                  │
│                           ▼                  │
│                    Docker Engine             │
│                           │                  │
│             ┌─────────────┴─────────────┐    │
│             ▼                           ▼    │
│        frontend                    backend   │
│        bridge                      internal  │
└──────────────────────────────────────────────┘
```

Dockge's native HTTP listener is bound only to `127.0.0.1`. Caddy terminates HTTPS on a separate internal port, and UFW limits that port to the trusted LAN.

## Installed platform

| Component | Validated state |
|---|---|
| Ubuntu Server | 24.04.4 LTS |
| Docker Engine | 29.6.2 |
| Docker Compose | v5.3.1 |
| Dockge | Healthy |
| Caddy proxy | HTTP/2 success |
| Docker logging | `json-file`, `10m`, three files |

These versions record the completion state and are not immutable pins for future maintenance.

## Dockge deployment

| Purpose | Path |
|---|---|
| Dockge Compose definition | `/opt/dockge/compose.yaml` |
| Dockge persistent data | `/opt/dockge/data` |
| Managed Compose stacks | `/opt/stacks` |
| Docker daemon configuration | `/etc/docker/daemon.json` |
| Architecture standard | `ARCHITECTURE.md` |

The public repository includes sanitized examples only. Runtime data, credentials, JWT material, private certificates, and application databases are excluded.

## Network standard

Each application stack should define its own `frontend` and `backend` networks:

```yaml
networks:
  frontend:
    driver: bridge
  backend:
    driver: bridge
    internal: true
```

User-facing services and components that require outbound access use `frontend`. Databases and private application components use only `backend`. A service may join both only when it must bridge a user-facing request to a private dependency.

Compose scopes these networks to the stack by default. Shared external networks require an explicit architecture decision.

## Naming and labels

Stack directories, service names, and explicit container names use lowercase kebab-case and describe workload function, for example:

- `misp-server`
- `thehive-app`
- `cortex-worker`
- `dlp-watchd`

Operational labels identify the program, phase, and role:

```yaml
labels:
  coc.program: "cyber-operations-center"
  coc.phase: "phase-04"
  coc.role: "threat-intelligence"
```

Phase numbers normally belong in labels instead of container names.

## Log rotation

Docker's host-wide daemon configuration uses the `json-file` driver with a maximum size of 10 MB and three retained files per container. New containers inherit this policy. Containers that predate the configuration must be recreated to inherit it.

## Secrets policy

Dockge-managed stacks use Docker Compose secrets when the target application supports a file reference such as `/run/secrets/<secret-name>`.

```yaml
services:
  app:
    secrets:
      - app-password
    environment:
      APP_PASSWORD_FILE: /run/secrets/app-password

secrets:
  app-password:
    file: ./secrets/app-password
```

Secret source files must use mode `0600`, remain outside version control, and never appear in screenshots or validation output. File-backed Compose secrets reduce exposure through environment variables and ordinary inspection, but they are not encrypted at rest.

## Validation checklist

- [x] Docker Engine installed and daemon active
- [x] Docker commands run without `sudo`
- [x] `hello-world` completed successfully
- [x] Docker Compose plugin available
- [x] Dockge container healthy
- [x] Dockge native port bound to localhost only
- [x] Caddy Dockge endpoint returns HTTP/2 200
- [x] UFW permits the Dockge HTTPS endpoint only from the trusted LAN
- [x] Frontend/backend network convention documented
- [x] Naming and labeling convention documented
- [x] Docker daemon configuration validated
- [x] Dockge recreated with the bounded logging configuration
- [x] Compose-compatible secrets policy documented
- [x] Public evidence sanitized

## Security considerations

- Docker group membership is equivalent to highly privileged host access and is limited to the administrative account.
- Dockge has access to the Docker socket and must be treated as an administrative control plane.
- Dockge credentials are unique and are not stored in this repository.
- Dockge's native HTTP port is not exposed to the LAN.
- HTTPS uses Caddy's previously verified internal authority.
- The added firewall rule is limited to the trusted local subnet.
- Docker logs are bounded to reduce disk-exhaustion risk.
- Backend-only networks use `internal: true` to remove their external route.
- A service attached to both networks can still relay traffic; dual-homed services require careful review.
- No secret, live address, private certificate, token, or raw screenshot is committed.

## Troubleshooting record

### Docker group membership did not apply immediately

The account was added to the `docker` group, but the existing SSH session retained its original group list. Logging out and reconnecting applied the new membership.

### Dockge initially reported a missing database configuration

The first-start message was expected. Dockge created its SQLite configuration and generated its JWT secret before reporting that initial account setup was required.

### UFW did not provide the intended Dockge isolation alone

Docker-published ports interact directly with the host packet-filtering stack. The Compose mapping was changed from all interfaces to `127.0.0.1:5001:5001`, and Caddy became the only network-facing path.

### Long terminal pastes were truncated

Documentation was entered in smaller verified sections. Balanced Markdown fences and section headings were checked before completion.

### Swarm secrets conflicted with the selected management model

The initial plan suggested initializing Swarm for encrypted secrets while using Dockge for ordinary Compose stacks. The final standard keeps one deployment model: Docker Compose secrets are used where supported, and the lack of at-rest encryption is documented accurately.

## Lessons learned

- Installation success is not enough; effective permissions and an unprivileged test must also be validated.
- Management interfaces deserve the same HTTPS and network restrictions as production applications.
- Host firewall state does not replace explicit bind-address control for container-published ports.
- Internal Docker networks reduce exposure but do not replace application-layer authorization.
- Logging limits should be configured before service count grows.
- Secrets guidance must match the actual deployment orchestrator.
- Sanitized evidence should prove control state without disclosing operational details.

## Known limitations and deferred work

- The host remains dependent on Wi-Fi and DHCP pending the earlier network follow-ups.
- Dockge is protected by its own account but does not yet sit behind centralized identity or MFA.
- Compose file-backed secrets are not encrypted at rest; a dedicated secret manager may be evaluated later.
- Container image update, vulnerability-scanning, backup, and recovery procedures remain future work.
- Runtime metrics and centralized logs will be introduced in later observability phases.

## Evidence

Sanitized validation results and the public-release decision are recorded in [evidence/README.md](evidence/README.md). Reusable configuration examples are stored under [config/](config/).

## Outcome

Atlas now provides a validated Docker and Dockge foundation with private HTTPS management, bounded logs, per-stack network segmentation, consistent naming and labeling, and a secrets pattern aligned with Docker Compose.

The environment is ready for **Phase 4 — Core Network and Security Services**.
