# cheetahbytes Skills

## Contained Skills

- [`agy`](skills/agy/SKILL.md): delegate research, read-only code review, or collaborative sparring to Agy CLI when you explicitly request it.
- [`brainstorming`](skills/brainstorming/SKILL.md): use before substantial creative or feature work that requires design. Explores the existing project, delegates unresolved user-owned decisions to Grill Me, evaluates implementation approaches, and produces an approved technical design before planning. Inspired by [obra/superpowers/brainstorming](https://github.com/obra/superpowers/tree/main/skills/brainstorming)
  - **Requires** the `grill-me` skill (not bundled in this repo) to resolve user-owned product/behavior decisions — brainstorming can't complete its workflow for substantial changes without it.
  - **Recommends** (not required) the `writing-for-agents` skill as a reference when drafting the design doc, so it's written to be consumed reliably by `writing-plans` afterward.
  - Both `grill-me` and `writing-for-agents` are part of Matt Pocock's personal skill collection.
  - Without `grill-me`, brainstorming falls back to asking the user-owned questions itself, one at a time.
- [`writing-plans`](skills/writing-plans/SKILL.md): use once a design/spec is approved to turn it into a bite-sized, TDD-driven implementation plan with no placeholders. Hands off from `brainstorming`. Adapted from a personal `writing-plans` skill inspired by [obra/superpowers](https://github.com/obra/superpowers)
- [`pare`](skills/pare/SKILL.md): use to inspect and simplify code before making changes. Overlaps Claude Code's built-in `/simplify`, but proposes findings and waits for approval before editing, and refuses to change observable behavior. Manual invocation only. This skill is largely inspired by Noah Dunnagan's [cafe/distill](https://github.com/noahdunnagan/cafe/tree/main/plugins/distill) plugin.
- [`engineering-defaults`](skills/engineering-defaults/SKILL.md): apply the canonical technology stack when starting a project or choosing frameworks, UI, data, authentication, hosting, testing, or other dependencies.
- [`google-developer-docs-style`](skills/google-developer-docs-style/SKILL.md): apply Google's clear, accessible, globally understandable style to technical documentation, README files, tutorials, API docs, UI instructions, and Markdown or HTML content.
- [`wiki-maintainer`](skills/wiki-maintainer/SKILL.md): maintain Craft documentation as a searchable knowledge base: search first, update the canonical document, file by the existing folder taxonomy. Needs the Craft MCP tools (`craft_craft_read`, `craft_craft_write`).
- [`straight-answer`](skills/straight-answer/SKILL.md): keep verdicts independent of the user's preferred answer when validating decisions, reviewing work, or writing advocacy.
