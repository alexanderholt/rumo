# External Template Sources

Standard legal form templates from established, vetted sources. The Document Drafter should use these as starting frameworks instead of drafting from scratch.

## How to use this file

Before drafting any document, check this file for an external source that covers the document type. Start from the external template and tailor it to the company's regulatory map and specific situation. The Drafter's value is in tailoring — not in reinventing standard forms.

## Open Agreements CLI

The fastest path for most documents. Bundles templates from Common Paper, Bonterms, YC, and NVCA (run `list` for the full current set). Generates filled DOCX files directly.

**Usage:**
```bash
# List all templates
npx -y open-agreements@0.10.2 list

# Fill a template
npx -y open-agreements@0.10.2 fill <template-name> --set "key=value" -o output.docx

# Fill from JSON
npx -y open-agreements@0.10.2 fill <template-name> -d values.json -o output.docx
```

**Available templates (36 listed here; the package may include more):**

| Template ID | Type | License |
|---|---|---|
| `common-paper-mutual-nda` | NDA (mutual) | CC BY 4.0 |
| `common-paper-one-way-nda` | NDA (one-way) | CC BY 4.0 |
| `bonterms-mutual-nda` | NDA (mutual, cover page style) | CC0 |
| `common-paper-cloud-service-agreement` | SaaS/Cloud agreement | CC BY 4.0 |
| `common-paper-csa-with-sla` | Cloud agreement + SLA | CC BY 4.0 |
| `common-paper-csa-with-ai` | Cloud agreement + AI terms | CC BY 4.0 |
| `common-paper-csa-click-through` | Click-through ToS | CC BY 4.0 |
| `common-paper-data-processing-agreement` | DPA | CC BY 4.0 |
| `common-paper-business-associate-agreement` | BAA (HIPAA) | CC BY 4.0 |
| `common-paper-professional-services-agreement` | PSA | CC BY 4.0 |
| `bonterms-professional-services-agreement` | PSA (cover page style) | CC0 |
| `common-paper-independent-contractor-agreement` | Contractor agreement | CC BY 4.0 |
| `common-paper-design-partner-agreement` | Design partner | CC BY 4.0 |
| `common-paper-pilot-agreement` | Pilot/trial agreement | CC BY 4.0 |
| `common-paper-software-license-agreement` | On-prem software license | CC BY 4.0 |
| `common-paper-partnership-agreement` | Referrals, co-marketing | CC BY 4.0 |
| `common-paper-ai-addendum` | AI data use, IP, risk | CC BY 4.0 |
| `common-paper-statement-of-work` | SOW | CC BY 4.0 |
| `common-paper-order-form` | Order form | CC BY 4.0 |
| `common-paper-amendment` | Contract amendment | CC BY 4.0 |
| `common-paper-letter-of-intent` | LOI | CC BY 4.0 |
| `common-paper-term-sheet` | Term sheet | CC BY 4.0 |
| `openagreements-employment-offer-letter` | Offer letter | CC BY 4.0 |
| `openagreements-employee-ip-inventions-assignment` | CIIAA / IP assignment | CC BY 4.0 |
| `openagreements-employment-confidentiality-acknowledgement` | Employee confidentiality | CC BY 4.0 |
| `yc-safe-valuation-cap` | SAFE (valuation cap) | CC BY-ND 4.0 |
| `yc-safe-discount` | SAFE (discount) | CC BY-ND 4.0 |
| `yc-safe-mfn` | SAFE (MFN) | CC BY-ND 4.0 |
| `yc-safe-pro-rata-side-letter` | SAFE side letter | CC BY-ND 4.0 |
| `nvca-stock-purchase-agreement` | Series A SPA | Proprietary (NVCA) |
| `nvca-investors-rights-agreement` | IRA | Proprietary (NVCA) |
| `nvca-voting-agreement` | Voting agreement | Proprietary (NVCA) |
| `nvca-rofr-co-sale-agreement` | ROFR/co-sale | Proprietary (NVCA) |
| `nvca-certificate-of-incorporation` | COI | Proprietary (NVCA) |
| `nvca-indemnification-agreement` | Indemnification | Proprietary (NVCA) |
| `nvca-management-rights-letter` | Management rights | Proprietary (NVCA) |

