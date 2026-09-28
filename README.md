# mac-dev-skills

A Claude Code plugin for modern **macOS 26/27 AppKit** development — the macOS counterpart to Microsoft's `win-dev-skills`. Skills, an orchestrator agent, and grounded native Swift tooling that stops the agent guessing.

## Install
Add this marketplace, then install the `appkit` plugin:
- `/plugin marketplace add malstrom/mac-dev-skills`
- `/plugin install appkit`

To install only the skills in any agent that supports [Agent Skills](https://agentskills.io) (Cursor, Codex, Gemini CLI, and others), without the `appkit-dev` agent:
```bash
npx skills add markmals/mac-dev-skills
```

Without `npm`, use [Rosie](https://rosieskills.dev), a standalone skills installer available from Homebrew:
```bash
brew install rosieskills/rosie/rosie
rosie install markmals/mac-dev-skills
```

## What's inside
- **14 skills** under `plugins/appkit/skills/` — `appkit-design` (the flagship: control selection, layout, semantic color/typography, Liquid Glass, window sizing, a11y — wired to both tools), `apple-hig` (the complete Apple Human Interface Guidelines bundled offline as a router skill — the all-platform design authority `appkit-design` implements against), setup, dev-workflow, code-review, ui-testing, packaging (Developer ID + TestFlight + Mac App Store), migration, three macOS-26/27 modernization skills (launch-continuity, modern-input, liquid-glass-concentricity), `appkit-private-apis` + `appkit-app-inspector` (advanced / dual-use), and `appkit-session-report`.
- **`appkit-dev` agent** — builds AppKit apps end-to-end.
- **Native tools** — `sdk-api` (SDK API + availability validator) and `sdk-search` (AppKit/HIG pattern search). **The native tools now live in [`apple-platform-tools`](https://github.com/markmals/apple-platform-tools)**; the original `appkit-api` / `appkit-search` sources are retained here under `src/tools/` for history (see `src/tools/DEPRECATED.md`).

## Installing the tools
Install `sdk-api`, `sdk-search`, `headerdump`, and `redump` from Homebrew:
```bash
brew install markmals/tap/apple-platform-tools
```
`uitool` is in the formula too — the cooperative build, signed for `attach`. The unrestricted posture (apps you didn't sign) needs the arm64e injectable and a defanged dev box, built from a clone (see `appkit-app-inspector`).

To rebuild the superseded originals retained under `src/tools/`:
```bash
scripts/build-tools.sh
```
Requires Xcode 26 or 27 (the macOS SDK), Swift 6.

## Sync with apple-platform-tools

The AppKit skills carry generated CLI-contract references from
`apple-platform-tools` so `sdk-api`, `sdk-search`, `headerdump`, `redump`, and
`uitool` behavior changes do not drift silently. Regenerate them with:

```bash
APPLE_PLATFORM_TOOLS_ROOT=/path/to/apple-platform-tools scripts/generate-apple-platform-tools-contracts.sh
```

CI runs the same script with `--check`.

## Status
Active development. See `docs/superpowers/specs/` for the design and `docs/superpowers/plans/` for implementation plans.
