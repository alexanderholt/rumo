# Attorney Flag Format

An attorney flag marks a question that needs outside counsel. Flags are rare: Rumo answers most questions itself. A flag is warranted only when the question meets the bar in "When a lawyer is actually needed" in [legal-reasoning-framework.md](legal-reasoning-framework.md). Every flag must be specific, substantive, and actionable, and must include Rumo's best answer so far.

## Inline format (used within documents and memos)

> **[ATTORNEY FLAG]** [One-sentence description of the issue]. [Which bar it meets: litigation/government action, lawyer's act required, or high-stakes and still split after research]. [Rumo's best answer and why]. [The specific question for the lawyer, and the specialty to look for].

### Example

> **[ATTORNEY FLAG]** The company received an OCR data request about a reported breach. This is a government inquiry, so it meets the bar. Rumo's read: the company is a business associate, not a covered entity (45 CFR § 160.103), so the 60-day notice clock runs to the covered entity, not to patients. Ask a HIPAA enforcement lawyer to confirm that position and handle the OCR response.

## Attorney Flag Register format (consolidated list)

| ID | Date | Matter | Source | Issue | Severity | Priority | Status |
|----|------|--------|--------|-------|----------|----------|--------|
| ATF-001 | 2026-04-05 | MTR-002 | Regulatory memo | OCR data request on reported breach | High | Now | Open |

This file is the canonical definition of flag IDs, severity, priority, and status. Every other skill uses these scales.

Severity is how bad it is if wrong. Priority is when it needs an answer. Keep them separate: a High-severity issue on a feature that is not being built yet is Parked, not Low.

### Priority levels
- **Now** — blocks current work
- **Before launch** — must be resolved before the affected feature ships
- **Parked** — only relevant if a future feature is built

### Severity levels
Severity reflects probability AND magnitude, consistent with the risk calibration test in [legal-reasoning-framework.md](legal-reasoning-framework.md):
- **Critical** — High probability and high magnitude: active enforcement, clear violation, material consequences if wrong. You can point to an enforcement action or lawsuit against a similar company.
- **High** — High probability or high magnitude, not both. Genuine legal ambiguity that affects business operations or product design, often with a recent enforcement trend.
- **Medium** — Theoretical risk with limited enforcement history, or manageable consequences even if it materializes.
- **Low** — No enforcement history, standard industry practice, minor impact.
- **Confirm and move on** — Not a substantive risk; a quick check of an assumption. Rumo runs it itself and closes the flag.

### Status values
- **Open** — Needs attorney review
- **Sent to attorney** — Shared with counsel, awaiting response
- **Resolved** — Attorney has reviewed and provided guidance
- **Downgraded** — Calibration (e.g., GC Review) lowered the severity; record the old and new rating and why
- **Withdrawn** — Calibration found it is not a real issue; keep the row with a one-line reason instead of deleting it

## When to generate a flag

Generate an attorney flag only when one of these is true:
- **Litigation or government action:** a lawsuit filed or threatened, a demand letter with real exposure, a subpoena, a regulator inquiry or investigation
- **A lawyer's act is required:** a court appearance, a formal opinion letter, an attorney-signed filing, closing a priced equity round
- **Still split after the work, at high stakes:** Rumo researched it and ran Adversary/Defense, the question is genuinely contestable, and being wrong is Critical or High severity

Do NOT generate a flag for:
- Routine disclaimers ("consult an attorney")
- Ambiguity Rumo hasn't researched yet. Research it first
- Questions Rumo can answer with a stated confidence level, even if the answer is a judgment call
- Assumptions Rumo can check by reading the statute
- Questions that can be resolved with additional factual information from the founder
