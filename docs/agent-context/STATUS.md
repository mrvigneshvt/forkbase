# STATUS

## Current state

- 2026-10-14: Direction confirmed (all three sign-offs: pillars, milestone order, beta bar). Fork created and cloned; all planning docs + `ARCHITECTURE.html` + `SYSTEM_DESIGN.html` consolidated into this directory. Phase 0 started — 2 of 6 steps done.
- Local clone: `~/Workspace/forkbase` · remotes: `origin` = mrvigneshvt/forkbase, `upstream` = superset-sh/superset.
- Fork HEAD at consolidation: `cc31d024c` — note: upstream's billing work is active (`feat: move billing to Autumn…`), relevant intel for the Phase 1a gate hunt.

## Next step

**Phase 0 — Baseline** (from the [build plan](plans/0001-forkbase-build-plan.md)), remaining steps:

- Verify prereqs on Arch: `bun` (version pinned in upstream `.bun-version`), `docker`, `jq`, `gh`.
- Run `./.superset/setup.local.sh` (brings up Postgres + neon-proxy + Redis via Docker, seeds the dev account), then `bun run dev`.
- Docs sweep: `https://docs.superset.sh/llms-full.txt`, `DEVELOPMENT.md`, `CONTRIBUTING.md`.
- Rebrand inventory: enumerate every hardcoded Superset reference (names, bundle IDs, update feed, telemetry/crash reporting).
- Also read upstream's `docs/linux-desktop-acceptance.md` — upstream already has Linux acceptance work in the tree (M2 intel).

Exit criteria: the forkbase dev app boots from source on Linux alongside the installed AppImage.

Also pending from the author: the **Linux pain log** — one line per annoyance in today's AppImage. It is the M2 spec.

## Checkpoint ledger (append-only, newest last)

- **2026-10-14 (1)** — Recon + planning session. Direction locked: fork & rebrand → Linux-first + free Android + self-hosted cloud; Bun + TS. Agent-context docs written.
- **2026-10-14 (2)** — Fork created: [github.com/mrvigneshvt/forkbase](https://github.com/mrvigneshvt/forkbase) (clears old fork-location gap). Cloned to `~/Workspace/forkbase` with `upstream` remote. Milestone order confirmed: **Linux-first dogfood after M1** (recorded as D9). Planning docs + both HTMLs moved from the planning worktree and `~/.opencode/plan` into this directory; worktree emptied. Package count corrected (25 → 26). Next: Phase 0 remaining steps.