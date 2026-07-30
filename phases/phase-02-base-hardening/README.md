# Phase 2 — Base Hardening and Operations Portal

**Status:** Complete  
**Completion date:** 2026-07-30  
**Budget:** $0  
**Asset ID:** `coc-srv-01`  
**Friendly name:** Atlas

## Goal

Establish the secure Ubuntu baseline required by later phases and deploy a private HTTPS operations portal only after the host controls were validated.

## Scope

Phase 2 covered:

- migration from SSH password authentication to an Ed25519 key;
- denial of root and password-based SSH login;
- a default-deny UFW firewall policy;
- Fail2Ban protection for SSH;
- AppArmor validation;
- Auditd deployment and kernel-auditing validation;
- automatic security-update validation and operating-system patching;
- installation of Caddy from its official stable repository;
- deployment of a private HTTPS operations portal;
- creation of a standardized asset-ID registry outside the public web root; and
- controlled installation of Caddy's public local-CA certificate on the administrative workstation.

Stable router address assignment was reviewed but remains an explicit follow-up rather than a completed control.

## Architecture

```text
Administrative workstation
        │
        │ SSH key / trusted local HTTPS
        ▼
┌──────────────────────────────────────────┐
│ coc-srv-01                               │
│                                          │
│ SSH ─ UFW ─ Fail2Ban                     │
│ AppArmor ─ Auditd ─ unattended-upgrades  │
│                                          │
│ Caddy                                    │
│ ├── private HTTPS portal                 │
│ └── future reverse-proxy entry point     │
└──────────────────────────────────────────┘
```

Caddy is the web server and future reverse proxy. The custom portal is the current private operations homepage; a richer dashboard application can be introduced behind Caddy later without replacing the HTTPS gateway.

## SSH hardening

The Windows administrative workstation generated an Ed25519 key pair. Only the public key was installed on the server.

The hardened settings are stored in `/etc/ssh/sshd_config.d/00-coc-hardening.conf`:

```text
PubkeyAuthentication yes
PasswordAuthentication no
KbdInteractiveAuthentication no
PermitRootLogin no
```

The `00-` prefix is deliberate. Ubuntu's cloud-init snippet contained `PasswordAuthentication yes`, and OpenSSH normally uses the first value encountered for most directives.

The configuration was checked with `sshd -t`, reloaded, and tested from a fresh terminal. A separate password-only attempt returned `Permission denied (publickey)`.

## Firewall

UFW was installed on the minimized Ubuntu image and configured with default-deny incoming traffic, default-allow outgoing traffic, low-level logging, and inbound allowances for SSH, HTTP, and HTTPS.

Both UFW's runtime policy and systemd startup state were validated. A fresh key-authenticated SSH connection succeeded after activation.

The public record intentionally omits live addresses. Firewall rules should be tightened to explicit trusted networks when the final network segmentation and VPN design are implemented.

## Fail2Ban

Fail2Ban's SSH jail reads authentication events from the systemd journal. The local policy is:

```ini
[sshd]
enabled = true
backend = systemd
maxretry = 5
findtime = 10m
bantime = 1h
```

The configuration passed `fail2ban-client -t`. The service and SSH jail remained active after restart. A deliberate ban test was not performed from the only active administrative workstation because it could interrupt the change session.

## AppArmor and Auditd

AppArmor was already loaded by Ubuntu. Final validation showed 101 loaded profiles, 8 profiles in enforce mode, and 4 Transmission profiles in complain mode.

The complain-mode profiles were not forced into enforcement without application testing. Phase 2 therefore records AppArmor accurately as active with enforced profiles, not as universal confinement.

Auditd was installed, enabled, and started. Kernel auditing reported `enabled 1` and zero lost records at final verification.

## Automatic updates and patching

Ubuntu's existing `unattended-upgrades` configuration enabled daily package-list refreshes and unattended upgrades. Both apt timers were active.

A dry run identified eligible security updates. All pending OpenSSL, library, timezone, and distribution-information updates were applied. No packages or reboot requirement remained at phase completion.

## Caddy operations portal

Caddy `v2.11.4` was installed from its official stable Debian/Ubuntu repository after the operating-system baseline was hardened and updated.

| Purpose | Path |
|---|---|
| Caddy configuration | `/etc/caddy/Caddyfile` |
| Original configuration backup | `/etc/caddy/Caddyfile.before-coc-phase2` |
| Public portal page | `/srv/coc-portal/index.html` |
| Private asset registry | `/etc/coc/asset-registry.json` |

