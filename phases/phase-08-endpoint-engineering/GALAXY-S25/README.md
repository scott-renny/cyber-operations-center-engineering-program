# Galaxy S25 Endpoint Baseline

> **Status:** Complete with deferred identity-key follow-up  
> **Completion date:** 2026-08-13  
> **Evidence:** Operator-validated; raw screenshots retained privately

## Purpose

Maintain a hardened Android and Samsung Knox baseline for the primary mobile phone and reconnect it safely to the rebuilt security stack.

## Validated baseline

- Current Samsung system and Google Play system updates
- Secure device credential and immediate power-key locking
- Biometric convenience backed by the device credential
- Samsung Knox platform status reviewed
- Developer options unnecessary or disabled; USB debugging and OEM unlocking off
- Auto Blocker enabled
- Theft and recovery controls enabled where supported
- Find-device and last-location capability reviewed
- Play Protect scan completed
- Camera, microphone, location, and special application access reviewed
- Unknown-app installation restricted
- Advertising and personalization settings reduced
- Sensitive application placement and local-data exposure reviewed
- Protected DNS and VPN behavior reviewed for trusted and untrusted use

## Connectivity model

The phone uses its own WireGuard peer identity when remote access to private services is required. DNS behavior is validated through the approved filtering path. Keys and tunnel configuration are not stored here.

## Deferred work

NFC security-key registration and the account-by-account FIDO2 inventory are intentionally deferred. Phase 8 does not claim every account is enrolled or that recovery factors were redesigned.

See [validation](01-validation.md).
