# slopguard

**A filter for AI coding agents.** Stops generic UI, filler copy, over-engineered code, and dishonest claims (invented APIs, “tests pass” without a run). DE and EN.

Not a style guide. It rejects slop; it does not pick your colors, fonts, or brand. Direction stays yours.

## Install

### Skill (Cursor, Claude Code, Codex, and other agents via skills.sh)

```bash
npx skills add taner-svg/slopguard
```

### Cursor always-on rule

Copy [`rules/slopguard.mdc`](rules/slopguard.mdc) to `.cursor/rules/slopguard.mdc` in your project.

### Paste into any LLM

```bash
curl -o slopguard.md https://raw.githubusercontent.com/taner-svg/slopguard/main/slopguard.md
```

Put the contents in Custom Instructions or the system prompt.

Step-by-step for each agent, update, and remove: [GUIDE.md](GUIDE.md).

## What it covers

- **Scope discipline** — smallest diff; no speculative factories, unused deps, drive-by renames
- **Code honesty** — no swallowed errors, no invented signatures, no “done” without a run
- **React habits** — no derive-only `useEffect`, speculative `"use client"`, index keys when identity exists
- **UI clichés** — no default purple glow, glass, icon-card grids, template heroes (see `references/ui-cliches.md`)
- **Prose** — EN + DE blacklists, banned constructions (“not only… but”, forced triples)
- **Chat** — answer first; no “Great question”, emoji scaffolds, or restated diffs

## Layout

```
skills/slopguard/SKILL.md     # core skill
skills/slopguard/references/  # EN/DE blacklists, UI clichés
rules/slopguard.mdc           # Cursor always-on rule
slopguard.md                  # single paste file
AGENTS.md                     # compact agent pointer
GUIDE.md                      # install / update / remove
```

## Usage modes

The skill asks once: **during** (filter while building) or **after** (audit → findings → you approve → fix). Both end with a delivery checklist.

## License

MIT. See [LICENSE](LICENSE).
