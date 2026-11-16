# Principles: complexity-first architecture

A principle is a lens for finding and evaluating possible improvements. None is an invariant to enforce regardless of context. The actual objective is maintainability under real use cases, with correctness and operational constraints intact.

## 1. Diagnose complexity by its effects

- **Change amplification:** Simple requirement causes edits in many places; identify the repeated decisions, not merely the files.
- **Cognitive load:** Maintainer must understand unrelated modules, implicit ordering, configuration, or hidden state.
- **Unknown unknowns:** The relevant code/constraints aren't discoverable from the obvious starting point; usually highest-priority design risk.
- Trace causes to unnecessary **dependencies** and **obscurity**. Some dependencies are essential; make them explicit and manageable.
- Complexity is *weighted by where developers work*. A complex rarely touched parser with a stable simple interface may be less costly than a tiny frequently edited orchestration function.

## 2. Deep modules and information hiding

- Prefer interfaces simple relative to the capability they provide; count **facts callers need**, not method lines.
- Place a design decision in the module best positioned to own it. Hide storage formats, retry bookkeeping, normalization, policy mechanics, and other details when callers do not need them.
- Do not hide facts callers must know: consistency guarantees, cancellation, security semantics, transactional boundaries, lifecycle ownership, latency limits, or actionable failures.
- The common case should be easy and safe by default. Avoid options exposed solely because the implementer doesn't want to choose defaults.
- A moderately general interface may be simpler than a cluster of task-specific operations, but build only the generality current use supports.

## 3. Distinct levels of abstraction

- Each level should earn its existence by translating or encapsulating important details.
- Pass-through functions, duplicate contracts, and chained wrappers warrant investigation, **not automatic deletion**. Useful exceptions include security enforcement, auditing, caching, protocol adaptation, dispatch, and meaningful policy.
- Avoid structuring modules solely by execution chronology when the same knowledge is required at different stages; seek knowledge ownership instead.
- Prefer moving unavoidable complexity into one suitable module rather than forcing every caller to handle it.

## 4. Cohesion: together or apart

Combine when modules share nontrivial knowledge, must change together, or a merged interface is materially simpler. Separate when independent decisions, lifecycles, change rates, ownership, or general-vs-specific policies justify it. Beware both excessive fragmentation and god modules.

Avoid extraction just to hit file/function length limits. A longer cohesive method may be clearer than several mutually dependent microfunctions. Conversely, a large method mixing independent responsibilities merits splitting.

## 5. Simplify semantics rather than conceal errors

Prefer operations with well-defined behavior over unnecessary exceptional paths (e.g., idempotent "ensure absent" rather than "delete only if present" when appropriate). Consolidate error translation where it belongs.

**Never discard important failure information.** Don't mask auth failures, partial commits, data corruption, lost messages, or safety-critical conditions merely to simplify callers. Retries require limits, idempotence analysis, cancellation, backoff, and observability.

## 6. Design alternatives and continual improvement

Sketch two or more substantively different interfaces when the architectural decision matters. Evaluate user-facing behavior, interface complexity, and how likely changes propagate. Improve existing designs incrementally during feature work, but avoid unrelated cleanups that jeopardize delivery.

## 7. Documentation, names, consistency

- Explain behavior and decisions unavailable from declarations: invariants, ownership, side effects, ordering, errors, tricky rationale.
- A contract too difficult to describe precisely may be poorly shaped.
- Precise, consistent names reduce mistaken assumptions; use conventions suited to the language and existing repo.
- Explain intent, not syntax. Keep docs close to code; avoid duplicating cross-module decisions.
- Follow existing conventions unless there is a strong, scoped reason to change them comprehensively.

## 8. Design and performance

Prefer naturally efficient algorithms and data layouts where simple. Measure before optimizing a claimed bottleneck. Preserve a baseline and representative workload; keep complex optimization only when benefits outweigh cost. Avoid assuming any particular call/alloc/network cost without measurement.

## 9. Testing as architecture feedback

Contract tests express externally observable promises; focused internal tests can protect difficult algorithms or corner cases. Seams should express meaningful variability and ownership, not just mockability. Choose realistic test doubles when possible, verify critical integration and failure behavior, and avoid brittle tests coupled to implementation details.

## Source map

Concepts drawn primarily from Ousterhout chapters 2–11, 13–18, 20; synthesis and test-seam vocabulary adapted from Matt Pocock's codebase-design materials. Rephrased for contemporary multi-language projects and with explicit exceptions.
