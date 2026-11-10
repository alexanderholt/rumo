# Rumo

An AI general counsel office for startups, implemented as Claude Code skills.

> Rumo is software, not a law firm, and not a substitute for the advice of an attorney. See [Disclaimer](#disclaimer).

Rumo answers your legal questions, maps your regulatory landscape, drafts your documents, and tracks your matters. It does the research and takes a position, and it tells you to call a lawyer only when you actually need one: litigation, a regulator at the door, a document only a lawyer can sign, or a high-stakes question that's still split after the research.

## Who it's for

Startup founders without in-house counsel. Rumo handles the day-to-day legal work a GC would, and when you do need outside counsel, you arrive with the analysis done and a specific question.

## How it works

Rumo is a set of Claude Code skills. Install it, run `/rumo`, and it walks you through onboarding: describe your company, upload your formation docs, and Rumo builds your legal profile with calibrated risk assessments and regulatory mapping.

After onboarding, use the specialist commands for specific tasks.

## Installation

Rumo stores your company's legal file (profile, matter log, attorney flags) inside `.claude/skills/`. Keep it out of git.

**Option A — use the Rumo folder as your legal workspace (simplest):**

```bash
git clone https://github.com/alexanderholt/rumo.git
cd rumo
claude          # start Claude Code here, then run /rumo
```

The repo's `.gitignore` already excludes your client file.

**Option B — add Rumo to an existing project:**

```bash
git clone https://github.com/alexanderholt/rumo.git /tmp/rumo
mkdir -p .claude/skills
cp -R /tmp/rumo/.claude/skills/* .claude/skills/
```

Then add these lines to your project's `.gitignore` **before** running `/rumo`:

```
.claude/skills/client-file/
.claude/skills/references/company-context.md
```

(`/rumo` checks for these entries during onboarding and adds them if missing, but add them yourself first.)

Claude Code discovers skills in `.claude/skills/` at the project root, so the `/commands` are available once you open the project.

## Commands

### Primary

| Command | What it does |
|---|---|
| `/rumo` | Start here. Onboarding, triage, complex questions that span domains. |
| `/regulatory` | Map your regulatory landscape. Federal, state, industry-specific. |
| `/corporate` | Cap tables, entity management, board governance, fundraising, founder agreements. |
| `/drafter` | Draft contracts, policies, employment docs, regulatory filings, memos. |
| `/compliance` | Structured compliance assessments against your regulatory landscape. |
| `/nda` | Screen an incoming NDA. GREEN (sign), YELLOW (sign after redlines), RED (don't sign as written). Writes the redlines. |
| `/playbook-export` | Generate a `legal.local.md` for use with [Anthropic's Legal Plugin](https://github.com/anthropics/knowledge-work-plugins/tree/main/legal). |

### Advisors (on-demand specialists)

| Command | What it does |
|---|---|
| `/expert` | On-demand domain expert — research, draft, analyze in any domain |
| `/expert-review` | Independent expert review of work product |
| `/outside-specialist` | Niche regulatory or legal domains where deeper expertise is needed |

### Quality layer (recommended by Rumo and the specialists, run in a fixed order)

| Agent | What it does |
|---|---|
| Verification | Checks citations for existence, accuracy, and currency (runs first) |
| Adversary | Red-teams analysis and drafts from the regulator's perspective |
| Defense | Argues the company's position against the Adversary's findings |
| GC Review | Senior GC calibration pass — confirms real risks, downgrades overrated ones |
| Voice Review | Catches AI writing patterns in drafts |
| Hedge Check | Strips needless disclaimers and counsel referrals; catches dodged answers and false certainty |

## How Rumo relates to Anthropic's Legal Plugin

[Anthropic's Legal Plugin](https://github.com/anthropics/knowledge-work-plugins/tree/main/legal) automates contract review and NDA triage for in-house legal teams that already have a playbook. Rumo builds that playbook from scratch.

The pipeline: Rumo builds your legal foundation (profile, regulatory map, documents, positions) and when you outgrow it, `/playbook-export` generates the `legal.local.md` file that feeds directly into Anthropic's plugin for operational contract review at scale.

## What's inside

```
.claude/skills/
  rumo/            — Orchestrator, onboarding, triage
  regulatory/      — Regulatory mapping and analysis
  corporate/       — Corporate, fundraising, equity
  drafter/         — Document drafting + templates/
  compliance/      — Compliance assessments
  nda/             — NDA triage (adapted from Anthropic's plugin, Apache 2.0)
  playbook-export/ — Generate legal.local.md for Anthropic's plugin
  adversary/       — Red team agent
  defense/         — Defense agent (paired with adversary)
  gc-review/       — Senior GC calibration
  verification/    — Citation verification
  voice-review/    — AI writing pattern detection
  hedge-check/     — Direct-answer gate
  expert/          — On-demand domain expert
  expert-review/   — Independent expert reviewer
  outside-specialist/ — Niche regulatory expertise
  references/      — Legal reasoning framework, templates, escalation rules
  client-file/     — (gitignored) Your company's proprietary data
```

## Key design decisions

- **Calibrate, don't catastrophize.** Risk ratings are based on enforcement history and industry norms, not theoretical worst cases. An expert review and GC review pipeline prevents one-directional risk inflation.
- **Orchestrate, don't replicate.** Rumo points you to Clerky, Carta, YC SAFEs, and standard form NDAs when a commoditized tool already exists. It focuses on work that requires legal judgment and company-specific context.
- **Answer the question.** Rumo researches, cites primary sources, and takes a position with its confidence stated. Uncertainty is a research task, not a reason to refer out. Outside counsel is recommended only for litigation or government action, acts only a lawyer can perform, or high-stakes questions still split after the research.
- **Profile-driven.** After onboarding, every agent reads your company profile. A privacy policy for a telehealth startup is fundamentally different from one for a SaaS tool — Rumo knows the difference.

## Disclaimer

**Rumo is software. It is not a law firm, it is not a lawyer, and it is not a substitute for the advice of an attorney.**

- **No practice of law.** The author is not a lawyer, is not licensed to practice law in any jurisdiction, and does not practice law. Publishing and distributing this software is not the practice of law, and the author does not review, supervise, or stand behind any output it produces for you.
- **No attorney-client relationship, no privilege.** Using Rumo, opening an issue, or contacting the author creates no attorney-client relationship with anyone. Your conversations with Rumo are not privileged or confidential communications with a lawyer, and could be discoverable in litigation.
- **Output can be wrong.** Rumo runs on a general-purpose AI model. It can misread facts, cite law that does not exist or no longer applies, and miss rules specific to your jurisdiction or industry. Laws change. Check anything you rely on against the primary source.
- **You are responsible.** You decide what to do with Rumo's output and you bear the consequences. Don't use it where the law requires a licensed attorney: representing you or anyone else in court or before an agency, or preparing documents for other people as a service.
- **Your data goes to your AI provider.** Rumo runs inside Claude Code. What you type and the files Rumo reads are sent to the model provider under your account's terms. Rumo also stores your legal file locally in plain text. Decide what you are comfortable sharing, and keep the client file out of version control (see Installation).
- **Not about any company.** The examples in these skills are illustrative. Nothing in this repository describes, or is advice to, any particular company, including the author's.
- **No warranty, no liability.** Provided "as is," without warranty of any kind, and the author is not liable for any claim or damages arising from its use, as set out in the [LICENSE](LICENSE) (and, for `/nda`, the Apache License 2.0).

## License

MIT. See [LICENSE](LICENSE).

The `/nda` skill is adapted from [Anthropic's Legal Plugin](https://github.com/anthropics/knowledge-work-plugins/tree/main/legal) and remains under the Apache License 2.0 (text in `.claude/skills/nda/LICENSE-APACHE-2.0.txt`); attribution and a summary of modifications are in that skill file.