The registry is owned by `root:root` with mode `0640` and is not stored in the web root.

The Caddy configuration redirects HTTP to HTTPS, uses Caddy's internal authority for the private lab name, enables compression, removes the server identity header from portal responses, and sets content-security, anti-framing, MIME-sniffing, and referrer-policy headers.

Reusable sanitized examples are included under [`config/`](config/) and [`portal/`](portal/).

## Local HTTPS trust

The private lab hostname cannot receive a normal public certificate. Caddy therefore generated a local certificate authority.

The public root certificate was copied to the Windows workstation only after its SHA-256 certificate fingerprint matched on Ubuntu and Windows. It was added to the current user's trusted-root store. The private CA key never left the server.

The actual fingerprint is retained in the private operational record rather than the public repository.

## Asset-ID scheme

| Asset ID | Device class | Role | Status |
|---|---|---|---|
| `coc-srv-01` | Ubuntu server | Core lab host | Active |
| `coc-ws-01` | Windows workstation | Primary workstation | Active |
| `coc-lt-01` | Windows laptop | Mobile endpoint | Planned |

The public registry example contains no live addresses, serial numbers, MAC addresses, or private ownership details.

## Validation checklist

- [x] Ed25519 public-key login succeeds
- [x] Password-only SSH login is rejected
- [x] Root SSH login is disabled
- [x] SSH configuration syntax is valid
- [x] UFW is active and enabled
- [x] Default-deny incoming policy is active
- [x] Fresh SSH login succeeds through UFW
- [x] Fail2Ban service and SSH jail are active
- [x] AppArmor enforcement state is documented accurately
- [x] Auditd and kernel auditing are active
- [x] Automatic-update timers are active
- [x] No package updates remain pending
- [x] Caddy configuration is valid
- [x] HTTP redirects to HTTPS
- [x] HTTPS portal returns a successful response
- [x] Browser trusts the verified local authority
- [x] Asset registry JSON and permissions are valid
- [x] Sanitized public evidence is recorded

## Security considerations

- No password, SSH private key, token, live address, MAC address, serial number, or private CA key is committed.
- The asset registry is outside the public Caddy root.
- Local CA trust was limited to the current Windows user and verified before installation.
- The portal is designed for the trusted household network and must not be exposed publicly without a separate threat model, authentication layer, and external exposure test.
- Router port forwarding has not yet been independently validated and remains a required operational check.
- The server still depends on Wi-Fi and a DHCP address.
- AppArmor complain-mode profiles remain a documented visibility gap.

## Troubleshooting record

### UFW was absent

The minimized Ubuntu installation did not include UFW. It was installed before rules were configured or activated.

### UFW runtime and systemd state differed

`ufw status` showed active rules while `systemctl is-active ufw` initially returned inactive. Starting the enabled UFW service normalized both states, and a fresh SSH connection confirmed continued access.

### Caddy certificate test returned curl error 77

The normal administrative account could not traverse Caddy's protected data directory to read the CA certificate. Running the local verification with administrative read access succeeded without weakening the directory permissions.

### Windows denied hosts-file modification

The initial PowerShell window was not elevated. A verified administrator PowerShell session was used to add the local name mapping.

## Lessons learned

- Effective configuration output is stronger evidence than configuration text alone.
- SSH hardening requires configuration-order awareness on cloud-init-enabled Ubuntu systems.
- Access controls should be tested through both positive and intentional negative cases.
- Minimized installations require explicit package discovery rather than assumptions.
- AppArmor being loaded does not mean every profile or process is enforced.
- A private HTTPS service requires both name resolution and carefully verified trust distribution.
- A public web root and a private operational registry should remain separate.
- Service startup state and live firewall state should both be validated.

## Known limitations and deferred work

- Create a DHCP reservation for `coc-srv-01`.
- Confirm there are no router port-forwarding rules for administrative or portal ports.
- Review the Transmission AppArmor profiles before moving them from complain to enforce mode.
- Move infrastructure services to wired networking when practical.
- Enroll `coc-lt-01` and verify the local CA fingerprint again before trusting it.
- Phase 3 will introduce the container platform; the security services remain planned for Phase 4.

## Evidence

Sanitized command results and the public-release decision are recorded in [evidence/README.md](evidence/README.md).

## Outcome

Atlas now provides a patched, key-administered, default-deny Ubuntu baseline with layered SSH protection, mandatory-access-control visibility, kernel auditing, automated security updates, and a private HTTPS operations portal.

The verified platform is ready for **Phase 3 — Container Platform**.
