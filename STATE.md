# STATE.md — current state

> Rewritten, not appended, as the LAST act of every session. Holds only what's
> current — in flight, blocked, and what a fresh session needs before touching
> anything. History moves to `HISTORY.md`.

## In flight

**v1.0.0 published: DigitalOcean's own real, first-ever schema snapshot
(UBI-216), 59 resources + 137 data sources.** Generated from a manually
bundled copy of DigitalOcean's real, public OpenAPI 3.0 spec (github.com/
digitalocean/openapi) -- the raw upstream document does not load through
`ubx-provider-dynamic`'s own loader as published (two Redocly-only,
non-standard `$ref` conventions, tracked as UBI-217). No `hash-watch.yml`
exists yet for exactly this reason -- adding one that points at the raw
URL would fail every scheduled run. See `CLAUDE.md`'s own note.

## Blocked / needs a decision

**Regenerating this snapshot from a fresh upstream fetch requires the
same manual bundling step until UBI-217 lands.** Not a blocker for
`v1.0.0` itself (already published), but real, load-bearing for any
future drift regeneration -- whoever picks this up next should check
UBI-217's status first.
