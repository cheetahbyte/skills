---
name: software-design
description: Design, assess, and safely improve software architecture using complexity-first reasoning, deep modules, information hiding, and evidence-backed trade-offs. Use for new modules or interfaces, architecture audits, codebase design reviews, refactoring plans, and implementation-oriented structural improvements. Does not trigger for routine formatting, small isolated bug fixes, or purely stylistic reviews unless design is at issue.
---

# Software Design

Design for **lower long-term cost of understanding and changing the system**, not for minimum lines, minimum files, maximum abstractions, or a preferred architecture pattern. Apply to functions, types, packages, applications, and distributed systems.

## Operating contract

- Inspect the actual code and its context before diagnosing it. Treat a pattern as a **hypothesis** until supported by concrete usage, change history, tests, or repeated friction.
- Preserve behavior, public compatibility, domain invariants, operational characteristics, and user constraints unless changes are explicitly authorized.
- Read existing architecture docs, domain glossary, ADRs, conventions, and tests; respect decisions unless new evidence justifies reopening them.
- Prefer **fewer facts a caller must know** and **fewer locations a maintainer must edit**. A larger internal implementation can be the simpler system.
- Prioritize evidence of change amplification, cognitive load, and unknown dependencies. Flag risk to correctness, security, observability, and performance even when reducing code complexity.
- Do not invent performance results, maintenance statistics, or codebase findings. Distinguish observation, inference, recommendation, and uncertainty.
- A valid outcome is **keep the existing design**. Do not introduce interfaces, adapters, frameworks, or generalized mechanisms solely for hypothetical future demand.
- Do not confuse test seams with public architecture. Retain internal tests when they verify valuable invariants, algorithms, failures, or performance; favor externally observable behavior for primary contract tests.
- Follow the repository's established terminology. Use the vocabulary below precisely in analysis, but do not rename domain concepts to satisfy vocabulary preferences.
- Apply book principles as heuristics, not dogma. The controlling objective is lower *system-wide* complexity under the actual constraints.

## Vocabulary

- **Module**: code with an interface and implementation, at any scale.
- **Interface**: everything a caller must know, including behavior, invariants, ordering, errors, ownership, configuration, and relevant performance promises; not merely a language `interface` declaration.
- **Implementation**: machinery hidden from callers.
- **Depth**: useful behavior and decisions encapsulated per unit of interface complexity; not lines-of-code ratio.
- **Information hiding**: keeping a design decision and its consequences in one well-chosen place.
- **Leakage**: multiple modules must know the same design decision, including undocumented coordination.
- **Seam**: a point where behavior/dependency can be replaced or controlled without modifying the consuming logic.
- **Adapter**: concrete implementation used at a seam.
- **Leverage**: repeated benefits callers get from a concise interface.
- **Locality**: changes, knowledge, debugging and tests concentrated near the owning module.

## Select the mode

Infer from the user request, do not run all modes automatically.

| Mode | Intent | Read next | Typical output |
|---|---|---|---|
| **Design** | New feature, module, contract, or architecture decision | `references/design.md`, `references/tradeoffs.md` | Options, recommended contract, ownership, risks |
| **Review** | Architecture health check, identify refactors, codebase assessment | `references/review.md`, `references/red-flags.md` | Prioritized, cited findings and optional report |
| **Refactor** | Improve an existing design or implement an accepted change | `references/refactoring.md`, `references/testing.md` | Migration plan, verified edits if authorized |

Consult `references/principles.md` to select pertinent principles, and `references/documentation.md` when designing interfaces or updating contracts. Load only relevant references; do not repeat their entire contents in output. For an HTML report load `references/reporting.md` and `templates/architecture-report.html`.

## Shared workflow

### 1. Establish scope and constraints

- Identify the actual user goal, affected area, and **explicit non-goals**. If unspecified, choose the smallest useful scope and state it.
- Find the entry points and representative callers. Inspect current contract, call flow, state, data ownership, error paths, and tests.
- Consult repository-specific guidance and existing decisions. For broad audits, start with recently changed or frequently problematic areas, then widen only if warranted.
- Capture important invariants and compatibility constraints before changing an interface.