## Sources that cannot be automated (direct founders here)

These are high-quality but behind bot protection or login walls. The Drafter cannot fetch them. Direct the founder to these sites when the document type isn't covered by Open Agreements CLI or internal templates.

### Cooley GO (cooleygo.com/documents)
Best for: incorporation packages, consulting agreements, advisor agreements. Interactive web generator behind Cloudflare bot protection — cannot be accessed by headless browsers or CLI. Founders must use the site directly.

### GitHub BEIPA (github.com/github/balanced-employee-ip-agreement)
Employee-friendly alternative to traditional CIIAAs. CC0 (public domain). More balanced toward employees — lets them keep IP for personal projects. Use when the company wants a progressive IP assignment approach.

### Founder Institute FAST (fi.co/fast)
The standard advisor agreement. Checkbox-based equity tiers (0.15%–1.0%) across three company stages and three engagement levels. Free to use.

### Series Seed (github.com/CooleyLLP/seriesseed)
CC0 (public domain). Seed equity financing: stock purchase agreements, board/stockholder consents, accredited investor questionnaire, convertible promissory notes, term sheets.

### Open Source Site Policies
Real production policies, open sourced by major tech companies:
- **GitHub** (github.com/github/site-policy) — CC0. ToS, privacy, acceptable use, DMCA. Actively maintained (884+ commits).
- **Automattic/Legalmattic** (github.com/Automattic/legalmattic) — CC BY-SA 4.0. ToS, privacy, cookie policy, offer letters.
- **Basecamp** (github.com/basecamp/policies) — CC BY 4.0. ToS, privacy, SLA, cancellation, refund. Archived 2023; now at 37signals.com/policies.

## Document type → best source mapping

| Document Type | Automated (CLI) | Manual (direct founder) |
|---|---|---|
| NDA (mutual) | `common-paper-mutual-nda` | — |
| NDA (one-way) | `common-paper-one-way-nda` | — |
| Cloud/SaaS agreement | `common-paper-cloud-service-agreement` | — |
| Terms of Service | `common-paper-csa-click-through` | — |
| Privacy Policy | Internal template + regulatory map | GitHub/Automattic open policies |
| DPA | `common-paper-data-processing-agreement` | — |
| BAA | `common-paper-business-associate-agreement` | — |
| Contractor agreement | `common-paper-independent-contractor-agreement` | — |
| Consulting/PSA | `common-paper-professional-services-agreement` | — |
| Employment offer letter | `openagreements-employment-offer-letter` | — |
| CIIAA / IP assignment | `openagreements-employee-ip-inventions-assignment` | — |
| Employee-friendly IP agreement | — | GitHub BEIPA (github.com) |
| Advisor agreement | — | Founder Institute FAST (fi.co/fast) |
| Board consents | Internal template | — |
| Restricted stock agreement | Internal template | — |
| Incorporation package | — | Cooley GO / Stripe Atlas |
| Stock option plan | — | Cooley GO |
| 83(b) election | — | Cooley GO |
| Founder stock purchase | — | Cooley GO |
| SAFE | `yc-safe-*` | — |
| Series A financing | `nvca-*` (recipe) | — |
| SOW | `common-paper-statement-of-work` | — |
| AI addendum | `common-paper-ai-addendum` | — |

## Attribution requirements

- **CC BY 4.0** (Common Paper, Bonterms, Automattic): Must give credit. Include "Based on [Source] standard, licensed CC BY 4.0" in document metadata or footer.
- **CC0** (Series Seed, GitHub BEIPA, GitHub site-policy): No attribution required.
- **CC BY-ND 4.0** (YC SAFEs): Must give credit. Cannot distribute modified versions — fill in blanks only, do not alter standard terms.
- **CC BY-SA 4.0** (Automattic/Legalmattic): Must give credit. Derivative works must use the same license.
- **Proprietary** (NVCA via Open Agreements): Downloaded at runtime. Check NVCA terms before distribution.
