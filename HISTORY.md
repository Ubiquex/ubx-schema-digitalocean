# HISTORY.md — narrative archive

Consulted only when a session needs to know why a decision was made — not
read on every open.

## 2026-08-30 — repo created, v1.0.0 published (UBI-216)

DigitalOcean onboarded as the proving case for the `ubx-provider-runbook`
onboarding runbook. Step one (confirming a real, public, machine-readable
spec exists and adding a live `[dynamic_providers.digitalocean]` entry to
`ubiquex`'s own `sdk/providers/.ubx/config`) found the spec does not load
through `ubx-provider-dynamic`'s own OpenAPI loader as published — two
Redocly-only, non-standard `$ref` conventions kin-openapi does not
resolve. Filed as UBI-217.

`v1.0.0` generated from a manually bundled copy of the real, current
upstream spec (`npx @redocly/cli bundle`), the same real workaround used
to compute step one's own resource/field counts. 59 real resource types,
137 real data-source types. `ubiquex`'s own config switched from the live
entry to this pin in the same body of work.
