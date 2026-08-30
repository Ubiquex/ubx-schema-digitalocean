# STATE.md — current state

> Rewritten, not appended, as the LAST act of every session. Holds only what's
> current — in flight, blocked, and what a fresh session needs before touching
> anything. History moves to `HISTORY.md`.

## In flight

**Not yet published, despite manifest.json/members/ already committed locally.**
`v1.0.0` (59 resources + 137 data sources) has never actually reached this
repo's own `main` on GitHub -- the very first push attempt (commit 710bb52)
was rejected outright by GitHub's own secret-scanning push protection, and
no push has succeeded since. A prior session's own `STATE.md`/`HISTORY.md`
said "published" without that push ever having landed; corrected here
rather than repeated.

**The push protection finding is a real, confirmed false positive, not a
live secret.** GitHub flagged a Slack Incoming Webhook URL pattern at two
locations each in `members/digitalocean.json` and `members/digitalocean_ds.json`.
Read directly: both are real, verbatim documentation example values copied
from DigitalOcean's own public API spec (`https://hooks.slack.com/services/
T1234567/AAAAAAAA/ZZZZZZ` and `.../T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX`
-- textbook placeholder tokens, not a real credential). Fix is to allow this
specific finding via GitHub's own secret-scanning UI (the unblock link the
push itself prints), not to scrub legitimate spec content -- these are real
DigitalOcean API documentation examples, part of what UBI-217's own
"the DigitalOcean and Linode specs are real and correct" already
established. This requires repo-admin action on github.com, not something
a session should do unilaterally.

**UBI-217 has landed in `ubx-provider-dynamic`** (PRs open, not yet merged):
a new per-provider `redocly_bundle` config flag shells out to
`npx @redocly/cli bundle` before `Load` ever sees the bytes, replacing the
ad-hoc manual bundling step `v1.0.0`'s own content was originally generated
from. Verified directly: regenerating via the new, official
`--generate-snapshot-group` mechanism (`redocly_bundle = true` in the
generation config) produces byte-identical `manifest.json`/`members/*.json`
content to what's already committed here -- the manual workaround was
correct, and is now reproducible through the real, supported path instead
of a one-off.

## Blocked / needs a decision

**The push is blocked on a founder-only action**: visit the unblock URL
GitHub's own push protection printed (a real, specific alert ID, not a
guessable one -- re-run `git push` from this checkout to get a fresh one if
needed) and allow the finding, since it is a documentation example, not a
live secret. Once unblocked: push, cut the real `v1.0.0` GitHub Release
(`publish.yml`), and switch `ubiquex`'s own `sdk/providers/.ubx/config`
`[dynamic_providers.digitalocean]` entry from live (already carrying
`redocly_bundle = true`) to a real `source`/`version` pin, matching the
other six real providers.

**`hash-watch.yml` is added, but not yet operational**: it needs whichever
`ubx-provider-dynamic` release first ships the `redocly_bundle` flag
(latest published today is `v1.0.2`, which does not have it -- PRs open,
not yet merged). A run against an older release would silently ignore
`redocly_bundle = true` (BurntSushi/toml's own default unknown-field
behavior) and fail generation the same way it did before UBI-217, not
silently succeed.
