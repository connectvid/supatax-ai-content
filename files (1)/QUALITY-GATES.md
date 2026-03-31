# QUALITY-GATES.md
## Hard-Stop Quality Rules — No Page Gets Published Without Passing All Gates

These are binary PASS/FAIL checks. A single FAIL = the page does not publish. No exceptions.

---

## HOW TO USE THIS FILE

Before marking any page as `done` in 04-publishing-schedule.csv, run through every gate in the appropriate section. If all gates pass, change status to `ready-to-publish`. If any gate fails, mark `needs-revision` and fix the specific failure.

Claude Code must run this checklist automatically after generating each page's content. Output a checklist result block at the end of every piece of content.

---

## GATE GROUP 1: STRUCTURE (Every page type)

### G1-A: Word Count
- Q&A pages: **400–750 words** (no padding, no cutting essential info)
- Pillar guides: **2,000–3,500 words**
- Short companion pages (see notes column in CSV): **350–500 words**
- ❌ FAIL if: under minimum OR over maximum
- Why: Under = thin content, Google won't trust it. Over = signals padding, hurts IGS.

### G1-B: H1 Contains Target Keyword
- The H1 must contain the exact target keyword OR a grammatically natural near-exact variant
- ❌ FAIL if: H1 is a generic marketing phrase with no keyword
- ❌ FAIL if: H1 is the same as another page on the site
- ✅ PASS examples:
  - Target: "is homeowners insurance tax deductible" → H1: "Is Homeowners Insurance Tax Deductible?"
  - Target: "backup withholding" → H1: "Backup Withholding: What It Is and How to Stop It"
- ❌ FAIL examples:
  - Target: "backup withholding" → H1: "Everything You Need to Know About Withholding"

### G1-C: Heading Count
- Q&A pages: minimum 3 H2s, maximum 7 H2s
- Guides: minimum 6 H2s, maximum 12 H2s
- ❌ FAIL if: fewer than minimum (thin structure)
- ❌ FAIL if: more than maximum (over-engineered, padded)
- No heading may use marketing language ("Everything You Need to Know", "Ultimate Guide", "Complete Overview")

### G1-D: No Skipped Heading Levels
- H1 → H2 → H3 (never H1 → H3 directly)
- ❌ FAIL if: H3 appears without a preceding H2

### G1-E: No Preamble in First Paragraph
- First paragraph must answer the core question within the first 2 sentences
- ❌ FAIL if: first sentence is any of these patterns:
  - "In this article, we will..."
  - "Have you ever wondered..."
  - "When it comes to taxes..."
  - "Tax season can be..."
  - "Great question!"
  - Any sentence that doesn't contain the direct answer

---

## GATE GROUP 2: CONTENT QUALITY (Every page type)

### G2-A: IRS Form Reference
- Every page about a tax rule, deduction, or IRS process must name the specific IRS form
- ✅ Required when applicable: Form 1040, Schedule A, Schedule C, Schedule E, W-9, W-4, 1099-NEC, Form 4868, Form 8332, Form 706, Form 843, etc.
- ❌ FAIL if: page discusses "claiming a deduction" without naming which form/line
- Exception: purely definitional pages (e.g., "what is a tax strategist") do not require a form reference

### G2-B: Tax Year Specificity
- Every page must reference the 2025 or 2026 tax year explicitly
- ❌ FAIL if: page contains only generic statements with no year
- ✅ PASS examples: "In 2025, the backup withholding rate is 24%"
- ❌ FAIL examples: "The IRS requires a flat withholding rate..."

### G2-C: Specific Rate / Dollar / Percentage / Threshold
- Every financial page must contain at least one specific number
- ✅ PASS examples: "24% flat rate", "$23,500 contribution limit", "7.5% AGI threshold", "15-year MACRS class life"
- ❌ FAIL if: page only says "a percentage of your income" without specifying what percentage
- Exception: Pages about California/state taxes where amounts are ranges — include the range

### G2-D: State-Specific Note
- Every page where state rules differ must include a state-specific callout
- Minimum: ONE sentence noting where a state differs from federal rules
- Priority states for callouts: California, New York, Texas, Florida, Pennsylvania
- ❌ FAIL if: page about a federal deduction never mentions that states may differ
- Exception: Pages that are already state-specific (e.g., California Capital Gains Tax) don't need additional state notes

### G2-E: Information Gain Score Check
Before publishing, ask: "Does this page contain at least ONE thing that TaxGPT's equivalent page does NOT have?"
Options for exceeding TaxGPT:
- 2025/2026 tax year data (they often have 2023/2024)
- A specific calculation example with real numbers
- A state-specific rule they don't mention
- An edge case or exception they miss
- The specific IRS form line number
- A "what to do next" action step
- ❌ FAIL if: the page contains nothing a user couldn't find on TaxGPT's equivalent page
- ✅ Mark which specific element provides the Information Gain at the end of the content block

