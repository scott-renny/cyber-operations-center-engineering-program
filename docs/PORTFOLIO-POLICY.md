# Public Portfolio and Sanitization Policy

## Purpose

Enable credible public evidence without exposing household privacy, secrets, infrastructure, or unsafe operational detail.

## Publication classes

- **Public:** policy, sanitized architecture, synthetic logs, generalized lessons, approved screenshots.
- **Public after sanitization:** configuration excerpts, case studies, dashboards, inventories, detection results.
- **Private:** raw logs, run-time inventories, internal diagrams, household activity, backups, case records.
- **Never publish:** passwords, tokens, keys, cookies, recovery codes, personal communications, forensic images, live exploit credentials, or information that enables unauthorized access.

## Release checklist

Confirm ownership/licensing; remove secrets and personal data; replace infrastructure identifiers; remove metadata; crop unrelated UI; verify no real attack target or third-party data; preserve an internal original; inspect final export at full resolution; record release date and destination.

## Responsible presentation

Campaign content must state that testing was authorized and lab-scoped. Do not provide evidence that implies activity against third parties. Findings must distinguish planned architecture from validated implementation. AI-assisted drafting may be disclosed when appropriate, but the operator remains responsible for accuracy, testing, and sanitization.
