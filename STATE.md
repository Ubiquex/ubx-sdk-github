# STATE.md — current state

> Rewritten, not appended, as the LAST act of every session. See `HISTORY.md`
> for the narrative.

## In flight

**Two real, open items (UBI-249), neither a blocker, both worth
picking up:**

1. **The `github_build` category fix (`Repositories`, merged to `main`)
   is NOT in any published release yet.** The `v1.2.2` git tag points
   to `42876ca`, before the fix; the fix landed afterward as a separate
   commit. `ubx-docs-providers`' own `fetch-docs.mjs` downloads the
   tagged release artifact, not live `main`, so the docs site (once
   actually deployed) will keep showing `data_github_build` as
   Uncategorized until a new version is cut and published with the fix
   included. Needs a version bump (1.2.3) and a real `publish.yml`
   dispatch.
2. **84 wire types are uncategorized, unrelated to `github_build`.**
   `1.2.1` was 340/340 categorized (zero gaps). `1.2.2` (404 wire
   types, +64 from earlier UBI-250/coverage-gap work this same arc,
   only one of which is `github_build`) sits at 320/404 after this
   arc's own category fix. Not investigated further -- a real,
   separate `write-artifacts`-shaped gap, category authoring needed for
   whatever service tokens these 84 wire types belong to.

## Blocked

Nothing blocked. Zero open PRs.

## Current state

**`translator-watch.yml` is now live (UBI-249).** This repo's own
`hash-watch.yml` already auto-regenerates and correctly commits
`PROVENANCE.json` on real spec drift; `translator-watch.yml` adds the
other, independent trigger (a translator-tag move) that path never
covered -- regenerates holding the schema fixed at this repo's own
pinned version, self-heals (`PROVENANCE.json` only) on an empty diff,
opens a real review PR on a genuine one. Never auto-merges.

**`.gitignore` was fixed this arc: a bare, unanchored `build/` line
(meant for Python's own build-artifact directory) also matched
`sdk/go/github/data/build/`, a real generated package for the
`github_build` data source -- silently excluded from every commit
since this repo's creation.** Anchored to `sdk/python/build/` and
`sdk/python/dist/` now. `data_github_build` shipped for the first time
in `1.2.2` as a direct result -- verified published and importable in
all three languages (npm `1.2.2`, PyPI `1.2.2`, Go proxy `v1.2.2` at
the real module path `github.com/ubiquex/ubx-sdk-github/sdk/go`, not
the repo root). Its intro and field descriptions were already authored
and already counted in coverage from before it shipped.

This repo's own `--descriptions-dir` fix (a session-wide gap: every
hand regeneration had omitted the flag) and `PROVENANCE.json` bootstrap
(this repo never had one before) both merged this same arc.

`VERSION` at repo root: fetched 2026-08-24 from GitHub's own live GHEC
OpenAPI description -- not re-checked this arc.

## Before touching anything

- Never self-merge here. See `CLAUDE.md`.
- Never hand-edit generated bindings — fix the generator or the upstream
  schema, then regenerate.
