# cheetahbyte's Skills

## Contained Skills

- [`agy`](skills/agy/SKILL.md): delegate research, read-only code review, or collaborative sparring to Agy CLI when you explicitly request it.
- [`writing-plans`](skills/writing-plans/SKILL.md): turn an agreed design into a bite-sized, TDD-driven implementation plan with no placeholders, for a fresh agent or later session to execute. Skip it when the same session implements. Adapted from a personal `writing-plans` skill inspired by [obra/superpowers](https://github.com/obra/superpowers)
- [`pare`](skills/pare/SKILL.md): use to inspect and simplify code before making changes. Overlaps Claude Code's built-in `/simplify`, but proposes findings and waits for approval before editing, and refuses to change observable behavior. Manual invocation only. This skill is largely inspired by Noah Dunnagan's [cafe/distill](https://github.com/noahdunnagan/cafe/tree/main/plugins/distill) plugin.
- [`engineering-defaults`](skills/engineering-defaults/SKILL.md): apply the canonical technology stack when starting a project or choosing frameworks, UI, data, authentication, hosting, testing, or other dependencies.
- [`google-developer-docs-style`](skills/google-developer-docs-style/SKILL.md): apply Google's clear, accessible, globally understandable style to technical documentation, README files, tutorials, API docs, UI instructions, and Markdown or HTML content.
- [`wiki-maintainer`](skills/wiki-maintainer/SKILL.md): maintain Craft documentation as a searchable knowledge base: search first, update the canonical document, file by the existing folder taxonomy. Needs the Craft MCP tools (`craft_craft_read`, `craft_craft_write`).
- [`straight-answer`](skills/straight-answer/SKILL.md): keep verdicts independent of the user's preferred answer when validating decisions, reviewing work, or writing advocacy.
- [`herdr-delegation`](skills/herdr-delegation/SKILL.md): decide when the lead session delegates to Herdr worker panes, Agy for plan review and Pi (Sol, Luna, Astra) for everything else, how to brief them, and how to verify what comes back. Needs `HERDR_ENV=1` and `herdr --skill` for the mechanics.
