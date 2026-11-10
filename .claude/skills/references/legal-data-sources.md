# Legal Data Sources

Free APIs for legal research and citation verification. Use WebFetch to query these directly.

## Federal Regulations

**eCFR (Electronic Code of Federal Regulations)**
- Base URL: `https://www.ecfr.gov/api/versioner/v1/`
- No API key required
- Use for: Looking up any federal regulation by title, part, and section

**eCFR endpoint reference (verified 2026-04-07):**

1. **Get available dates for a part:** `versions/title-{N}?part={P}` — returns JSON with all amendment dates. Use the most recent date for subsequent calls.
2. **Get full regulation text:** `full/{DATE}/title-{N}.xml?part={P}` — returns XML for the entire part. **Must use a specific date from the versions endpoint, NOT `current`.** Only `.xml` format works (`.json` returns 406). No section-level filtering — fetch the whole part and parse for the section you need.
3. **Get structure/outline:** `structure/current/title-{N}.json` — returns JSON hierarchy of parts, subparts, and sections. `current` works here. Use this to verify a section exists before fetching the full part.

**Correct workflow:**
```
Step 1: GET versions/title-45?part=164 → find latest date (e.g., 2024-06-25)
Step 2: GET full/2024-06-25/title-45.xml?part=164 → full XML of Part 164
Step 3: Parse XML for the section you need (e.g., § 164.310)
```

**Common mistakes that return errors:**
- `full/current/...` → 404 (`current` not accepted on `full` endpoint)
- `full/{DATE}/...json` → 406 (`full` only returns XML)
- `full/{DATE}/...&section=164.310` → 406 (no section-level filtering)

- Docs: https://www.ecfr.gov/developers/documentation/api/v1 (note: docs page may be blocked by bot protection)

**Federal Register**
- Base URL: `https://www.federalregister.gov/api/v1/`
- No API key required
- Use for: Finding proposed rules, final rules, notices, and recent regulatory changes
- Example: `https://www.federalregister.gov/api/v1/documents.json?conditions[term]=telehealth&conditions[type][]=RULE`
- Docs: https://www.federalregister.gov/developers/documentation/api/v1

## Federal Statutes

**Congress.gov**
- Base URL: `https://api.congress.gov/v3/`
- API key required (free — register at api.congress.gov)
- Use for: Looking up federal bills, resolutions, amendments, and their status
- Docs: https://api.congress.gov/

**US Code (bulk)**
- URL: https://uscode.house.gov/download/download.shtml
- XML bulk download (not a REST API)
- Use for: Full text of federal statutes when you need the exact statutory language

## Case Law

**CourtListener (Free Law Project)**
- Base URL: `https://www.courtlistener.com/api/rest/v4/`
- API key required (free — register at courtlistener.com)
- Use for: Case law search (9M+ opinions), citation verification, finding enforcement actions
- Supports semantic search: add `semantic=true` to search queries for plain-language case law lookup
- 501(c)(3) nonprofit, means-based pricing, free for most use cases
- Docs: https://www.courtlistener.com/help/api/rest/

## Pending Legislation

**LegiScan**
- Base URL: `https://api.legiscan.com/?key=YOUR_KEY`
- API key required (free — register at legiscan.com)
- Free tier: 30,000 queries/month
- Use for: Tracking pending legislation in all 50 states + Congress, checking if laws are changing
- Docs: https://legiscan.com/legiscan
