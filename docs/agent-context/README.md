# Forkbase — agent context

**Forkbase** is a fork of [superset-sh/superset](https://github.com/superset-sh/superset) — the open-source (Elastic License 2.0) agentic IDE that orchestrates 100+ coding agents — taken in its own direction:

> **The Linux-first, free-mobile Superset.**

## Pillars

| # | Pillar | What it means |
|---|--------|---------------|
| 1 | Rebrand | One scripted, rebasable white-label patch (names, icons, bundle IDs, update feed, telemetry) |
| 2 | First-class Linux desktop | Packaging (AUR/Flatpak/deb), Wayland/Hyprland polish, replace macOS-only packages (e.g. `macos-process-metrics`), tray/notifications/deep links/auto-update. The author daily-drives Arch (Omarchy) — dogfooding is the spec |
| 3 | Free Android app | Enable Android on the in-repo Expo/React Native `apps/mobile` (upstream ships iOS-only, Pro-gated) |
| 4 | Self-hosted cloud | Run `api`/`gate`/`relay`/`realtime`/`review-host`/`usercontent` yourself — no Pro gate, your own accounts |

## Status

Direction confirmed (2026-10-14): pillars · milestone order (**Linux-first dogfood after M1**, D9) · beta bar. Phase 0 started — fork created + cloned (2 of 6 steps); dev-stack boot pending. Details in [STATUS.md](STATUS.md).

## Map

- [STATUS.md](STATUS.md) — current state, next step, append-only checkpoint ledger
- [ARCHITECTURE.html](ARCHITECTURE.html) — visual architecture: system context, monorepo map, mobile chain, fork model, license layer
- [SYSTEM_DESIGN.html](SYSTEM_DESIGN.html) — visual system design: sign-offs, pillars, D1–D9, milestone roadmap, risks, beta bar
- [plans/0001-forkbase-build-plan.md](plans/0001-forkbase-build-plan.md) — the phased build plan (main document)
- [decisions/0001-foundation.md](decisions/0001-foundation.md) — D1–D9 with alternatives and rationale
- [research/2026-10-14-superset-recon.md](research/2026-10-14-superset-recon.md) — recon evidence, verified vs inferred
- [KNOWN-GAPS.md](KNOWN-GAPS.md) — open questions Phase 1 must clear

## Resume point for a cold agent

1. Read [STATUS.md](STATUS.md).
2. Execute the next unchecked step in the [build plan](plans/0001-forkbase-build-plan.md).
3. Respect the [decision log](decisions/0001-foundation.md) — changing a decision requires a new decision record superseding it, not a silent override.

## Where this lives

This `docs/agent-context/` is inside the fork itself — [github.com/mrvigneshvt/forkbase](https://github.com/mrvigneshvt/forkbase) — and travels with the code. Local clone: `~/Workspace/Projects/personal/forkbase` (remotes: `origin` = fork, `upstream` = superset-sh/superset). The original planning worktree (`~/.superset/worktrees/forkbase/nebula-earthworm-c986f9aa`) was emptied after consolidation on 2026-10-14.