### 2. Diagnose complexity, not aesthetics

Ask:

1. **Change amplification:** What needs editing for a plausible change? Is the same decision encoded elsewhere?
2. **Cognitive load:** What must a caller/maintainer remember to use or modify this safely?
3. **Unknown unknowns:** Which dependencies, side effects, ordering rules, or invariants are invisible?
4. **Depth:** What does the interface make easy, and what decisions does it fail to hide?
5. **Ownership:** Does one module own each nontrivial decision? Are layers adding new abstractions or simply forwarding?

Ground claims in specific locations and examples. Use `references/red-flags.md` for diagnostic tests and falsifying evidence. A red flag alone is not sufficient justification for refactoring.

### 3. Consider alternatives

For decisions with meaningful cost or irreversibility, **design it twice**: compare the current design and at least one genuinely different proposal. For high-impact decisions, compare 2–3 plausible alternatives, not cosmetic variants. Include the option to leave code alone. Describe each alternative's interface from the **caller's point of view** before discussing implementation. See `references/tradeoffs.md`.

Compare: caller burden, decision locality, information leakage, migration and testing risk, compatibility, performance, complexity added, and expected future change. Don't optimize hypothetical flexibility absent supporting evidence.

### 4. Recommend proportionately

- **Strong**: observed friction, clear improvement, bounded risk and verification.
- **Worth exploring**: credible issue but trade-off, scale, or impact needs validation.
- **Speculative**: possible issue without adequate evidence; normally do not recommend implementation.
- **Keep**: existing design is defensible or change costs outweigh benefits.

State the strongest counterargument, assumptions that could change the recommendation, and how to verify success. Rank by expected benefit × likelihood of change, adjusted for risk and effort; never invent numeric precision.

### 5. Execute only to the requested level

- **Design**: present the recommended contract/structure and decision rationale. Do not modify code without permission/request.
- **Review**: report findings, not architecture rewrites. A requested report may be HTML or Markdown; reports should not require CDN access to be legible.
- **Refactor**: when implementation is requested, first establish a passing baseline (or report why impossible), preserve behavior with characterization tests, make coherent incremental changes, run relevant checks and inspect diff. Report what was verified and what was not.

Never silently delete tests, break public interfaces, rewrite ADRs, introduce a new dependency, or widen scope. When the user has authorized substantial implementation, proceed within that authorization while clearly surfacing consequences.

## Output formats

**Design**: problem/constraints → existing or candidate contracts → alternatives and trade-offs → recommendation → tests and migration implications.

**Review**: summary of examined scope → prioritized findings with evidence and counterarguments → top next action (or no change) → limitations. The optional HTML format is in `references/reporting.md`.

**Refactor**: intended behavior/invariants → selected design and migration steps → modifications/tests → verification results → remaining risks.

Keep responses concise by default; expand when complexity warrants. Always clearly separate observed facts from proposed changes.

## Reference map

- `references/principles.md` — principles and applicability limits
- `references/red-flags.md` — concrete diagnostic tests and exceptions
- `references/design.md` — new design / interface workflow
- `references/review.md` — repo exploration and architecture audit
- `references/refactoring.md` — migration and implementation discipline
- `references/tradeoffs.md` — design alternatives and decision record
- `references/testing.md` — seams, adapters, test strategy
- `references/documentation.md` — interface docs, naming, comments
- `references/reporting.md` — Markdown/HTML reports
- `templates/architecture-report.html` — standalone, offline HTML scaffold
- `examples/sample-review.md` — example of appropriately qualified findings

## Intellectual provenance

Synthesized and adapted from Matt Pocock's `codebase-design` and `improve-codebase-architecture` skills and John Ousterhout's *A Philosophy of Software Design* (first edition), plus independently authored safety, evidence, and workflow guidance. This skill paraphrases ideas; it does **not** bundle or reproduce the book. See `README.md` and `SOURCES.md`.
