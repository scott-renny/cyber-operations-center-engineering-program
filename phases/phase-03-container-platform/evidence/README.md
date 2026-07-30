# Phase 3 Validation Evidence

This directory records sanitized validation evidence for the Phase 3 container-platform implementation.

## Public-release decision

The public record includes command names, expected control states, component versions, and sanitized configuration examples. It excludes:

- live IP addresses and subnet details;
- usernames and passwords;
- Dockge account details;
- Docker or application secrets;
- private certificate material and fingerprints;
- raw screenshots containing operational context;
- container IDs, image digests, and host-specific runtime identifiers.

The original Dockge dashboard screenshot remains in the private project evidence set.

## Validation summary

| Control | Sanitized result |
|---|---|
| Operating system compatibility | Ubuntu Server 24.04 LTS |
| Docker daemon | Active |
| Non-root Docker access | Successful |
| Docker test container | Completed successfully |
| Docker Compose | Available |
| Dockge health | Healthy |
| Dockge native bind | Localhost only |
| Caddy reverse proxy | HTTP/2 200 |
| Firewall scope | Trusted LAN only |
| Docker daemon JSON | Configuration valid |
| Applied Dockge log policy | `json-file`, `10m`, three files |
| Architecture headings | Network, naming, logging, secrets present |
| Markdown code fences | Balanced |

## Representative commands

The following commands were used to validate the effective state. Their live output is intentionally not reproduced.

```bash
docker version
docker compose version
docker run hello-world
docker compose ps
docker inspect --format '{{json .HostConfig.LogConfig}}' <container>
sudo dockerd --validate --config-file=/etc/docker/daemon.json
sudo caddy validate --config /etc/caddy/Caddyfile
sudo systemctl is-active docker
sudo systemctl is-active caddy
sudo ufw status
curl --resolve <internal-name>:<port>:127.0.0.1 -k -I https://<internal-name>:<port>
```

## Evidence handling

No raw screenshot or terminal capture is committed. Public documentation records only the minimum facts needed to demonstrate that the controls were implemented and tested.
