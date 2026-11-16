# Sources and attribution

This skill is an independently worded synthesis of these materials:

1. Matt Pocock, [`codebase-design`](https://github.com/mattpocock/skills/tree/main/skills/engineering/codebase-design), including `SKILL.md`, `DEEPENING.md`, and `DESIGN-IT-TWICE.md`, accessed 2026-11-16.
2. Matt Pocock, [`improve-codebase-architecture`](https://github.com/mattpocock/skills/tree/main/skills/engineering/improve-codebase-architecture), including `SKILL.md` and `HTML-REPORT.md`, accessed 2026-11-16.
3. John Ousterhout, *A Philosophy of Software Design*, first edition, Yaknyam Press (2018; uploaded copy), especially chapters 2–11, 13–18, 20 and the closing design-principles/red-flags summaries.
## Explicit adaptations and disagreements

- Treat 'one adapter = hypothetical seam, two = real' as a useful warning, not a hard law.
- Do not indiscriminately delete lower-level tests after adding deep-module interface tests.
- Do not mandate a bespoke architectural vocabulary where established project/domain terms are clearer.
- Do not make sub-agent availability, a graphical report, or external network/CDNs prerequisites for a useful review.
- Require claims with concrete supporting evidence and offer a reason *not* to change the design.
- Treat performance and error-handling simplifications conservatively where correctness and availability depend on them.