---

## GATE GROUP 3: INTERNAL LINKS (Every page type)

### G3-A: Exactly 3 I-Node Links in Q&A Pages
- Q&A pages must contain exactly 3 contextual body links
- ❌ FAIL if: fewer than 3 links (missed internal equity)
- ❌ FAIL if: more than 3 links (dilutes PageRank per link)
- Exception: Short companion pages (marked in CSV notes) may have 2 links

### G3-B: Guides Must Have 4–6 I-Node Links
- Pillar guides must contain 4–6 contextual body links
- ❌ FAIL if: fewer than 4 or more than 6

### G3-C: All Link Slugs Are Valid
- Every internal link slug must match an exact entry in 01-pages-master.csv or 01b-pages-expansion.csv
- ❌ FAIL if: any link points to a slug not in the master list
- Why: prevents dead links, ensures crawl path integrity

### G3-D: Anchor Text is Near-Exact Match of Destination Keyword
- ✅ PASS: destination target keyword = "is home insurance tax deductible" → anchor: "is home insurance tax deductible" or "home insurance is not tax deductible"
- ❌ FAIL: anchor = "click here", "learn more", "read this article", "find out"
- ❌ FAIL: anchor is vague (e.g., "this page", "our guide")

### G3-E: Annotation Text Reinforces the Semantic Connection
- The sentence containing the link must contextually explain WHY the destination is relevant
- ✅ PASS: "If you're also wondering about other property costs, our answer on [whether closing costs are tax deductible](/tax-answers/are-closing-costs-tax-deductible/) covers each settlement line item separately."
- ❌ FAIL: "For more information, see [are closing costs tax deductible](/tax-answers/are-closing-costs-tax-deductible/)."

### G3-F: Stay Within Topical Borders
- Zero links to non-tax content from /tax-answers/ or /guides/ pages
- ❌ FAIL IMMEDIATELY: any link to off-topic content (non-tax tools, unrelated services)

### G3-G: Back-Links Added After Publishing
- After publishing a page, IMMEDIATELY update 2 existing pages to add links TO the new page
- Check the `internal_links_from` column in 01-pages-master.csv
- ❌ This step is not optional — it must happen within 24 hours of publishing
- Mark in the CSV: add note "backlinks-added: [date]"

---

## GATE GROUP 4: SCHEMA (Every page type)

### G4-A: FAQPage Schema Present on Q&A Pages
```json
{
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "[H1 as question]",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "[First paragraph — plain text, no HTML]"
    }
  }]
}
```
- ❌ FAIL if: schema is missing
- ❌ FAIL if: `name` field is not in question format
- ❌ FAIL if: `text` field contains HTML tags

### G4-B: Article Schema Present
- Required on all Q&A and guide pages
- Must include: headline, author (Zawwad), publisher (SupaTax AI), datePublished, dateModified
- ❌ FAIL if: missing or incomplete

### G4-C: BreadcrumbList Schema Present
- Required on all Q&A and guide pages
- Must include: Home → Tax Answers → [Page Title] (3 levels)
- ❌ FAIL if: missing or only 2 levels

### G4-D: Schema JSON-LD is Valid
- No trailing commas, no malformed JSON
- Test with: schema.org validator or Google Rich Results Test
- ❌ FAIL if: JSON is syntactically invalid

---

## GATE GROUP 5: META DATA (Every page type)

### G5-A: Meta Title Format
- Q&A pages: "[Target Keyword Variant] | SupaTax AI" or "[Target Keyword Variant] (Year)"
- Max 60 characters preferred, hard max 65 characters
- ❌ FAIL if: over 65 characters
- ❌ FAIL if: keyword not present in title

### G5-B: Meta Description
- Length: 140–160 characters
- Must contain: the direct answer to the question (not just a description of what the page covers)
- ❌ FAIL if: under 140 characters (wasted SERP real estate)
- ❌ FAIL if: over 160 characters (gets truncated, wasted copy)
- ❌ FAIL if: starts with "In this article..." or similar

### G5-C: Canonical Tag
- Every page must have a self-referencing canonical tag
- ❌ FAIL if: canonical is missing or points to a different URL

---

## GATE GROUP 6: TOPICAL BORDERS (Every page type)

