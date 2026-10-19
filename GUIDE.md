# slopguard guide

Install, update, and remove. English for discoverability; the skill itself is DE+EN.

## What you get

| Path | Use |
|------|-----|
| `skills/slopguard/` | Agent skill (`SKILL.md` + `references/`) |
| `rules/slopguard.mdc` | Cursor always-on rule |
| `slopguard.md` | Paste into any chat / custom instructions |
| `AGENTS.md` | Compact pointer for agent entry files |

## Install

### skills.sh / npx skills (recommended for agents)

```bash
npx skills add taner-svg/slopguard
```

Or with an explicit skill name:

```bash
npx skills add taner-svg/slopguard --skill slopguard
```

Start a new agent session after install so the skill loads.

### Cursor rule (always on)

1. Copy `rules/slopguard.mdc` to your project’s `.cursor/rules/slopguard.mdc`.
2. Optionally also install the skill so blacklists in `references/` are available as linked files.
3. New chat / agent session.

### Claude Code / Codex / other skill folders

Copy the folder `skills/slopguard` into the skills directory your agent reads (project or user level). See your agent’s docs for the exact path.

You can also append the pointer from root `AGENTS.md` to your project `AGENTS.md`, `CLAUDE.md`, or equivalent.

### Paste-only (ChatGPT, Gemini, any window)

```bash
curl -o slopguard.md https://raw.githubusercontent.com/taner-svg/slopguard/main/slopguard.md
```

Paste the file contents into Custom Instructions or the system prompt. No folders required.

### Manual clone

```bash
git clone https://github.com/taner-svg/slopguard.git
```

Then copy `skills/slopguard` and/or `rules/slopguard.mdc` as above.

## Update

Skills installed via `npx skills`:

```bash
npx skills update
```

Or re-clone / pull this repo and copy files over again. Rules and paste files do not auto-update; replace them from `main`.

Start a new session after updating.

## Remove

- Delete the installed `slopguard` skill folder from your agent’s skills directory.
- Delete `.cursor/rules/slopguard.mdc` if you added it.
- Remove any pointer block you appended to `AGENTS.md` / `CLAUDE.md`.
- Clear pasted custom instructions that came from `slopguard.md`.

## Modes

At session start the skill asks **during** vs **after** unless you already chose.

- **during** — filter while generating; run the delivery checklist before shipping.
- **after** — audit existing work, list findings, wait for approval, then fix.

## Troubleshooting

- Skill not loading: confirm the folder name is `slopguard` and contains `SKILL.md`; open a new session.
- Rule not applying in Cursor: check `alwaysApply: true` in the `.mdc` frontmatter and that the file is under `.cursor/rules/`.
- Name clash: other tools also use “slopguard” for dependency scanning. This repo is an **output filter**, not an install firewall.
