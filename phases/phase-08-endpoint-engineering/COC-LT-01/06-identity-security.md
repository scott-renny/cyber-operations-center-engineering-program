# COC-LT-01 Identity Security

## Completed in Phase 8

| Service | Hardware-key state | Validation |
|---|---|---|
| Microsoft account | Hyper FIDO Pro Mini enrolled | Private-session sign-in required the hardware key and succeeded |
| Bitwarden | Hyper FIDO Pro Mini enrolled | Enrollment completed |

The Microsoft passkey was named **COC-LT-01 Hyper FIDO Pro**. Existing passwords and recovery methods were retained during enrollment to prevent lockout.

## Security-key strategy

A workstation-associated key supports phishing-resistant authentication without making routine use of one workstation dependent on another workstation's key. High-value accounts may ultimately register more than one approved key for resilience.

The public inventory records assignment and enrollment status only. It must never contain key PINs, recovery codes, account identifiers, or credential material.

## Deferred work

The following items were discussed but not completed and are not part of the Phase 8 completion claim:

- GitHub enrollment
- Google enrollment
- AWS enrollment
- Amazon enrollment
- TrustKey T110 enrollment as a secondary or other-workstation key
- FIDO2-backed SSH authentication
- Git commit signing

## Recovery rule

Keep existing recovery factors and securely stored recovery codes until at least two approved authentication paths have been enrolled and independently tested. Loss or suspected compromise of a key requires account review, credential revocation, inventory update, and replacement-key enrollment.
