---
name: pr-writeup
description: "Use when writing or updating a PR body."
metadata:
  category: collaboration
---
## Before Writing

- Inspect the actual diff against the target branch.
- Read surrounding code when necessary.
- Follow repository conventions and `GLOSSARY.md` if available.
- Describe what was implemented, not merely what was requested.
- Never invent implementation details, tests, benchmarks, or results.

## Template

~~~markdown
## Summary

<What changed? Use a visual if it improves clarity.>

## Why

<What problem motivated this change?>

## Evidence

<Verified before/after behavior, tests, benchmarks, or screenshots.>

## Risk & Rollback

**Reversibility:** <Reversible | Requires migration | Irreversible>

**Blast Radius:** <Affected components or consumers>

<Potential failure modes and rollback constraints.>
~~~

## Summary

Explain the change in 1–3 sentences.

Choose the smallest visual that makes the implementation clear:

- **Pseudocode:** Algorithms and behavior.
- **Call tree:** Execution flow.
- **Component tree:** UI structure and state ownership.
- **File tree:** Refactors and module boundaries.
- **Mermaid:** Component interactions and data flow.
- **Diff sketch:** Structural or behavioral changes.

Use multiple visuals only when they explain distinct aspects. Omit visuals when prose is clearer.

## Why

Explain the problem, limitation, or inefficiency motivating the change.

Focus on why the previous behavior was insufficient, not what the implementation does.

Omit this section when the motivation is already obvious from the summary.

## Evidence

Provide concrete verification, preferably:

1. Before/after screenshots for visual changes.
2. Failing-before/passing-after tests for bug fixes.
3. Benchmarks for performance changes.
4. Actual build, test, or execution results.

For benchmarks, include the workload, environment, baseline, and measured results.

Never fabricate evidence. If tests were not run, state `Not run` and explain why when known.

Do not confuse compilation, tests, benchmarks, and manual inspection.

## Risk & Rollback

**Reversibility:**
- `Reversible` — A code revert safely restores previous behavior.
- `Requires migration` — Rollback requires additional steps.
- `Irreversible` — Previous state cannot reliably be restored.

**Blast Radius:** Identify affected components, platforms, APIs, persisted data, or users.

Briefly explain plausible failure modes, compatibility concerns, and rollback constraints. Avoid speculative risks unrelated to the diff.

## Rules

- Output only the PR body.
- Skip preambles and conclusions.
- Be technically precise and concise.
- Prefer concrete behavior over implementation trivia.
- Never present assumptions as verified facts.
- Avoid repeating information across sections.
- Scale detail to the complexity of the PR.
- Follow existing repository conventions.
