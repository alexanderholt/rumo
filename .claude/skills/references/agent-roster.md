# Rumo — Agent Roster

## Model recommendation

**Use Claude Opus** for all substantive legal work. The agents require complex multi-step reasoning (IRAC analysis, statutory construction, adversarial thinking), reliable procedural compliance (matter management, attorney flag triple-write), and calibrated confidence (knowing which questions are settled and which are genuinely open). Opus is meaningfully better at all three.

| Tier | Agents | Why Opus matters |
|---|---|---|
| **Opus strongly recommended** | Rumo, Regulatory, Corporate, Compliance, Adversary, Defense, GC Review, Outside Specialist | Complex reasoning, legal judgment calls, calibration |
| **Opus recommended** | Drafter, Verification | Statutory precision, citation accuracy |
| **Sonnet acceptable** | Voice Review, Hedge Check | Pattern matching tasks with shorter prompts |

## Primary agents

| Command | Role | When to use |
|---|---|---|
| `/rumo` | Orchestrator, onboarding, triage, complex multi-domain questions | Starting point for new companies. Complex questions that span domains. Escalation endpoint. |
| `/regulatory` | Regulatory Analyst | Regulatory mapping, memos, ongoing regulatory Q&A, data privacy landscape |
| `/corporate` | Corporate & Fundraising Analyst | Cap tables, entity management, board governance, fundraising, founder agreements, employment classification, IP triage |
| `/drafter` | Document Drafter | Contracts, employment docs, regulatory filings, internal policies, memos |
| `/compliance` | Compliance Reviewer | Structured compliance assessments against regulatory landscape |
| `/nda` | NDA Triage Specialist | Screen incoming NDAs — GREEN (sign), YELLOW (sign after redlines), RED (don't sign as written). Profile-aware. |
| `/playbook-export` | Playbook Generator | Generate `legal.local.md` from Rumo profile for use with Anthropic's Legal Plugin |

## Cross-cutting agents (quality layer)

These run in the canonical order defined in `rumo/SKILL.md` (Verification → Adversary → Defense → GC Review → Voice Review → Hedge Check). Rumo and the specialists recommend them by output type; they run when an agent dispatches them (see "How to dispatch") or the founder invokes them.

| Agent | Role | Dispatched by |
|---|---|---|
| Legal Research & Verification | Citation verification (existence, accuracy, currency) + case law research | Any agent, on work product that cites authority |
| Adversary | Red team — attacks analysis from opposing/regulator perspective | Rumo or a specialist, on analysis and drafts |
| Defense | Argues the company's position against Adversary findings. Finds defenses, favorable precedents, and reasons risks are manageable. Paired with Adversary. | Rumo, after Adversary review |
| GC Review | Senior GC calibration pass. Reviews full legal profile for overrated risks, confirms real ones, tells the founder what actually matters. | Rumo, after expert review or as final quality gate |
| Voice & Authenticity Reviewer | Catches AI writing patterns in drafts | Rumo or the Document Drafter, when the quality pipeline for a draft is run |
| Outside Specialist | On-demand domain expert for niche areas | Rumo or a specialist, including when the Adversary lists "Specialist needed" |
| Hedge Check | Strips needless disclaimers and counsel referrals; catches dodged answers and false certainty | Rumo, as the final step on output the founder will read |

## How to dispatch

There are two different things, and each skill should use the right one:

1. **Dispatching an agent (agent-to-agent).** Invoke the target skill with the Skill tool. Forked skills do not see the conversation, so pass everything they need in the arguments: the full work product (or the file path to it), the matter ID if one exists, and any prior review output **verbatim** (for example, Defense needs the full Adversary review). The result comes back to the caller. Quality agents have read-only tools, so **the caller records the results** in the matter log, attorney flag register, matter index, and legal profile.
2. **Routing the founder (user-facing).** "Tell the founder to run `/x`" is only for sending the founder to a specialist for their next question. It is not a way to hand off work between agents.

When a skill says "dispatch," "hand off," "escalate to," or "asks [agent] directly," it means option 1.

## Orchestrate, don't replicate

Where free or low-cost tools already solve a problem well, direct the founder to those tools:
- **Company formation:** Clerky, Stripe Atlas
- **Cap table management:** Carta, Pulley
- **Standard SAFEs:** YC standard SAFE templates
- **Standard NDAs:** Standard form NDAs
- **Operational contract review at scale:** Anthropic's Legal Plugin (use `/playbook-export` to generate the playbook)

Rumo drafts, analyzes, and answers where legal judgment and company-specific context are required.
