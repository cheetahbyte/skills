# Documentation and naming as design instruments

## Define contracts before bodies for significant modules

Draft a short interface-level description, signatures, and caller examples before implementing major new abstractions. Use the difficulty of describing the contract to detect missing ownership, ambiguous errors, or hidden sequencing. This is a design technique, not a requirement to comment every obvious line.

Interface docs should capture *only what callers need*:

- Meaning of inputs and outputs, units, inclusive/exclusive bounds.
- State/ownership/resource lifecycle, mutation and side effects.
- Preconditions, invariants, ordering, thread/concurrency guarantees.
- Error behavior and actionable recovery; cancellation, retries and transactional guarantees where pertinent.
- Performance properties only if callers need to rely on them.

Implementation docs explain *why* a nonobvious choice exists, not each syntactic action. Avoid comments that merely mirror code. Prefer concise paragraphs near declarations and code paths; link one canonical description for cross-module invariant or ADR.

## Names are part of the contract

Prefer precise names that distinguish different concepts and units (`logicalBlock` versus `diskBlock`), and use them consistently. A widely scoped value needs enough context to remain clear; a tiny loop variable can be short. Follow the language idiom and existing repo conventions when they keep meaning obvious.

When a concept cannot be named cleanly, investigate whether it holds unrelated responsibilities. Do not solve a bad abstraction with an ever-longer identifier.

## Documentation smell tests

- Does reading the interface require opening its implementation?
- Does documentation include internals that callers should not need?
- Does a contract need pages of exceptions or choreography? Could semantics simplify it?
- Are comments copied across call sites and becoming inconsistent?
- Are cross-module invariants discoverable at a natural starting point?
- Would a fresh maintainer interpret this name/contract correctly?

## Changes to existing code

Keep nearby docs in sync with modified behavior, update the diffs, and avoid duplicated rationale. A commit message is not an adequate substitute for discoverable code comments/architecture notes when the decision will matter to future maintainers.

## Avoid dogma

Neither a blanket "self-documenting code needs zero comments" rule nor a blanket "comment every function" rule is reliable. Optimize for information readers cannot otherwise readily infer. A concise, precise contract can be more important than abundant inline comments.
