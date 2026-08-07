# COC-LT-01 WireGuard

## Objective

Provide authenticated, encrypted access to COC services while applying a stricter traffic policy when COC-LT-01 is outside the trusted home network.

## Implemented profiles

| Profile | Intended use | Routing | DNS | Kill switch |
|---|---|---|---|---|
| Home | Trusted home network | Split tunnel to approved COC networks | Approved resolver | Not required by the recorded design |
| Untrusted | Public or otherwise untrusted network | Full tunnel | Approved DNS through the tunnel | Enabled |

No private keys, live endpoints, addresses, or resolver details are stored in this public record.

## Architecture

```text
Trusted network:
COC-LT-01 -> normal Internet path
          -> WireGuard for approved COC destinations

Untrusted network:
COC-LT-01 -> WireGuard full tunnel -> approved egress and DNS
          X direct fallback when the tunnel is unavailable
```

## Completed validation

- WireGuard peer status was reviewed with `wg show` on the VPN endpoint.
- The split-tunnel profile reached approved internal resources.
- The full-tunnel profile routed Internet traffic through the VPN.
- DNS resolution succeeded under the intended profile.
- The untrusted profile prevented unintended direct traffic when the tunnel was unavailable.
- Administrative services remained reachable through the approved VPN path.

## Failure handling

If the untrusted profile cannot establish a tunnel, preserve the kill switch, move to a trusted network if practical, and troubleshoot endpoint reachability, time, DNS, and peer status. Do not publish configuration files or diagnostic output containing keys or live addresses.
