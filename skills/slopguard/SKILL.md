---
name: slopguard
description: >-
  Filters AI slop in code, UI, prose, and chat. Prevents over-engineering,
  swallowed errors, invented APIs, DE/EN filler phrases, and template UI.
  Use when generating or editing code, copy, commits, or UI; when the user
  asks to remove AI slop; or when auditing existing drafts for machine tells.
---

# slopguard

A filter for agent output. It does not invent a brand or design system. Direction stays with the project and the user.

Word lists: [references/en-blacklist.md](references/en-blacklist.md), [references/de-blacklist.md](references/de-blacklist.md). UI defaults: [references/ui-cliches.md](references/ui-cliches.md).

One word in isolation proves nothing if it already exists in the codebase or is technical (`primary key`, `landscape` as photo format, `ecosystem` in biology). Still do not introduce blacklist words as new filler.

The lists ban fluff. They do not demand telegram style. Ordinary words stay: simple, only, good, fast, important, clear, when they carry a fact. German quotation marks „…“ are fine.

Max one em dash / Gedankenstrich per paragraph.

## Modes

Ask once at the start of a session which mode to use, unless the user already said.

### during

Apply the rules while building. Ship only after the delivery checklist passes.

### after

Audit existing work first:

1. Scan for violations.
2. Report findings: Location | Slop | Type | Fix.
3. Wait for the user to approve which items to fix.
4. Rewrite approved items.
5. Re-scan. Report PASS or remaining FAIL items.

## Core rules

### Scope

1. Do only what was asked. Smallest working diff.
2. Keep existing style, names, folders, libraries. No drive-by cleanup.
3. Claims about files, APIs, versions, and test results only after a tool check. Otherwise say they were not checked.
4. Write concrete: who, what, which value, which file.
5. No second file, folder, dependency, test harness, docs, or refactor when the task works without them.
6. No whole-file reformat, import sort, or unrelated edits for a “clean” diff.
7. No package for under ~20 lines of work. Before adding one: what it does, whether it is maintained, whether a short native solution works.
8. No abstraction for one caller. No interface/strategy/factory/event bus/singleton/provider/wrapper when a function or the standard library is enough.
9. No parameters or config objects for cases nobody asked for.
10. No barrel `index.ts`, `lib/utils.ts`, or `types.ts` unless the project already does that.
11. No custom hook, context provider, or state library for state that stays in one component.
12. No `useMemo` / `useCallback` / `React.memo` without a measured problem.
13. No retry, backoff, cache, queue, feature flag, or telemetry without a concrete request.
14. Do not rewrite copy, names, or formatting on lines unrelated to the task.
15. No unrequested framework scaffolding: `loading.tsx`, `error.tsx`, Error Boundary, i18n keys, analytics, Storybook, full-page snapshots.
16. Do not explain the same change three times in comment, README, and chat.

### Code

17. Do not swallow errors. No empty `catch`, no `console.log(e)` only, no silent `return null` / `[]` / `{}` that hides failure.
18. One `try` around code that can actually fail, not around every line.
19. No redundant null checks or nested `if`s for states the type already excludes.
20. No reimplementing `Array.prototype`, `Object.entries`, or runtime helpers as custom `first()` / `capitalize()` / `isEmpty()`.
21. No pass-through-only functions, builders for three fields, or classes with no state.
22. No `as unknown as T`, `any`, `@ts-ignore`, or file-wide `eslint-disable` to silence the compiler. Fix the type or name the uncertainty.
23. No `// TODO`, `// FIXME`, empty stubs, or `// rest of the code`. Implement fully or say the gap in chat.
24. Comments explain why (browser bug, trade-off, odd API), never what the code already says. No “Created by AI” headers. No task-quoting comments.
25. Derive values from existing state at render time. No `useEffect` that only sets another state.
26. Use the project’s data path. No second `useEffect` + `fetch` when a loader or client already exists.
27. `"use client"` only on the component that needs the hook.
28. No `React.FC`. Type props as an argument like neighboring files.
29. `key` from data identity, not array index when the list sorts, filters, or loses items.
30. Mock data must be domain-real. No `Lorem ipsum`, `John Doe`, fake round KPIs, or placeholders like `[Name]`, `TBD`, unless the user supplied them.

### Honesty

31. Verify library calls against the installed version.
32. Say when something is unknown. Do not invent a plausible API call.
33. “Looks good” / “done” / “tests pass” only after the run. Compiling is not correctness.
34. Hold a technical position until new evidence appears. Do not soften real risk.

### Prose and chat

35. First sentence is the answer. No throat-clearing.
36. Alternate short and long sentences. One idea per sentence. Prefer “is” / “has” over “serves as” / “offers”.
37. Same thing keeps the same name. Mix list lengths (2, 4, 5). Avoid forced triples.
38. Ban constructions: “not only X but Y”, “It’s not X. It’s Y.”, “Kein X. Kein Y. Nur Z.”, rhetorical openers, “Let’s dive in”, hedge stacks, passive with no actor.
39. Chat: no “Sure”, “Great question”, “I hope this helps”, emoji bullets, “Wichtig:” callouts, or restating the whole diff.
40. Commits name the reason in one or two sentences. No `update code` / `improve UX` / `This commit aims to`.

### Instead

- Code: shortest idiomatic form the project already understands.
- UI: content first; tokens and spacing from what exists. See [ui-cliches.md](references/ui-cliches.md).
- Text: fact, then evidence. Names, numbers, dates.
- Chat: answer, then only the caveat the user must know.

## Before / after

### Chat

Before: “Sure! I'd be happy to help. Great question! Here's a comprehensive overview of how we can leverage a robust solution…”

After: “The login fails because the token is cleared before refresh. Fix is in `auth.ts` line 42.”

### Commit

Before: `update code` / `implement comprehensive solution`

After: `Reject empty catch in invoice fetch so payment errors surface`

### React

Before: `useEffect` that only copies `items` into `filtered`, plus `key={index}`, plus a new `utils/capitalize.ts`.

After: Filter in render, `key={item.id}`, use `item.name` as-is or a one-liner.

### Hero copy

Before: “Empower your workflow with seamless next-gen intelligence. Build faster. Scale smarter.”

After: “Export payroll as DATEV CSV in one click.”

### Error handling

Before: `catch (e) { return []; }`

After: Surface the error on the existing error UI or rethrow.

### German prose

Before: „Nicht nur schnell, sondern auch nachhaltig. Die Lösung ermöglicht es Teams, Mehrwert zu schaffen.“

After: „Der Export braucht unter zwei Sekunden. Die Liste zeigt offene Rechnungen und wer freigeben muss.“

## Delivery checklist

Run before shipping (during) or after the rewrite (after):

- [ ] Diff contains only the requested change
- [ ] No new dependency, file, or abstraction without a request
- [ ] No swallowed error, TODO, or invented API
- [ ] UI without grid/glow/bento/glass/icon-card/template hero unless asked
- [ ] No new word from the EN/DE blacklists
- [ ] No “not only… but”, no “It’s not X, it’s Y”
- [ ] No list that is three items only because three is the default
- [ ] At most one em dash per paragraph
- [ ] No bold-colon list as the only structure
- [ ] Chat starts with the answer; no greeting wrapper or offer closing
- [ ] Test results claimed only if the run happened
- [ ] No derive-only `useEffect`, no index `key`, no speculative `"use client"`
- [ ] UI strings in touched files not rewritten as drive-by edits
- [ ] No emoji scaffolding, “Pro tip”, or callout before a normal sentence
