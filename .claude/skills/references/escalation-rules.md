# Escalation Rules

## When any specialist agent must escalate to Rumo

These triggers are codified, not left to judgment. If any of these conditions are met, escalate.

1. **Cross-domain question** — The question touches another specialist's domain
2. **Genuine legal ambiguity** — The answer could reasonably go either way
3. **Unclear regulatory landscape** — The applicable regulations are unclear or conflicting
4. **Material risk change** — The finding materially changes the company's risk profile
5. **Scope creep** — The task grew more complex than initially scoped
6. **Multi-jurisdictional conflict** — State laws conflict with each other or with federal law
7. **Conflicting obligations** — Different legal requirements point in opposite directions (e.g., employment law says X, investor agreement says Y)
8. **Risk threshold breach** — The issue could result in litigation, regulatory action, or deal failure (also check whether it meets the bar for outside counsel)
9. **No precedent found** — Legal Research & Verification Agent finds no clear precedent
10. **Active disputes** — Anything touching active disputes or threatened litigation

## How to escalate

Escalate by dispatching `/rumo` with the Skill tool (see "How to dispatch" in [agent-roster.md](agent-roster.md)), or, if you were invoked directly by the founder, by telling the founder to take it to `/rumo`. Either way, state:
1. What the original question was
2. Which trigger was hit
3. What you've determined so far
4. What you need Rumo to resolve

## Lateral handoffs

Not everything needs to go up. When a specialist needs input from another specialist on a routine matter, they can hand off directly, using the Skill tool as described in "How to dispatch" in [agent-roster.md](agent-roster.md). Rumo should be aware but doesn't need to orchestrate every handoff. Examples:
- Document Drafter needs state-specific regulatory input → asks Regulatory Analyst directly
- Corporate & Fundraising Analyst needs a document drafted → hands off to Document Drafter directly

Escalate to Rumo when the handoff reveals unexpected complexity.
