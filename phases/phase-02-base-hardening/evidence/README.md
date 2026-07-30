# Phase 2 — Sanitized Validation Evidence

**Validation date:** 2026-07-30  
**Asset ID:** `coc-srv-01`  
**Public-release status:** Approved after sanitization

## Evidence handling

This public record excludes passwords, private keys, certificate private keys, live addresses, machine identifiers, MAC addresses, serial numbers, router configuration, and uncropped desktop details.

Original terminal output and the browser screenshot were reviewed during implementation but remain outside the public repository. The sanitized results below preserve the technical conclusions.

## SSH authentication

Effective server settings:

```text
permitrootlogin no
pubkeyauthentication yes
passwordauthentication no
kbdinteractiveauthentication no
```

Positive test:

```text
HARDENED SSH KEY LOGIN SUCCESSFUL
```

Intentional negative test:

```text
Permission denied (publickey).
```

Result: **Pass** — key authentication succeeds while password-only access and root login are disabled.

## Firewall

Sanitized policy:

```text
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)

OpenSSH  ALLOW IN
80/tcp  ALLOW IN
443/tcp ALLOW IN
```

A fresh key-authenticated SSH connection succeeded after UFW activation and again after the systemd service state was normalized.

Result: **Pass** — the host applies a persistent default-deny inbound policy without interrupting approved administration.

## Fail2Ban

```text
Status for the jail: sshd
Currently failed: 0
Currently banned: 0
Journal matches: systemd SSH service
```

Effective policy:

```text
maxretry: 5
findtime: 600 seconds
bantime: 3600 seconds
```

Result: **Pass** — the SSH jail is active and consumes system-journal events.

## AppArmor

```text
apparmor module is loaded.
101 profiles are loaded.
8 profiles are in enforce mode.
4 profiles are in complain mode.
```

Result: **Pass with documented limitation** — AppArmor is active, but four Transmission profiles remain in complain mode pending application testing.

## Auditd

Sanitized status:

```text
enabled 1
failure 1
rate_limit 0
backlog_limit 8192
lost 0
backlog 0
```

Result: **Pass** — kernel auditing is enabled and reported no lost events.

## Automatic updates and patch state

```text
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
```

Both apt timers were scheduled. After the controlled upgrade:

```text
Listing... Done
No reboot required
```

Result: **Pass** — automatic updates are enabled and no package updates remained pending.

## Caddy and portal

```text
Caddy version: v2.11.4
Service enabled: yes
Service active: yes
Configuration: Valid configuration
HTTP result: 308 Permanent Redirect
HTTPS result: 200
```

Verified HTTPS response controls:

```text
Content-Security-Policy: configured
Referrer-Policy: no-referrer
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
```

The browser opened the private portal without a certificate warning after the local CA fingerprint was verified and trusted.

Result: **Pass** — the private portal is available through trusted HTTPS with the intended response controls.

## Asset registry

```text
JSON validation: valid
Owner: root
Group: root
Mode: 0640
Location: outside the public web root
```

Result: **Pass** — the operational registry is valid and not anonymously downloadable from the portal.

## Listening services

Sanitized final result:

```text
TCP 22  OpenSSH
TCP 80  Caddy redirect
TCP 443 Caddy HTTPS
UDP 443 Caddy HTTP/3 listener
```

UFW does not currently permit UDP 443.

## Overall result

| Control | Result |
|---|---|
| SSH key authentication | Pass |
| Password-only SSH rejection | Pass |
| Root SSH login disabled | Pass |
| Default-deny firewall | Pass |
| SSH access through firewall | Pass |
| Fail2Ban SSH jail | Pass |
| AppArmor | Pass with documented limitation |
| Auditd | Pass |
| Automatic security updates | Pass |
| Current package state | Pass |
| Caddy validation | Pass |
| HTTP-to-HTTPS redirect | Pass |
| Trusted HTTPS portal | Pass |
| Asset-registry protection | Pass |
| Public evidence sanitization | Pass |

**Overall result: PASS — Phase 2 completion criteria satisfied, with documented operational follow-ups.**
