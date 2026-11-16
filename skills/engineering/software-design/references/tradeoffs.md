# Trade-offs and design-it-twice process

## When alternatives matter

Use explicit comparison for cross-module contracts, new data ownership, dependencies, deployment boundaries, public APIs, and costly refactors. Trivial fixes usually don't warrant three designs or heavyweight ceremony.

## Generate meaningful alternatives

Pick competing **architectural hypotheses**, not variations in naming:

- **Keep/clarify:** retain structure, improve interface documentation or discoverability.
- **Consolidate:** move shared knowledge behind an existing owning module; remove redundant calls.
- **Extract:** introduce a dedicated module for one repeated decision with a simpler interface.
- **Rethink semantics:** remove unnecessary state/ordering/error cases by changing operation meaning if compatible.
- **Ports/adapters:** isolate an external dependency or genuine variability; check whether the seam pays for itself.

Use at least two alternatives when justified; include current design as a baseline. For major decisions, try radically different approaches before recombining strong parts.

## Comparison questions

| Dimension | Question |
|---|---|
| Interface burden | How many concepts, sequencing rules, exceptions, configuration knobs do callers need? |
| Locality | How many owners must coordinate a plausible feature or fix? |
| Leakage | Where does implementation knowledge cross module interfaces? |
| Cohesion | Are responsibilities grouped by decision ownership or arbitrary step/order? |
| Correctness | Which invariants become easier to state and enforce? |
| Testability | Can observable contracts be verified without duplicating implementation? |
| Deployment | Do distributed ownership, consistency, and backward compatibility constrain design? |
| Performance | What is known, assumed, or measured about relevant hot paths? |
| Reversibility | Can the choice be changed cheaply when needs evolve? |
| Cost | How much code churn, dependency change, migration, and operational risk? |

Avoid fabricated weighted score totals or false numerical precision. If priorities are unclear, explain the trade-off and what evidence would decide it.

## Counterfactual / falsification

For every recommended refactor ask:

1. What concrete change becomes easier afterward?
2. Could we obtain 80% of that benefit without restructuring (documentation, test, naming, tooling)?
3. Where could this proposal make life worse (more indirection, larger blast radius, weaker failure visibility)?
4. What would change our recommendation? E.g., no expected new callers, proven perf regression, a hidden security boundary, a required external compatibility contract.

## Small ADR-style decision note

```
Context: [why this decision is needed]
Constraints: [must stay true]
Options: [A/B including keep]
Decision: [choice and rationale]
Consequences: [benefits and costs]
Verification: [tests or measurable observations]
Revisit when: [trigger that would make this decision stale]
```

Do not create or modify official ADRs without appropriate authorization. Link existing ADRs and flag conflicts rather than ignoring them.
