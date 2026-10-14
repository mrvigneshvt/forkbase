# Decision 0001 — Forkbase foundation

Date: 2026-10-14 · Status: accepted · Session: forkbase planning (worktree `nebula-earthworm-c986f9aa`)

Evidence base: [research/2026-10-14-superset-recon.md](../research/2026-10-14-superset-recon.md). Each decision lists the alternatives weighed. Changing any of these requires a new decision record superseding this one — never a silent override.

---

## D1 — Fork & rebrand, not clean-room or hybrid core

**Context.** Superset's entire product — desktop app, the in-repo Expo mobile client, and the remote-access cloud stack (`api`, `gate`, `relay`, `realtime`, `review-host`, `usercontent`) — is open under Elastic License 2.0. Classic binary reverse engineering is unnecessary.

**Options weighed.**
1. Fork & rebrand — take everything, rename, diverge. *(chosen)*
2. Hybrid — own minimal core borrowing architecture patterns, not code.
3. Clean-room — study behavior only, reimplement everything.

**Decision.** Fork & rebrand. Author quote: *"I am planning to fork it and then I am going to take it on my own direction with whatever they have currently."*

**Rationale.** Maximum velocity; the differentiators (Linux, Android, self-host) are additive, not architectural; the reverse-engineering effort a clean-room demands buys nothing the license doesn't already grant.

**Consequences.** Inherited code stays ELv2 forever (D6); upstream maintenance becomes a standing cost (D7); the beta can be published immediately since the license already permits forking and self-hosting.

---

## D2 — Stack: Bun + TypeScript (upstream's own)

**Options weighed.** Bun + TS *(chosen)* · Go (static binary, strong CLI story) · Rust (perf/safety, slower iteration).

**Rationale.** Same stack as upstream means every studied pattern maps 1:1, monorepo tooling (turbo, biome, lingui, bun workspaces) is reused, and fork diffs stay minimal.

---

## D3 — Direction pillar: first-class Linux desktop

**Context.** Upstream: macOS is the primary target; Linux ships as an "experimental" x64 AppImage; Windows doesn't exist. The author daily-drives Arch Linux (Omarchy, Hyprland) on the experimental AppImage.

**Options weighed** (author-selected from gap list): first-class Linux *(chosen)* · Windows support · deep review-on-the-go · radical self-host/privacy.

**Decision.** Linux-first is forkbase's differentiating direction.

**Rationale.** The author is the target user (dogfooding = spec); upstream's `packages/macos-process-metrics` proves macOS-only assumptions exist in the tree; Linux packaging (AUR/Flatpak/deb) and Wayland/tiling-WM polish are needs upstream shows no priority for.

**Consequences.** Phase 1 includes a Linux audit track; generic fixes go upstream where acceptable (D7); the author's daily pain log becomes the pillar-2 spec.

---

## D4 — Free Android app via the in-repo Expo client

**Context.** `apps/mobile` is Expo/React Native (expo-router, EAS, config-plugins) — cross-platform by construction. Upstream's mobile is iOS-only and Pro-gated ("Mobile requires Superset Pro, iOS 26 or later" — upstream README).

**Decision.** Enable Android on `apps/mobile` and ship it free.

**Rationale.** The gap is distribution, not architecture: both the client and its cloud stack are open. Android enablement is porting work (patches, native modules, push, certs) — not a rewrite.

**Consequences.** Android is part of the beta definition; a phone ↔ self-hosted-cloud E2E test is a build slice.

---

## D5 — Self-hosted cloud replaces the Pro cloud

**Context.** The remote-access stack (`api`/`gate`/`relay`/`realtime`/`review-host`/`usercontent`) is in the open repo; the Pro gate is expected to be upstream's hosted account/billing system, not closed client code (location unverified — Phase 1a).

**Decision.** Forkbase ships a self-hostable cloud side (Docker), removing the Pro gate for mobile/remote access; the beta is open.

**Consequences.** Auth/self-hosting is the hardest new engineering (mobile's coupling to upstream cloud accounts is unverified); the deployment story is a Phase 3 design-doc deliverable.

---

## D6 — License stance

**Decision.**
- Inherited code: stays **Elastic License 2.0**. It cannot be relicensed. Upstream README: "use it, fork it, modify it, self-host it for your team. The only thing off the table is repackaging Superset itself as a service you sell to others."
- Forkbase's new code (Android additions, new packages): author's choice of license, added on top.
- Beta is published (open, source-available); free Android distribution is unaffected.

**Consequences.** Not OSI-open as a whole; if forkbase ever monetizes, selling the repackaged fork as a hosted service is prohibited — own additions can be monetized freely.

---

## D7 — Fork discipline (how "own direction" survives upstream's velocity)

Upstream ships daily (~500 open PRs at recon time). Binding rules:

1. **Seams, not edits** — forkbase features live in new packages/apps (`packages/forkbase-*`) and upstream's plugin mechanisms; never inline-edit upstream files where a config seam works.
2. **White-label as one scripted patch** — rebrand necessarily touches upstream files; keep it a single rebasable patch script, never scattered edits.
3. **Conscious hard-fork moment** — track upstream until the beta is stable, then pick a divergence commit and own it (cherry-pick security fixes only). Drift-into-divergence is forbidden.
4. **Upstream generic fixes** — Linux fixes upstream will accept go upstream as PRs; every merge shrinks the fork diff.

---

## D8 — Reverse engineering (REA) demoted to optional gap-fill

**Decision.** Source-first everywhere. REA tooling is used only where the source can't answer: shipped AppImage (1.37.0) vs repo `main` deltas, and passive runtime confirmation of the desktop↔cloud protocol (own traffic, credentials excluded). This matches the REA skill's own rule: complete source repo → normal repository tools.

---

## D9 — Milestone order: Linux-first dogfood

Date: 2026-10-14 (post-recon sign-off session) · Status: accepted

**Context.** After M1 (rebrand), three build tracks compete for attention: M2 Linux hardening, M3 self-host/un-gate, M4a Android triage.

**Options weighed.** Linux-first dogfood *(chosen)* · mobile-first (prove the free-mobile story earliest) · all tracks fully parallel.

**Decision.** When tracks compete, M2 (Linux) wins. M3/M4a proceed in the background.

**Rationale.** The author runs the experimental Linux AppImage daily — M2 delivers value to its own user fastest; it is the lowest-unknown track; generic Linux fixes can go upstream while the fork diff is smallest; the dogfood pain log is the M2 spec.

**Consequences.** Android E2E (M4b) still waits on M3, and the beta needs M2 + M4b — so M3's Phase 1 investigation must not be starved. Priority means ordering, not starving.