### G6-A: Page Is Within Topical Borders
The following topics are BANNED from supatax.ai content:
- Payroll software tutorials (QuickBooks, Gusto, ADP)
- Accounting software how-tos (QuickBooks, Xero, Wave)
- International/foreign tax (unless US taxpayer with foreign income)
- Business formation (forming an LLC, incorporation steps) — this is suparank.co territory
- Estate planning (writing a will, trust creation) — mention estate TAX only
- Cryptocurrency tax in depth (a brief mention is okay, not a dedicated page)
- Immigration and visa tax implications
- ❌ FAIL if: page's primary topic is on the banned list
- Note: Mentioning these topics briefly in context is fine. The page cannot be ABOUT them.

### G6-B: No Cannibalization With Existing Pages
- Before publishing, check: does a page with the same dominant intent already exist?
- ❌ FAIL if: two pages target the exact same dominant intent (e.g., two pages both trying to rank for "is homeowners insurance tax deductible")
- Companion pages (different phrasing, cross-linked) are allowed — but they must have meaningfully different angles

---

## GATE GROUP 7: WRITING QUALITY

### G7-A: No Filler Phrases
The following phrases are BANNED and auto-fail:
- "In this article, we will explore..."
- "Great question!"
- "Tax season can be stressful, but..."
- "As a taxpayer, you may be wondering..."
- "It's important to note that..."
- "In conclusion..."
- "We hope this article helped..."
- "Please consult a tax professional for advice specific to your situation" (allowed ONCE at end, not mid-content)
- ❌ FAIL if: any of these appear in the content

### G7-B: No Pronoun Ambiguity on Entities
- When two entities of the same type appear (e.g., two IRS forms, two states), never use ambiguous pronouns
- ❌ FAIL if: "it" or "they" could refer to more than one entity in the paragraph

### G7-C: Sentence Dependency Structure
- Each sentence should contain one idea
- Sentences over 35 words must be split
- ❌ FAIL if: more than 3 consecutive sentences exceed 30 words each

---

## QUALITY GATE OUTPUT FORMAT

Claude Code must append this block to every piece of generated content:

```
=== QUALITY GATE RESULTS ===
Page ID: [P###]
Target Keyword: [keyword]
Word Count: [X] | Gate G1-A: [PASS/FAIL]
H1 Contains Keyword: [PASS/FAIL]
H2 Count: [X] | Gate G1-C: [PASS/FAIL]
No Preamble: [PASS/FAIL]
IRS Form Referenced: [Form XXXX] | Gate G2-A: [PASS/FAIL]
Tax Year Stated: [Year] | Gate G2-B: [PASS/FAIL]
Specific Rate/Number: [X%/$X] | Gate G2-C: [PASS/FAIL]
State-Specific Note: [State] | Gate G2-D: [PASS/FAIL]
Information Gain Element: [describe what we have that TaxGPT doesn't] | Gate G2-E: [PASS/FAIL]
Internal Links Count: [X] | Gate G3-A: [PASS/FAIL]
All Slugs Valid: [PASS/FAIL]
Anchor Text Quality: [PASS/FAIL]
Annotation Text Quality: [PASS/FAIL]
Within Topical Borders (no off-topic links): [PASS/FAIL]
FAQPage Schema: [PASS/FAIL]
Article Schema: [PASS/FAIL]
BreadcrumbList Schema: [PASS/FAIL]
Meta Title Length: [X chars] | Gate G5-A: [PASS/FAIL]
Meta Description Length: [X chars] | Gate G5-B: [PASS/FAIL]
No Cannibalization: [PASS/FAIL]
No Filler Phrases: [PASS/FAIL]

OVERALL: [ALL PASS → READY TO PUBLISH | X FAILS → NEEDS REVISION]
Failed gates: [list any failures]
```

---

## BATCH WRITING PROTOCOL

Since all 150 pages will be written before publishing begins:

1. **Write in cluster batches** — write all pages in a cluster together so you can verify the internal links are consistent across the cluster before writing the next one
2. **After writing each cluster** — do a cross-check: does every `internal_links_to` slug in this cluster exist in the content you've written?
3. **Run quality gates on every page individually** — not just the cluster as a whole
4. **Flag pages that need real-time data** (AFR rates, tax year 2025 specific numbers) — these need a final accuracy check before publishing, not just at writing time
5. **Write guides last** within each cluster — so all the Q&A pages they reference are written first

---

## REVISION PROTOCOL

If a page fails any gate:
1. Note the specific gate(s) that failed
2. Fix only the failed element — don't rewrite the entire page
3. Re-run the full quality gate checklist
4. Only mark `ready-to-publish` when ALL gates pass

---

*Quality gates version: 1.0*
*Last updated: 2026-03-31*
*These rules do not bend for speed. One bad page that causes a negative ranking state sets back the entire 90-day plan.*
