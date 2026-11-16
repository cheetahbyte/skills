# Architecture reporting

## Default: Markdown

Use a short, readable review unless a visual report is requested or would materially improve the decision. Quote concrete paths and symbols from inspected code; no fabricated excerpts. Include observed scope and missing evidence.

Suggested organization:

1. **Scope and limits**: repository, flows/files/docs actually inspected; availability of history/tests.
2. **Decision summary**: top finding or a justified no-change outcome.
3. **Findings**: each has strength, confidence, location, evidence, impact mechanism, proposal, strongest counterargument, risk, verification.
4. **Next action**: smallest valuable investigation/design/refactor step.

## Optional HTML

Use `templates/architecture-report.html` as an offline-capable single file with embedded CSS and SVG. Replace placeholder data with **verified** observations. Encode user/repository-supplied strings for HTML and avoid injecting untrusted arbitrary HTML. No external CDN dependency required; diagrams should render offline.

Good diagrams reflect the actual shape:

- Call graph: where coordination leaks or unnecessary forwarding occurs.
- Before/after ownership: which decision moves into which module.
- Sequence: contract or network semantics (no invented latency numbers).
- Dependency matrix: cross-module invariant and ownership.

Every diagram needs a text alternative summarizing what it shows. Avoid decorative charts and visualization that falsely implies measurement. A diagram can be omitted if its relationships cannot be established.

## Per-finding fields

- Title; recommendation: `Strong`, `Worth exploring`, `Speculative`, or `Keep`.
- Confidence: high/medium/low, with evidence gaps.
- Evidence: paths + methods + observed behavior; link/reference if supported.
- Diagnosis: source of change amplification/cognitive load/unknown unknowns.
- Proposed alternative: exact ownership/interface effect, or next investigation.
- Counterargument: why the current design may be appropriate.
- Validation: tests, example changes, measurements, or deployment checks.

Avoid an unsupported numeric 'architecture score'. A prioritized assessment is more credible than arbitrary percentages. Never imply a candidate has been accepted or implemented merely because it appears in a report.
