# Mode: Safe architectural refactoring

## Before changing code

- Establish baseline: working tree state, tests, typecheck/lint/build where relevant. If red already, identify failures preexisting versus change-induced.
- Identify entry points, all relevant callers (including tests, scripts, external consumers), user-visible behavior, invariants, feature flags, schema and transport contracts.
- Confirm scope and user authorization. An architecture review request is **not** implementation permission.
- State the desired interface and the exact knowledge that will move behind it. Compare with leaving it unchanged.

## Plan by risk

1. **Characterize behavior** at the public interface and at critical boundaries. Include success, failure, retries, cancellation, authorization, transactionality, resource cleanup, race conditions, and edge cases as applicable.
2. **Introduce new structure incrementally** behind stable interfaces where practical. Avoid big-bang rewrites. Track temporary adapters and removal conditions.
3. **Migrate callers coherently**, ideally in small verified slices. Consider dual-read/write, compatibility shims, expand-contract migrations, release ordering, and deployment coordination for distributed systems.
4. **Remove obsolete indirection** once callers have migrated. Only remove tests when the replacement tests adequately preserve their behavioral/invariant coverage.
5. **Validate** with relevant tests, static checks, builds, benchmarks when justified, and a final diff review including docs and migration notes.

## Dependency ownership

- In-process logic: combine when it improves locality; avoid inventing a port just for a mock.
- Local-reproducible externalities: prefer representative in-memory/local implementations for integration tests where reliable.
- Owned remote boundaries: test contract, transport, and failure semantics; ports/adapters can be justified by genuinely different deployment/test behaviors.
- Third-party systems: isolate vendor-specific details where it reduces leakage; test normal + failure cases and use contract/sandbox testing as appropriate.

See `testing.md` for seam trade-offs.

## Special hazards

- **Semantics:** don't turn rejected operations into silent success or mask important failures to simplify exceptions.
- **Performance:** protect throughput/latency characteristics when they are part of the existing contract; benchmark the appropriate workload.
- **Data:** migration, backfill, rollback, schema constraints, retry idempotence, and partial failures need explicit treatment.
- **Concurrency:** preserve ordering, cancellation, exactly/at-least-once behavior, and ownership; do not infer safety from a passing unit test.
- **External interfaces:** identify compatibility guarantees before removing parameters/endpoints/events.
- **Docs:** update interface comments, examples, ADRs only when authorized, and links to shared design constraints.

## Completion report

- What changed and the intended ownership improvement.
- What was held constant and how you checked it.
- Tests/checks run with actual outcomes; don't claim unexecuted checks passed.
- Remaining migration steps/known risks and any unverified assumptions.
- Whether the result demonstrably simplifies callers and concentrates knowledge.
