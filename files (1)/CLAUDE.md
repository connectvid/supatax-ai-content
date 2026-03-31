# CLAUDE.md
## Instructions for Claude Code — supatax.ai Build System

Read this file completely before writing any code or content for this project.

---

## YOUR ROLE

You are building SEO-optimized WordPress content for supatax.ai. Your primary output is:
1. WordPress page/post content (HTML or Gutenberg block format)
2. Schema JSON-LD markup
3. Meta title and description
4. Internal link anchor text with annotation text

You are NOT writing generic content. Every piece must follow the Holistic SEO methodology outlined in this document and in the KORAY skill file.

---

## HOW TO BUILD A Q&A PAGE

### Step 1: Read the page spec from 01-pages-master.csv
Find the page by slug. Extract:
- `target_keyword` — this is your H1 basis
- `meta_title` — use exactly as written (already optimized)
- `meta_description_hint` — expand this into a full 150-160 character meta description
- `internal_links_to` — you MUST include all listed links as I-nodes in the content
- `cluster` — tells you which other pages exist to reference
- `word_count_target` — hit this range (±100 words)

### Step 2: Write the content structure

```
[META TITLE: from pages-master.csv]
[META DESCRIPTION: expanded from hint, 150-160 chars]

H1: [target_keyword verbatim OR near-exact variant that is grammatically natural]

[ANSWER PARAGRAPH — 2-3 sentences that DIRECTLY answer the H1 question]
[No preamble. No "In this article". No "Great question". Start with the answer.]
[Include: IRS form number if applicable | Tax year (2025 or 2026) | Specific rate/threshold]

H2: [Sub-intent 1 — the next most important question a user has after getting the direct answer]
[Paragraph — 80-120 words. Dense, entity-rich. EAV structure: Entity + Attribute + Accurate Value]

H2: [Sub-intent 2 — edge case, exception, or "how to" apply this]
[Paragraph or numbered list if procedural — use numbered list for steps, bullet for options]

H2: [Sub-intent 3 — state-specific note or common mistake]
[Paragraph — flag at least one state where rules differ from federal]

H2: Related Tax Questions
[3 I-node links — use the exact slugs from internal_links_to column]
[Format: "For related reading, see [anchor text](/tax-answers/slug/) — [1 sentence annotation explaining the connection]."]

[SCHEMA — see schema section below]
```

### Step 3: I-node link formatting

DO THIS:
```html
<p>Homeowners insurance is not deductible for personal residences, but several other 
property-related costs are. For example, <a href="/tax-answers/are-closing-costs-tax-deductible/">
closing costs can sometimes be deducted</a> depending on the type of cost and whether 
you're a buyer or seller.</p>
```

NOT THIS:
```html
<p>Learn more about closing costs <a href="/tax-answers/are-closing-costs-tax-deductible/">here</a>.</p>
```

### Step 4: Schema JSON-LD

Every Q&A page needs THREE schema blocks:

```html
<!-- FAQPage Schema -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "[H1 phrased as a question — if H1 is already a question, use verbatim]",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "[First answer paragraph — plain text only, no HTML tags]"
    }
  }]
}
</script>

<!-- Article Schema -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "[meta title]",
  "author": {
    "@type": "Person",
    "name": "Zawwad",
    "url": "https://supatax.ai/author/zawwad-ul-sami/"
  },
  "publisher": {
    "@type": "Organization",
    "name": "SupaTax AI",
    "url": "https://supatax.ai"
  },
  "datePublished": "[YYYY-MM-DD]",
  "dateModified": "[YYYY-MM-DD]"
}
</script>

<!-- BreadcrumbList Schema -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://supatax.ai/"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Tax Answers",
      "item": "https://supatax.ai/tax-answers/"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "[H1]",
      "item": "https://supatax.ai[page slug]"
    }
  ]
}
</script>
```

---

## HOW TO BUILD A PILLAR GUIDE

### Differences from Q&A pages:
- Longer (2,500–3,000 words)
- More H2 sections (6–10)
- H3 sub-sections allowed and encouraged
- Links to 4–6 Q&A pages as I-nodes
- Include a dedicated "Frequently Asked Questions" H2 section with 3–5 questions
- Use `Article` schema not `FAQPage` as primary (but include `FAQPage` for the FAQ section)

