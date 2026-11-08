---
name: writing-specs
description: "Turn the feature discussed in this conversation into a design spec saved in the repo, ready for a fresh-context review and an implementation plan."
disable-model-invocation: true
---

# Writing specs

A spec records what will be built and why, as decided in this conversation. Its readers never saw the conversation: a goldfish reviewer that checks it against the code, then `writing-plans`, which turns it into tasks. Whatever lives only in the chat is lost to both, so the spec carries every **decision** with its reason.

A spec decides _what_ and _why_. Task order, steps, and function bodies belong to the plan.

Synthesize what was already discussed. The user interviewed themselves by discussing the feature; ask only the questions in steps 3 and 4.

## 1. Collect the decisions

Go through the whole conversation and list:

- every decision, with the reason the user or you gave;
- every alternative that was rejected, with the reason;
- every question still open, including ones you answered for yourself without the user confirming.

Done when: each decision has a reason, and nothing you assumed is filed as decided.

## 2. Ground it in the code

Read the modules the feature touches and the project's own vocabulary: a glossary, existing designs or ADRs, `AGENTS.md`. Then find **prior art**: how the codebase already solves the same concern elsewhere (how other secrets are stored, how other settings reach the UI, how other jobs report progress). A spec that ignores prior art reinvents it or contradicts it.

Done when: every module the spec names exists at the path you give, or is marked new, and each concern the feature shares with existing code names the code that already handles it.

## 3. Agree the testing seams

Propose where the feature will be tested: the highest seam that exercises the behavior, preferring seams that already exist and as few as possible. Ask the user to confirm them in one message, together with any conflict step 2 found between a decision and the code.

## 4. Write the spec

Save it where the project keeps designs (look for `docs/designs/`, `docs/specs/`, or similar); otherwise `docs/designs/<feature>.md`. Use the project's terms throughout. Write each section from the template below and leave out any that has nothing to say, except Open questions.

Name modules and files by path so a reviewer can find them; leave out line numbers and code, which go stale. The exception is a type, schema, or state machine that states a decision more precisely than prose.

Done when: the file exists and every item from step 1 appears in it.

## 5. Check and hand off

Reread the spec as someone who missed the conversation and fix it inline:

1. **Coverage:** every decision, rejected alternative, and open question from step 1 is in the spec.
2. **Standalone:** no sentence relies on the chat ("as discussed", "the approach above", "option B").
3. **Altitude:** no task lists, step orders, or function bodies.

Then give the user the path, the number of open questions, and the next step: a fresh review with `@spec-review <path>`, then `writing-plans` once the findings are settled.

## Template

```markdown
# <Feature>

**Status:** draft

## Problem

What the user cannot do today, or what goes wrong, from their point of view.

## Solution

What changes for the user, in a few sentences.

## Behavior

Numbered scenarios, one per distinct behavior: the trigger, then the observable result. Include failures, empty states, permissions, and what happens to existing data. Merge scenarios that only differ in wording.

## Decisions

One line per decision with its reason. Rejected alternatives go here as well, each with the reason it lost.

## Interfaces and data

API contract changes, events, schema and migrations, configuration, and settings, each with its compatibility impact.

## Affected code

Each module by path, with what changes there. Mark new modules as new. Name the prior art each one follows.

## Testing

The agreed seams, what each one proves, and the existing tests to model them on.

## Out of scope

What a reasonable implementer might add but must not.

## Open questions

What is undecided, and who decides it. Write "None" when nothing is open.
```
