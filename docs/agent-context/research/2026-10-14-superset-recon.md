# Superset recon — evidence log

Date: 2026-10-14 · Session: forkbase planning
Method: GitHub page fetches + local shell inspection. No clone, no source reading beyond public tree listings.

Legend: ✅ verified this session · 🔶 inferred (name/shape suggests it; Phase 1 confirms) · ❌ explicitly not done.

## Upstream repository (superset-sh/superset)

- ✅ **Product**: "agentic IDE to orchestrate 100+ coding agents in parallel"; surfaces = desktop app, CLI, TypeScript SDK (`@superset_sh/sdk`), MCP server. 15.2k stars · 1.4k forks · 4,909 commits · ~500 open PRs · README: "we ship daily".
- ✅ **License**: Elastic License 2.0. README: "use it, fork it, modify it, self-host it for your team. The only thing off the table is repackaging Superset itself as a service you sell to others."
- ✅ **Platform support** (README): macOS primary (.dmg) · Linux x64 AppImage "experimental" · Windows "not yet available". **Mobile requires Superset Pro, iOS 26 or later, and a computer with Remote Access enabled.**
- ✅ **Stack**: Bun (pinned `.bun-version`, v1.4.2+ required) · TypeScript · turbo monorepo (`turbo.jsonc`) · biome (`biome.jsonc`) · lingui · bun workspaces (`bun.lock`, `bunfig.toml`). Dev prereqs: `docker`, `jq`, `gh`.
- ✅ **Dev setup** (README): `./.superset/setup.local.sh` brings up local Postgres + neon-proxy + Redis via Docker, seeds a dev account ("Sign in as dev", or `admin@local.test` / `supersetdev`), needs no third-party credentials; `bun run dev`; the dev app runs alongside the installed app (per-workspace identity/ports).
- ✅ **Agent docs**: `docs.superset.sh/llms.txt` (index) and `docs.superset.sh/llms-full.txt` (full docs in one file).
- ✅ **`apps/`**: api · desktop · docs · gate · marketing · mobile · realtime · relay · review-host · usercontent · web.
- ✅ **`packages/`** (26): agent-setup · auth · chat · chat-runtime · chat-ui · cli · cli-framework · cloud-client · db · email · host-client · host-service · i18n · local-db · macos-process-metrics · mcp · panes · port-scanner · pty-daemon · sandbox · sdk · shared · trpc · ui · workspace-client · workspace-fs.
- ✅ **`apps/mobile` is Expo/React Native** (tree fetch): `app/` (expo-router), `eas.json`, `.eas/workflows`, `metro.config.js`, `app.config.ts`, `config-plugins/`, `store.config.js`, `RELEASE.md`, `.maestro/flows/`, `targets/agentactivity/`, iOS-oriented patch tests (e.g. `expo-observe-swift-version-patch.test.ts`), plus `AGENTS.md`/`CLAUDE.md`/`TODO.md` inside the app.
- ✅ Root docs of interest: `DEVELOPMENT.md`, `CONTRIBUTING.md`, `HOOKS_INVESTIGATION.md`, `TODO.md`, `WARP.md`; `.superset/` workspace config (setup/teardown/run scripts); `plugins/` + `.agent-marketplace.json` (plugin mechanism exists).

## Local install (this machine)

- ✅ `~/Applications/Superset.AppImage` — 413,300,973 bytes; mounted at `/tmp/.mount_SupersgxLDVg`; Electron runtime (chrome_*.pak, chrome_crashpad_handler, chrome-sandbox, libEGL/libGLESv2, icudtl.dat).
- ✅ CLI `superset` reports 1.37.0; shim: `exec /tmp/.mount_SupersgxLDVg/resources/resources/bin/superset`.
- ✅ Mount resources dir contains: `bin/ chat-migrations/ host-migrations/ migrations/ superset/` — DB migration sets ship in the binary.
- ✅ `~/.superset/bin/` shims 15 agent CLIs: amp, claude, codex, copilot, cursor-agent, devin, droid, gemini, grok, kimi, mastracode, muse, opencode, ufo, vibe.
- ✅ Live state dir `~/.superset/`: `local.db` (+wal/shm), `app-state.json`, `sessions/`, `worktrees/`, `hooks/`, `terminal-host.sock/.pid/.token`, `daemon.log`, `resources.jsonl`, `plugins/`, `host/`, `auth-token.enc`.
- ✅ This worktree: `~/.superset/worktrees/forkbase/nebula-earthworm-c986f9aa` — empty repo (single "Initial commit", branch `nebula-earthworm-c986f9aa`).
- ✅ Author's machine: Omarchy (Arch Linux, Hyprland) — the "experimental" Linux AppImage is the daily driver.

## Inferred — 🔶 to confirm in Phase 1

- 🔶 `apps/gate` is where Pro/billing gating lives (name only).
- 🔶 `apps/relay` tunnels phone ↔ desktop via the cloud; `realtime` carries live updates; `review-host`/`usercontent` serve Pages/PR review content.
- 🔶 Pro gating is account/billing checks against upstream's hosted cloud — i.e. removable in self-host mode.
- 🔶 Mobile's cloud-account coupling depth (how hard self-hosted auth will be).
- 🔶 Android blocker inventory (no `expo run:android` yet).

## Not done — ❌

- ❌ No clone; no source file read (only public GitHub tree listings).
- ❌ No AppImage extraction or binary analysis (deferred, decision D8).
- ❌ No runtime protocol observation.
- ❌ No reading of `local.db` contents (paths listed only).
- ❌ No secrets accessed: `auth-token.enc` and credential files were never opened.

**Postscript (2026-10-14, later same day):** the fork was cloned to `~/Workspace/forkbase` — source reading is now possible, and this ❌ list is historical for the planning session only.