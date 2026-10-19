# slopguard

This project uses **slopguard**: a filter against AI slop in code, UI, prose, and chat.

## Load

- Skill (preferred): `skills/slopguard/SKILL.md` and its `references/`
- Cursor always-on rule: copy `rules/slopguard.mdc` into `.cursor/rules/`
- Single paste file: `slopguard.md` for any LLM custom instructions

## Behavior

1. Ask once whether mode is **during** (apply while building) or **after** (audit → findings → approve → fix), unless already specified.
2. Follow the skill’s core rules and delivery checklist.
3. Do not invent APIs, swallow errors, or ship template UI/copy by default.
4. EN/DE blacklists live under `skills/slopguard/references/`.

## Not the same as

- Dependency “slopguard” CLIs that block typosquat packages
- Other anti-slop products focused mainly on UI liveliness or English writing only

This pack emphasizes over-engineering, honesty (verified claims), DE+EN prose, and chat hygiene.
