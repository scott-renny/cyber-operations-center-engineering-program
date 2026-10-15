# COC USB #2 — DFIR field toolkit

Supporting personal-lab engineering asset, separate from COC phase completion. Release 0.10.1 was installed by an owner-run identity-guarded updater and the latest 35 changed files were read-back verified. Post-update free space: 18.58 GiB. The staged suite passed 128 local Python tests; synthetic case integration, controlled guided decisions and retention failure paths were checked.

The toolkit provides guided acquired-evidence workflows, artifact/email/network/static-analysis review, case logging/reporting, harmless practice, handoff records, offline readiness/freshness reporting and explicitly chosen generated-log retention. USB #1 remains the repair/support toolkit. No other USB role is reassigned.

Integration boundary: this release does not deploy COC server services, configure central monitoring, enroll endpoints, upload evidence, carry live COC credentials or run unattended containment/remediation. The central program's phase statuses are unchanged. Authority, master evidence, protected storage, retention decisions and actual custody identity remain operator responsibilities.

Read-back/hash and synthetic test results do not establish universal forensic validity or operational readiness. Real-evidence, full live-query, GUI, acquisition and separate offline-lab acceptance remain distinct; boot testing was excluded by the owner. Known tool limitations remain in the public readiness catalog.

Source edition: https://github.com/scott-renny/coc-usb-dfir-toolkit

Case study: https://scott-renny.github.io/projects/coc-usb2-dfir-toolkit.html

Journal: https://scott-renny.github.io/journal/building-a-dfir-workflow-on-a-usb.html

See [Evidence handling](EVIDENCE-HANDLING-STANDARD.md), [Data governance](DATA-GOVERNANCE.md), [Change management](CHANGE-MANAGEMENT-STANDARD.md) and [Portfolio policy](PORTFOLIO-POLICY.md). The public source excludes vendor/boot/VM/container payloads, device identifiers, private evidence and original transcripts.
