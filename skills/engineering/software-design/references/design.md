# Mode: Design a new module or interface

## Discover first

1. Clarify the caller and task. Who will invoke the module? What do they need done? Identify the most frequent use case and the non-negotiable exceptional cases.
2. Read the surrounding code and existing domain abstractions. Identify a suitable owner; prefer an existing module when it can deepen without mixing unrelated knowledge.
3. State interface-level facts: input/output semantics, invariants, side effects, lifecycle, persistence, concurrency, errors, cancellation, authorization, performance constraints.
4. Explore at least two genuinely different designs for decisions with meaningful downstream effects. A third may optimize for common-case ergonomics or operational constraints. Skip formal alternatives for trivial local code.

## Write the caller's contract first

Write a small pseudo-API or language-native sketch with normal and abnormal usage examples. Document *what callers may assume*, not implementation steps. Try to express core behavior in a short, precise paragraph. Difficulty describing it suggests design friction. Keep names aligned with the repository's domain language.

Test contract questions:

- Does normal usage require a sequence of calls, or could one cohesive operation own the sequence?
- Are callers required to know a storage format, normalization rule, exact retry count, or internal state transition they do not control?
- Is the module returning a representation that exposes internal mutable state?
- Are defaults safe and unsurprising? Are important failures visible?
- Could a meaningful alternative be implemented without caller changes? If not, is the variability genuinely needed?

## Design implementation ownership

Place implementation details behind the smallest practical public interface. Internal composition is fine. Avoid layering solely to satisfy style patterns. Separate generic mechanisms from business-specific policy only when the resulting interfaces remain simpler.

Categorize dependencies (in-process, local reproducible, owned remote, third-party external). See `testing.md`. Decide where operations can be atomic, where compensation/idempotence is needed, and where failures translate.

## Recommend

Compare alternatives on interface burden, locality, leakage, realism of use cases, migration risk, and testability. Include the case for not abstracting. Prefer the solution that best matches current needs and plausible changes, *not* maximum flexibility. Present high-impact assumptions and a concrete test plan.

## Design output sketch

- **Problem / context**: one paragraph.
- **Constraints**: essential invariants and compatibility.
- **Option A / B**: interface and example calls; what each hides; where each fails.
- **Choice**: why it lowers total complexity; strongest counterargument.
- **Validation**: observable contract tests, integration and failure-path checks.

## Optional parallel exploration

For unusually high-stakes decisions, parallel reviewers/agents may each receive the same constraints and distinct design goals (smallest public interface, fastest normal use, minimal deployment coupling). Require independent alternatives, concrete callers, and explicit trade-offs. Do **not** require sub-agent capabilities: a single agent can sketch alternatives sequentially.
