# Red flags: hypothesis → evidence → exception

Use these as **questions**, not a linter or universal rule. For every proposed finding record: location, observed symptom, concrete change scenario, suspected underlying design decision, counterevidence, and confidence.

| Signal | Investigate / evidence | Counterevidence / when acceptable |
|---|---|---|
| Shallow module | Callers still perform the hard work, learn many methods, or traverse implementation | Adapter enforces meaningful security/protocol/instrumentation behavior |
| Information leakage | Same schema, lifecycle, invariant, or protocol rule embedded in multiple places | Cross-system protocol necessarily shared; generated schema/compiler checks enforce coordination |
| Temporal decomposition | Parse/validate/read/write split by step, yet all know the same format | Truly independent transformations or distinct team/deployment ownership |
| Pass-through functions | Several layers mirror the same signature and only forward | Explicit auth, translation, retry policy, observability, lifecycle, dispatch |
| Pass-through parameters | Many intermediate functions pass values they never use | Necessary explicit context is clearer/safer than hidden mutable/global state |
| Conjoined methods | Understanding either method requires reading both repeatedly | Small cohesive implementation deliberately colocated and easy to follow |
| Overexposure | Normal operation requires knobs/features relevant only to rare cases | Users have materially different requirements that cannot be inferred |
| Special/general mixture | Domain-specific condition embedded into otherwise reusable mechanism | A single product-specific module is not intended to be reusable |
| Repetition | Same *knowledge* and change obligation repeated across files | Similar code performs different domain functions; shared abstraction would obscure |
| Excessive exceptions | Every caller implements the same recovery/ignore logic | Failure must be actionable, observable, or transactionally significant |
| Ambiguous naming | Same identifier suggests distinct units or concepts | Local conventional names whose meaning is immediately visible |
| Hard-to-describe contract | Long list of preconditions or cross-module sequencing | Domain intrinsically complex; documentation honestly captures necessary behavior |
| Nonobvious behavior | Side effects, ownership, callbacks, or synchronization surprise readers | Necessary indirection with precise nearby contract docs |
| Comments restate code | Comment repeats the name/control flow and adds no semantics | Critical constraint restated intentionally to deter dangerous changes |
| Performance guesswork | Optimization justified by intuition or outdated benchmark | Known algorithmic blow-up with clear proof or strong workload data |

## Small diagnostic experiments

1. **Deletion test**: If the module disappeared, would its responsibility spread to many callers (earning its keep), or would an empty forwarding layer vanish? Trace all callers first.
2. **Plausible-change test**: Pick a likely product change. List *exact* locations and concepts that must change. Distinguish incidental file count from duplicated knowledge.
3. **Caller test**: Write one normal and one failure-path usage example from public declarations and documentation alone. Record unstated assumptions discovered by opening implementations.
4. **Ownership test**: For each invariant, data format, retry rule, or transaction boundary, name a single primary owner. If impossible, clarify where enforcement occurs.
5. **Error test**: Identify what a caller can do about each error; if nothing, ask whether behavior/handling could move downward. Never suppress meaningful errors.
6. **Alternative test**: Compare with **no refactor**, collapse/merge, targeted extraction, and interface redesign as applicable. At least one alternative must be structurally different.

## Confidence rubric

- **High**: concrete code and callers inspected; failure/change scenario reproduced, tests or history corroborate.
- **Medium**: credible coupling and trace, but no demonstrated maintenance impact or verification yet.
- **Low**: superficial pattern or inferred impact; investigate before recommending structural work.

Avoid numerical grades based on LOC, interface-to-implementation line ratios, number of classes, cyclomatic complexity, or dependency counts alone. Those can prioritize inspection but do not independently establish design quality.
