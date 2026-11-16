# Testing architecture: contracts, seams, adapters

## Contract-first testing

Test the behavior the interface promises: outputs, state transitions, durable effects, error semantics, ordering, performance when contractual. Prefer assertions that survive internal refactors. For critical paths, test failure behavior and invariants, not just happy paths.

**Do not delete all internal tests as a rule.** Internal algorithm tests, property tests, fuzzing, fault injection, and deterministic state-machine checks can expose defects contract tests cannot diagnose efficiently. Replace redundant tests only after mapping coverage and risk.

## Choose seams for a reason

A seam earns its cost if it provides meaningful substitutability, isolates volatile/inaccessible infrastructure, creates clear ownership, simplifies callers, or supports operational boundaries. Two production implementations, or production plus a realistic test implementation, are evidence of a useful seam but **not a required count**. A single adapter may still be worthwhile for a third-party system or domain boundary.

- Avoid defining an abstraction merely to mock every method in a class.
- Prefer dependencies supplied at composition boundaries; don't thread a context across dozens of irrelevant functions if a narrower scoped owner is possible.
- Avoid a globally mutable context as an accidental service locator. Where shared context is justified, document ownership and concurrency.
- Use results instead of side effects where it naturally clarifies behavior, but not at the expense of essential transaction/IO semantics.

## Dependency matrix

| Dependency | Preferred approach | Extra checks |
|---|---|---|
| Pure/in-process | Direct contract + property/algorithm tests | Edge cases and invariants |
| Local-substitutable, e.g., DB | Realistic local DB/container/in-memory equivalent | Constraints, transactions, query behavior |
| Owned remote | Port if useful; contract tests on both endpoints; in-memory adapter for logic tests | Schema versioning, network faults, ordering |
| External vendor | Injected client where valuable; stub for deterministic tests; sandbox/contract checks | Timeouts, retries, auth, rate limits, idempotency |
| Time/randomness/filesystem | Controlled source at narrow seam when needed | Determinism; lifetime; failure cleanup |

A fake that cannot reproduce critical database/network semantics must not be treated as proof that the production interaction works.

## Tests during refactors

1. Capture pre-refactor behavior with representative tests and fixture data.
2. Add contract-level tests before moving implementation if existing coverage is weak.
3. Preserve valuable targeted internal tests. Identify and remove only tests made truly redundant.
4. Migrate one slice at a time, validate adapters and integration boundaries.
5. Run regression suite and inspect whether the public contract stayed stable. Document gaps explicitly.

## Example test reasoning

A module that saves an order should be tested for persisted outcomes, duplicate submission behavior, validation, and error translation. It should *also* have focused tests for a complicated internal pricing algorithm if mathematical edge cases warrant them. Testing only a mocked `save()` invocation would not verify the actual contract.
