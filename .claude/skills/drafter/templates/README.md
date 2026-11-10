# Document Template Library

## External standard forms (check first)

Before using these internal templates, check `../references/external-template-sources.md` for open source standard forms from Common Paper, Bonterms, YC, NVCA, and others. These are battle-tested, committee-drafted agreements used in real transactions. Use them as the primary starting framework via the Open Agreements CLI:

```bash
npx -y open-agreements@0.10.2 list              # See all templates
npx -y open-agreements@0.10.2 fill <template> -o output.docx  # Generate filled DOCX
```

## Internal templates (regulatory overlays)

These internal templates define Rumo-specific structure: regulatory overlays, attorney flag insertion points, and company-context integration that external forms don't include. Use them to supplement external forms, not replace them.

## How the Document Drafter uses these

1. Check `external-template-sources.md` for an open source standard form for the document type
2. If one exists, use the external form as the primary framework
3. Read the internal template for regulatory overlay guidance and `[TAILOR]` / `[ATTORNEY REVIEW]` markers
4. Read the company legal profile and regulatory map to understand what's specific to this company
5. Produce a tailored draft that combines the standard form with company-specific regulatory overlays

## Templates available

| Template | When to use |
|---|---|
| `privacy-policy.md` | Any company that collects user data |
| `terms-of-service.md` | Any company with a web product or platform |
| `nda-mutual.md` | Pre-partnership or pre-investment discussions |
| `contractor-agreement.md` | Hiring independent contractors |
| `ciia.md` | Employee confidential information and invention assignment |
| `offer-letter.md` | Extending employment offers |
| `consulting-agreement.md` | Engaging consultants for advisory or project work |
| `board-consent.md` | Board approvals: option grants, officer appointments, fundraising authorization |
| `restricted-stock-agreement.md` | Founder/co-founder restricted stock with vesting and repurchase rights |

## Important

These templates are starting points. The Document Drafter must ALWAYS tailor them to the company's specific regulatory landscape and business context. A privacy policy for a telehealth company is fundamentally different from one for a SaaS analytics tool, even though the structure is similar.
