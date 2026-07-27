# Secrets, Certificates, and Key Management Standard

**Owner:** COC Program Owner
**Review cadence:** Quarterly; immediately after suspected exposure

## Scope

Passwords, passphrases, API tokens, OAuth secrets, SSH keys, WireGuard keys, TLS private keys, recovery codes, encryption keys, service-account credentials, database credentials, webhook secrets, and backup keys.

## Mandatory standards

- Store human-managed passwords and recovery information in Vaultwarden or an approved successor.
- Never commit secrets to Git, documentation, screenshots, issues, chat exports, or container images.
- Use `.env` or Docker secrets for local service configuration; permissions must be owner-only where supported (`0600` for secret files).
- Commit only `.env.example` files containing placeholders.
- Use unique credentials per service and environment.
- Prefer scoped, least-privilege, expiring tokens over shared administrator credentials.
- Use dedicated service accounts for integrations.
- Protect secrets in transit through approved encrypted channels.
- Do not place private keys on systems that do not require them.

## Key standards

### SSH

Use modern key types supported by the target, protect private keys with passphrases where operationally practical, restrict authorized keys, and remove superseded keys after validation.

### WireGuard

Generate private keys on the endpoint that will use them where practical. Store public keys in configuration management; treat private keys as Restricted. Rotate after device loss, suspected exposure, role change, or scheduled review.

### TLS

Caddy-managed automatic HTTPS is preferred where appropriate. Private keys are never copied into the public repository. Expiration monitoring and renewal validation are mandatory for manually managed certificates.

### API and automation tokens

Tokens must be scoped to required endpoints/actions, stored outside source code, masked in logs, and rotated after exposure or material workflow changes. Unsafe automation must support manual override.

## Rotation

| Secret type | Routine review | Rotate immediately when |
|---|---|---|
| Privileged passwords | Quarterly | Exposure, compromise, shared use, device loss |
| API/service tokens | Quarterly | Exposure, integration change, excessive privilege |
| SSH/WireGuard keys | At least annually | Device loss, exposure, unauthorized access |
| TLS certificates | Automated/expiry monitored | Private-key compromise or trust failure |
| Recovery codes | After use and annual review | Any code is exposed or consumed |
| Backup encryption keys | Annual access review | Exposure or repository compromise |

Rotation is not complete until the replacement works, dependent services are validated, the old credential is revoked, caches/sessions are invalidated where applicable, and the rotation record is closed.

## Logging and redaction

Secret values must not be logged. Logs may contain secret IDs, last four characters, owner, creation date, expiry, and rotation status when needed. Screenshots and reports must redact values, QR codes, cookies, authorization headers, session identifiers, and recovery codes.

## Emergency recovery

- Maintain an offline, protected recovery record for Vaultwarden access and critical encryption recovery.
- Store emergency material separately from the systems it recovers.
- Define a trusted household recovery contact where appropriate without granting routine access.
- Test recovery instructions at least annually without exposing live secrets.
- If the Vaultwarden master password and recovery material are lost, encrypted vault contents may be unrecoverable. The response is controlled credential reset/rotation across affected systems—not an attempt to bypass encryption.

## Exposure response

Open a security case, determine scope, revoke or disable the credential, issue a replacement, search logs for use, validate dependent services, update affected devices, preserve evidence, and record lessons learned.