### Guide content structure:
```
H1: [target_keyword or compelling head term variant]

[Introduction — 100-150 words. Satisfy primary intent. Set scope. No fluff.]

H2: [First major section — definition or "what is"]
H3: [Specific detail]
H3: [Specific detail]

H2: [Second major section — how it applies/how to calculate]
[I-node link to relevant Q&A page embedded here]

H2: [Third major section — exceptions or advanced cases]
[I-node link to relevant Q&A page embedded here]

H2: [Fourth section — state-specific or year-specific rules]
[I-node link to relevant Q&A page embedded here]

H2: [Fifth section — comparison or common mistakes]

H2: Frequently Asked Questions
[3-5 Q&As covering PAA results — use FAQPage schema]

H2: Related Tax Resources
[I-node links to 3 Q&A pages — with annotation text]
```

---

## CONTENT QUALITY CHECKLIST

Before finalizing any piece of content, run every check in QUALITY-GATES.md and output the gate results block. Summary checklist:

- [ ] First paragraph answers the question directly — no preamble
- [ ] H1 contains or is near-exact match of target keyword
- [ ] IRS form number mentioned where applicable
- [ ] Tax year (2025 or 2026) specified
- [ ] At least one dollar amount, percentage, or threshold included
- [ ] At least one state-specific note included
- [ ] All 3 I-node links from internal_links_to column are present
- [ ] I-node anchor text is near-exact match of destination page's target keyword
- [ ] Annotation text (surrounding sentence) reinforces the semantic connection
- [ ] Word count is within ±100 of target
- [ ] All three schema blocks present (FAQPage, Article, BreadcrumbList)
- [ ] Meta description is 150-160 characters
- [ ] NO links to off-topic content outside tax domain

---

## AFTER PUBLISHING A PAGE

After each page is published, do these immediately:

1. **Backlink the new page from 2 existing pages:**  
   Look at the `internal_links_from` column in 01-pages-master.csv for the page you just published.  
   Go to those pages and add an I-node link to the newly published page.

2. **Update 04-build-order.csv:**  
   Change status from `build` to `done` and note the publish date.

3. **Submit URL to GSC:**  
   Use the URL Inspection tool in Google Search Console to request indexing.

---

## WHAT NOT TO DO

- **NEVER** start a Q&A article with "In this article we will explain..." or "Great question!" or "Let's explore..."
- **NEVER** add more than 3 I-node links in a single Q&A page
- **NEVER** link to off-topic content from tax pages (stay within tax knowledge domain)
- **NEVER** use vague anchor text like "click here", "learn more", "read this"
- **NEVER** publish a page without immediately adding links FROM 2 existing pages TO the new page
- **NEVER** exceed the topical borders defined in supatax-ai.md
- **NEVER** write a heading as a marketing phrase — headings must be semantically descriptive (e.g., "What Is Backup Withholding?" not "Everything You Need to Know!")
- **NEVER** publish the pillar guide for a cluster before the Q&A pages for that cluster are live

---

## FILE REFERENCE MAP

| File | Purpose | When to Read |
|---|---|---|
| 00-master-plan.md | Full strategy overview: clusters, traffic model, 90-day goals | First read — understand the project |
| supatax-ai.md | Site context, URL structure, existing pages, critical warnings | Before any build |
| 01-pages-master.csv | Pages P001–P061: slug, keyword, word count, schema, interlinks | When building pages from original 50 |
| 01b-pages-expansion.csv | Pages P062–P156: the additional 95 pages for 150-page target | When building expanded pages |
| 03-keyword-map.csv | Keyword → page mapping, TaxGPT competitor data, traffic estimates | When writing meta data or checking priority |
| 04-publishing-schedule.csv | Day-by-day calendar April 1–June 30 with publish dates | When deciding what to publish next |
| 04-build-order.csv | Original build order logic (superseded by schedule, keep for reference) | Reference only |
| 05-blog-posts.csv | Pillar guide specs: H2 outline, internal links, notes | When building a /guides/ page |
| QUALITY-GATES.md | 22 hard-stop quality checks — run before every publish | After generating any piece of content |
| DECISIONS-LOCKED.md | Non-negotiable architectural decisions | When uncertain about any structural decision |
| KORAY_HOLISTIC_SEO_SKILL.md | Full Holistic SEO methodology by Koray Tuğberk GÜBÜR | When uncertain about content strategy or quality |
