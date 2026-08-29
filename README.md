# ubx-schema-digitalocean

A real, frozen, versioned DigitalOcean provider schema snapshot -- the pinnable
distribution artifact `ubx-provider-dynamic` and `ubiquex` resolve a
single `[providers.digitalocean]` entry against, with zero network calls at
schema resolution time (see `provider/acquireschema.go` in `ubiquex`, and
`internal/snapshot`'s own doc comment in `ubx-provider-dynamic`). The
resource/data-source split below is a real, internal discovery-time
detail -- one pin resolves both.

## What's here

DigitalOcean's own real published identity is a GROUP of two members, both
fetched from the identical real, public OpenAPI 3.0 spec
(github.com/digitalocean/openapi) but built through genuinely different
pipelines:

- `digitalocean` -- resource mode (59 real resource types, raw `Discover()`
  found 61; the full pipeline's own collision/unusable-field filtering
  trims the count slightly, as it does for every real provider).
- `digitalocean_ds` -- data-source mode (137 real, unclaimed read-only
  operations).

- `manifest.json` -- the group's own real identity: `schema_format`,
  `provider`, one `version` for the WHOLE group, and which member names
  it bundles.
- `members/<name>.json` -- one real, complete, independently-diffable
  file per member (`digitalocean.json`, `digitalocean_ds.json`). Committed
  as separate files, not one combined blob, so a real version bump's own
  git diff shows exactly which members changed.
- `.github/workflows/publish.yml` -- manual-dispatch-only. Packs
  `manifest.json` and every `members/*.json` into one compressed archive
  (`snapshot.tar.gz`) and cuts a real GitHub Release tagged `v<version>`
  carrying exactly two assets: `snapshot.tar.gz` and `SHA256SUMS`.

**No `hash-watch.yml` yet** -- see `CLAUDE.md`'s own real, named gap
(UBI-217): DigitalOcean's real spec does not load through
`ubx-provider-dynamic`'s loader as published, only after a manual
Redocly bundle. A scheduled job pointed at the raw upstream URL would
fail every run. `v1.0.0` was generated from a manually bundled copy,
by hand, this session -- real and correct, not automated yet.

## Consuming a real, published version

In `ubiquex`, one real pin resolves the whole group -- both real members
(`digitalocean` resource mode, `digitalocean_ds` data-source mode) are
served together from the SAME launch, the SAME real download:

```toml
[providers.digitalocean]
source  = "ubiquex/digitalocean"
version = "1.0.0"
```

`provider.AcquireSchema`'s own cache-by-source+version resolves ONE real
download and ONE extracted cache directory
(`~/.ubx/schemas/ubiquex/digitalocean/1.0.0/`) -- the launched process merges
every real member of the group (`internal/snapshot.MergeOpenAPIGroup`)
into one served schema, `ResourceSchemas` and `DataSourceSchemas`
together, exactly like a real, hand-written Terraform provider already
looks from the outside.

## Versioning

One real, mechanically-derived semver number for the WHOLE group, not
one per member: the highest real change level found across every
member (a brand new resource type or a field that gained write access
bumps MINOR; a resource type or field that disappeared, or a field that
lost write access, bumps MAJOR; a pure description-text change bumps
PATCH), plus an unconditional MAJOR if a member the group used to bundle
is gone entirely. See `internal/snapshot/diff.go` and `AssembleGroup` in
`ubx-provider-dynamic` for the real rule.

`v1.0.0` is this group's real, first-ever snapshot.

## Links

- Docs: https://docs.ubiquex.io
- Internals (architecture and design): https://github.com/Ubiquex/ubiquex-internals
- Linear board: https://linear.app/ubiquex
