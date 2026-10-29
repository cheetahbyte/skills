# cheetahbyte's skills

## Contained skills

### Collaboration

- [`ship`](skills/collaboration/ship/SKILL.md): commit, push, and open or update a PR. Conventional Commits messages and titles, plus PR bodies with concise summaries, visual explanations, concrete evidence, and risk and rollback assessments. The PR body is inspired by Matt Pocock's [`engineering/pr`](https://github.com/mattpocock/skills/blob/main/skills/engineering/pr/SKILL.md) skill.

### Engineering

- [`vet`](skills/engineering/vet/SKILL.md): read-only review of a change through three lenses: defects, spec conformance, and structure. Reports one line per finding with severity and proof, and hands behavior-preserving cleanup to `pare`. Combines ideas from [mattpocock/skills](https://github.com/mattpocock/skills), [juliusbrussee/caveman](https://github.com/juliusbrussee/caveman), [coderabbitai/skills](https://github.com/coderabbitai/skills), [cursor/plugins](https://github.com/cursor/plugins), and [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli).
- [`pare`](skills/engineering/pare/SKILL.md): inspect and simplify code before making changes. Overlaps Claude Code's built-in `/simplify`, but proposes findings and waits for approval before editing, and refuses to change observable behavior. Manual invocation only. Largely inspired by Noah Dunnagan's [cafe/distill](https://github.com/noahdunnagan/cafe/tree/main/plugins/distill) plugin.
- [`writing-plans`](skills/engineering/writing-plans/SKILL.md): turn an agreed design into a TDD-driven implementation plan for a fresh agent or later session to execute, or execute one task from such a plan. It drafts the plan first with `UNKNOWN` markers, then checks each one with a single lookup, and records the decisions from the conversation that the implementer never saw. Inspired by [obra/superpowers](https://github.com/obra/superpowers).
- [`diagnosing-bugs`](skills/engineering/diagnosing-bugs/SKILL.md): a diagnosis loop for hard bugs, failing CI, and performance regressions: build a tight feedback loop first, then reproduce, hypothesize, instrument, and fix. From [mattpocock/skills](https://github.com/mattpocock/skills) (MIT).
- [`research`](skills/engineering/research/SKILL.md): investigate a question against primary sources in a background agent and save the cited findings as Markdown. From [mattpocock/skills](https://github.com/mattpocock/skills) (MIT).
- [`techstack`](skills/engineering/techstack/SKILL.md): apply the canonical technology stack when starting a project or choosing frameworks, UI, data, authentication, hosting, testing, or other dependencies.

### Other

- [`google-developer-docs-style`](skills/other/google-developer-docs-style/SKILL.md): apply Google's clear, accessible, globally understandable style to documentation files and UI instructions.
- [`straight-answer`](skills/other/straight-answer/SKILL.md): keep verdicts independent of the user's preferred answer when validating decisions, reviewing work, or writing advocacy.
- [`writing-for-agents`](skills/other/writing-for-agents/SKILL.md): reference for writing skills, `AGENTS.md`, and `CLAUDE.md`. From [mattpocock/skills](https://github.com/mattpocock/skills) (MIT).
- [`terse`](skills/other/terse/SKILL.md): direct, concise user-facing replies: answer first, and remove filler, flattery, repetition, and unnecessary formatting without losing needed detail. Not invocable by the user or the model; load it with a session-start hook.
