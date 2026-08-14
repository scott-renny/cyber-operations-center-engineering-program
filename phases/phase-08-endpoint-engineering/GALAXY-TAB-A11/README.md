# Galaxy Tab A11 Endpoint Baseline

> **Status:** Complete with documented NFC boundary  
> **Completion date:** 2026-08-13  
> **Evidence:** Operator-validated; raw screenshots retained privately

## Purpose

Maintain a hardened Android and Samsung baseline for the tablet and reconnect it safely to the rebuilt security stack.

## Validated baseline

- Current Samsung system and Google Play system updates
- Secure device credential and immediate power-key locking
- Biometric settings reviewed where supported
- Samsung platform-security status reviewed
- Developer options unnecessary or disabled; USB debugging and OEM unlocking off
- Auto Blocker enabled
- Find-device and remote-recovery capability reviewed
- Play Protect scan completed
- Camera, microphone, location, and special application access reviewed
- Unknown-app installation restricted
- Advertising and personalization settings reduced
- Sensitive local data and application access reviewed
- Protected DNS and VPN behavior reviewed for trusted and untrusted use

## Device-specific boundary

The tablet does not inherit phone-only theft-detection claims. Find-device and remote-recovery controls are the documented compensating capability. NFC availability varies by model and region; this record does not assert that NFC hardware exists or that an NFC security key is enrolled.

## Connectivity model

The tablet uses a unique WireGuard peer identity when private remote access is required. Keys and tunnel configuration remain outside the repository.

See [validation](01-validation.md).
