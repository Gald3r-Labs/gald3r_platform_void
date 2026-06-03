# gald3r Readiness Report — Void

> An honest accounting of how much of the gald3r framework installs natively on this
> platform, what degrades to an approximation, and what has no native home yet.
> Generated from a live documentation crawl on 2026-06-02.

**Overall readiness: ⚠️ Partial.** Void is an open-source VS Code fork focused on
direct-to-LLM AI coding (Agent / Gather / Chat modes). Only two of gald3r's six layers land
natively — rules (`.voidrules`) and MCP (`mcp.json`). Commands, agents, skills, and hooks
have no native host; with upstream development paused since mid-2025, none of those gaps are
expected to close.

## C.R.A.S.H. capability grid

| | Capability | Native? | What gald3r gets here | The gap |
|---|---|:---:|---|---|
| **C** | Commands | ❌ | Built-in palette actions only (`Void: New Rule`, Quick Edit `Ctrl+K`); "prompt editing" exposes the system prompts | No user-defined command system — gald3r's `@g-*` command set can't install as native commands |
| **R** | Rules | ✅ | `.voidrules` — a single always-on project-root file prepended to chat context (Cursor-style), managed from the rules explorer | None for a flat file — but no `.void/rules/` directory (proposed in #643, unmerged), so multi-file rules collapse into one |
| **A** | Agents | ❌ | Fixed product modes only: Agent (full file/terminal/MCP access), Gather (read-only), Chat | No user-definable sub-agents — gald3r's `g-agnt-*` roles with scoped tools/models have no native mapping |
| **S** | Skills | ❌ | — | No `SKILL.md` / Agent Skills engine anywhere in docs, changelog, or codebase; gald3r skills can't install |
| **H** | Hooks | ❌ | — | No lifecycle hook API (no session-start / pre-tool / pre-commit / file-watch); gald3r's `g-hk-*` wiring can't fire (auto-approve request #629 is unmerged and isn't a script hook) |

_Legend: ✅ native · ⚠️ partial / approximated · ❌ no native mechanism · ❓ unverified_

**Beyond C.R.A.S.H. — MCP: ✅** Native Model Context Protocol support via a user-editable
`mcp.json` (`~/[appName]/mcp.json`); an MCP service manages server lifecycle and exposes
external tools to Agent mode. gald3r's MCP backend connects here — though the integration is
narrower than Cursor's and has had reliability issues (e.g. #752).

## Adoptable extras (non-C.R.A.S.H.)

Platform-native strengths gald3r can lean on, and which need wiring:

| Feature | Status | gald3r fit |
|---|:---:|---|
| VS Code extension ecosystem (one-click import) + themes/keybinds/settings | ✅ present | Inherited dev surface; not an AI-agent extension point, no gald3r work required |
| Fully open source (editable built-in system prompts; forkable) | ⚙️ needs customization | Lets gald3r inject behavior by editing prompts or forking — high effort, not a clean install |
| `@file` / `@folder` context references + AI commit message generation | ✅ present | Extra context/input surfaces gald3r can use as-is |
| Agent checkpoints/revert · persistent background terminals · SSH/WSL | ✅ present | Useful workflow primitives; no gald3r work required |

## The honest ceiling

gald3r adapts to this platform the way any third-party layer must — by mapping our commands,
rules, agents, skills, and hooks onto whatever extension points the platform happens to
expose. Where those points exist, the fit is clean. Where they don't, adaptation can only
*approximate* the real thing — a stand-in that covers the common case but not the edges.

That isn't a knock on the platform. It's the ceiling of bolting *any* framework onto a
surface that was never built to host it.

Full functional parity isn't something we can reach from the outside. It lives in the native
build — **gald3r_agent**, running on the **gald3r throne** over the **gald3r_world_tree** —
where commands, rules, agents, skills, and hooks aren't *adapted* to the platform, they *are*
the platform.

> ### gald3r_agent — coming soon. 🌳

---

<sub>Capabilities verified against the platform's official documentation on 2026-06-02, and
re-verified each release via the gald3r platform-docs crawl. This report describes gald3r's
third-party adaptation surface; it is not an endorsement or critique of the platform itself.</sub>
