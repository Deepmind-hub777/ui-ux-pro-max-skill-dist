# ui-ux-pro-max — skill package

A distributable copy of **UI/UX Pro Max**, a local, searchable design-intelligence
skill pack for AI coding agents. 75 files, ~3.7 MB, no external dependencies beyond
Python 3.x.

Upstream: <https://github.com/nextlevelbuilder/ui-ux-pro-max-skill>
License: MIT — see `LICENSE` (Copyright © 2024 Next Level Builder)

This repository is a redistribution, not the upstream project. Issues about the
underlying data or scripts belong upstream. No modifications have been made to the
skill content beyond dropping compiled `__pycache__` artifacts.

---

## What it contains

| Data | Count | File |
|---|---|---|
| Styles | 80 searchable (51 active) | `data/styles.csv` |
| Product palettes + reasoning profiles | 192 | `data/products.csv`, `data/ui-reasoning.csv` |
| Font pairings | 74 | `data/typography.csv` |
| Google Fonts | 1,934 | `data/google-fonts.csv` |
| Curated icons | 105 | `data/icons.csv` |
| UX guidelines | 120 | `data/ux-guidelines.csv` |
| Motion presets | 17 | `data/motion.csv` |
| Chart types | 25 | `data/charts.csv` |
| Stack guideline sets | 22 stacks, 1,278 rules | `data/stacks/*.csv` |

Supporting files: `SKILL.md` (the instruction file an agent reads),
`references/quick-reference.md` (full rule text by priority),
`references/pro-rules.md` (native-app polish + pre-delivery checklist),
`scripts/search.py` (the search entry point),
`scripts/tests/` (data-contract tests).

Everything is local CSV/JSON — no API calls, no keys, nothing leaves the machine.

## How an agent loads it

The pack follows the plain `SKILL.md` convention, so any agent that supports
skill directories can use it.

**Claude Code / Claude Cowork**
```bash
mkdir -p .claude/skills
cp -r ui-ux-pro-max .claude/skills/
```
The agent reads `.claude/skills/ui-ux-pro-max/SKILL.md` and calls
`scripts/search.py` by absolute path.

**Other agents (Cursor, Codex, custom harnesses)**
Point the agent's skill root at this directory. Two requirements:
1. The agent must read `SKILL.md` before acting.
2. `scripts/search.py` must be invoked by its absolute path — it lives inside the
   skill directory, not the user's project.

Run it standalone any time:
```bash
python3 scripts/search.py "saas dashboard analytics" --design-system
python3 scripts/search.py "keyboard focus modal" --domain ux
python3 scripts/search.py "chip badge overflow" --stack html-tailwind
```

Requires Python 3.x. No third-party packages.

## Coverage note

The data is a snapshot. `data/catalog-summary.json` records `verifiedAt: 2026-11-04`
and per-dataset SHA-256 hashes, so you can tell whether a copy has drifted. Font and
icon data derive from Google Fonts and Phosphor Icons — see `THIRD_PARTY_NOTICES.md`.

## Reuse

MIT. Keep `LICENSE` and this attribution with any copy or substantial portion.
