# Mode: Codebase architecture review

## Scope intelligently

If the user specified a feature or module, inspect that area and its callers/dependencies. Otherwise:

1. Read project README, architecture docs, ADRs, conventions, relevant domain glossary, deployment topology, tests.
2. Sample recent changes (`git log`, `git diff`, recent bug-fix patterns) and identify frequently touched paths. History is a **prioritization hint**; new or unusually risky modules may also matter.
3. Trace 1–3 representative user flows end to end across their meaningful module interfaces.
4. Inspect implementation/callers for suspected duplicated decisions, orchestration, implicit contracts and failure semantics.
5. Stop when additional scanning is unlikely to change the top recommendations. Explicitly report scope limitations.

Use available read/search capabilities rather than assuming a particular shell, repository, subagent framework, `git` history, or UI. Never claim to have reviewed the whole codebase after sampling.

## Investigate and substantiate

For each candidate:

- **Observation**: exact paths/symbols and excerpt or line references if available. Distinguish direct reading from inference.
- **Cost mechanism**: e.g., a new field requires four coordinated edits; callers know parsing details; errors are dropped.
- **Change scenario**: plausible, motivated by existing product usage, history, or current requirements.
- **Alternatives**: keep it, merge responsibilities, extract knowledge-owning mechanism, revise contract, or remove redundant layer.
- **Counterargument**: why current separation might be intentional and valuable, e.g., different availability/security/ownership constraints.
- **Risk & verification**: caller compatibility, behavioral tests, migration, performance benchmark where warranted.
- **Confidence**: high/medium/low based on evidence quality.

A smell is not a finding unless it has an articulated cost mechanism and evidence. Don't present duplicate-looking code as a defect when it represents different policies.

## Rank

Use **Strong / Worth exploring / Speculative / Keep** according to `SKILL.md`. Weight expected maintenance benefit against probability of future changes, implementation risk, and scope. High-risk design with hidden incorrectness may take priority over frequency.

Limit main report to the most useful candidates (normally 3–7); summarize minor observations separately or omit them. Do not rank based purely on number of files, lines, or wrappers.

## Artifact choice

Default to concise Markdown review in conversation/repo file if requested. If the user specifically requests a visual deliverable or it materially aids decisions, create a standalone offline-readable HTML report using `references/reporting.md`. Do not force HTML, a browser opening, or a temp file in environments where these are unavailable or unwelcome.

## Review output template

**Scope:** examined modules, sampled flows, docs/ADRs, relevant history and test evidence.

**Finding:** short title; confidence; recommendation strength.

**Evidence:** path and observable behavior; specific plausible change.

**Complexity mechanism:** why caller/maintainer work increases.

**Option / trade-off:** proposed change and counterargument.

**Validation:** tests, metrics or exploration that would change the decision.

**Next action:** single top recommendation or "no architectural refactor justified".

Present findings before detailed alternatives unless the user asked for a full redesign. Avoid prematurely specifying a new public interface in a discovery-only audit.
