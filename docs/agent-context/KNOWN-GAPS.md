# KNOWN-GAPS

Live list of acknowledged unknowns and deliberate exclusions. Remove each entry when resolved, noting where it was resolved.

| # | Gap / exclusion | Why it exists | What clears it |
|---|---|---|---|
| 1 | Pro-gate location unknown | Only names/structure seen (`apps/gate`, `packages/auth`, `cloud-client`); no source read yet. Fork HEAD is a billing commit — the gate is actively worked upstream | Phase 1a deep-dive |
| 2 | Phone→desktop wiring unknown | Remote-chain roles inferred from directory names | Phase 1b deep-dive |
| 3 | Android blocker inventory unknown | No `expo run:android` run yet; iOS-oriented patch tests seen in `apps/mobile` | Phase 1d triage |
| 4 | Self-host auth difficulty unknown | Mobile's coupling to upstream cloud accounts is unverified | Phase 1a/1b |
| 5 | Linux pain log empty | Pillar-2 spec comes from dogfooding; not started | Author logs daily AppImage pain; Phase 1c consolidates |
| 6 | Upstream's appetite for Linux PRs unverified | No issue/PR survey done | Phase 0/1 (survey open Linux issues/PRs) |
| 7 | Upstream test layout unverified | `bun test` setup not inspected | Phase 0 (affects TDD mechanics) |
| 8 | Windows deliberately out of scope | Author selected Linux as the direction gap | New decision record if that changes |

## Resolved

- 2026-10-14 — old gap "Fork GitHub owner/location unknown": fork created at [github.com/mrvigneshvt/forkbase](https://github.com/mrvigneshvt/forkbase), cloned to `~/Workspace/forkbase`. Recorded in STATUS ledger (2).

## Deliberate exclusions (decisions, not gaps)

- REA binary analysis deferred: only if the source leaves gaps (decision [D8](decisions/0001-foundation.md)).
- No monetization design in beta scope (license constraints in [D6](decisions/0001-foundation.md)).
- No local.db content inspection in planning (paths listed only; `auth-token.enc` untouched).