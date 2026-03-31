---
skill: 15-content-completeness
description: Every required element on every page before deployment. Includes validator checklist and wyomingllc.co lessons on what breaks silently.
version: 2.0.0
last-verified: 2026-03
source: wyomingllc.co lessons + Ahrefs On-Page SEO Guide + this conversation
---

# Skill 15: Content Completeness — Pre-Deployment Checklist

## Why This Exists

[WYOMING LESSON] Pages were deployed with missing schema, missing CTAs, generic headlines in schema, no FAQ sections, and no internal links. These problems compound at scale — 100 bad pages is 100x the cleanup work of 1 bad page.

The validator checks every box before ANY page touches production.

---

## HARD REQUIREMENTS — Page Fails Validation If Any Is Missing

### Identity & SEO
- [ ] H1 tag: present, exactly one, matches primary keyword
- [ ] Title tag: ≤60 characters, unique on site, contains primary keyword
- [ ] Meta description: ≤155 characters, unique on site, expands on title
- [ ] Canonical tag: points to own URL exactly
- [ ] URL slug: lowercase, hyphens, no dates, matches target keyword

### Open Graph (AI Citation + Social)
- [ ] og:title present
- [ ] og:description present (≤155 chars)
- [ ] og:image present — 1200×630px, readable at small size
- [ ] og:url present (canonical URL)
- [ ] twitter:card present

### Images
- [ ] Minimum 1 image on page (hero image)
- [ ] Every image has alt text (minimum 10 characters)
- [ ] At least one image alt text contains primary keyword
- [ ] No images with filename-only alt text (e.g., "image-1.png" is not alt text)
- [ ] OG image is 1200×630px

### Content Structure
- [ ] Exactly 1 H1 tag
- [ ] Minimum 3 H2 tags
- [ ] Every H2 is a question (includes entity name)
- [ ] Answer capsule in first 100 words (40-80 words, direct answer)
- [ ] FAQ section present (minimum 5 Q&As)
- [ ] Word count: minimum 1,500 words (pillar: 2,500+)
- [ ] Table of Contents present (for pages >1,500 words)
- [ ] No placeholder text ("Lorem ipsum", "Coming soon", "TBD")

### Schema
- [ ] At minimum 1 JSON-LD schema block present
- [ ] FAQPage schema present if FAQ section present
- [ ] Schema headline matches H1 EXACTLY (not "Site Name Guide")
- [ ] Schema description matches meta description EXACTLY
- [ ] datePublished in schema (ISO 8601 format)
- [ ] dateModified in schema (ISO 8601 format — real update date, not build date)
- [ ] Article schema on all blog/content pages
- [ ] HowTo schema on all process/how-to pages
- [ ] Service schema on all service pages
- [ ] BreadcrumbList schema present and accurate

### Internal Links
- [ ] Minimum 3 internal links pointing TO this page (check 02-internal-links.csv)
- [ ] All mandatory links from 02-internal-links.csv included
- [ ] Descriptive anchor text on every link (never "click here" or "learn more")
- [ ] No links to pages that don't exist (run href audit)
- [ ] CTA link to /apply/ (or relevant service page) present at bottom
- [ ] Link back to parent hub page present

### Conversion
- [ ] Above-fold CTA visible without scrolling on mobile
- [ ] CTA button present (not just text link)
- [ ] If pricing mentioned: full breakdown visible (not just total)
- [ ] WhatsApp contact option accessible on page

### EEAT (for YMYL pages — financial/legal/tax)
- [ ] Author field present OR organization attribution
- [ ] Last updated date visible on page
- [ ] Disclaimer present (for ITIN/tax/legal content)
- [ ] IRS verification link present (for ITIN service pages)

---

## SOFT REQUIREMENTS — Flags for Review, Not Hard Block

- Word count < 1,500 but > 800 — flag for review
- Only 3 internal links (minimum met but low) — flag for review
- No comparison table (for comparison pages) — flag for review
- FAQ has <5 Q&As — flag for review

---

## Content Writing Standards (Non-Negotiable)

### Language Rules
- Active voice always: Subject → Verb → Object
- Max 15-20 words per sentence
- No hedging: eliminate "might," "could," "possibly," "perhaps," "generally," "typically," "usually"
- State facts as facts: "ITIN processing takes 6-11 weeks" NOT "typically takes around 6-11 weeks"
- Use specific numbers: "3 requirements" NOT "several requirements"
- Date-stamp changing facts: "As of 2026, the IRS processing time is 6-11 weeks"

### H2 Rules (from Koray + wyomingllc.co validation)
- Every H2 must be a question
- Must include target entity: "How long does ITIN processing take?" NOT "Processing Time"
- Answer in first sentence after H2
- First sentence answer must be ≤40 words (featured snippet length)
- Expand fully after the 40-word answer

### Forbidden Phrases
Never write these anywhere on any page:
- "In this comprehensive guide we will cover..."
- "Click here to learn more"
- "Read more" as anchor text
- "In conclusion..."
- "It goes without saying..."
- Passive voice when active is possible
- "Various," "numerous," "many" (be specific)

### Format Rules
- Tables for ALL comparisons (never prose comparisons)
- Numbered lists for processes/steps
- Bullet lists for features/attributes
- One macro topic per page (if two topics — split into two pages)

---

## Schema Validation

After every page build, validate at:
- Google Rich Results Test: `search.google.com/test/rich-results`
- Schema.org validator: `validator.schema.org`

Common errors to catch:
- Schema headline ≠ H1 (must match exactly)
- FAQPage questions not matching visible FAQ text
- Missing required fields (author, datePublished)
- Duplicate schema on page
- JSON-LD syntax errors

---

## Minimum Content Standards Table

| Page Type | Min Words | Min H2s | Min Internal Links In | Min Internal Links Out | Required Schema |
|-----------|----------|---------|----------------------|----------------------|-----------------|
| Homepage | 800 | 4+ | All hub pages | 5 pillar pages | Org+WebSite+Service+FAQPage |
| Service page | 1,000 | 6+ | 5+ | 5+ | Service+Offer+FAQPage+Org |
| Hub/Pillar | 2,500 | 8+ | 5+ | All cluster pages | Article+FAQPage+Breadcrumb |
| Cluster/Spoke | 1,500 | 6+ | 3+ | 3+ | Article+FAQPage+Breadcrumb |
| Comparison | 2,000 | 6+ | 3+ | 3+ | Article+FAQPage+Breadcrumb |
| Blog post | 1,000 | 5+ | 3+ | 3+ | BlogPosting+FAQPage |
| Tool page | 800 | 4+ | 3+ | 3+ | SoftwareApplication+FAQPage |
| Spanish page | Match English ±20% | Match English | 3+ | 3+ | Same as English + inLanguage:es |

---

## The Orphan Prevention Check

[WYOMING LESSON] 236 pages were orphaned on wyomingllc.co.

Before publishing any page, verify:
1. Hub page already has a link to this page (or update hub page simultaneously)
2. At least 2 sibling pages link to this page
3. This page appears in sitemap.ts

After publishing:
```bash
# Verify all href= values point to existing pages
grep -r 'href="/' app/ --include="*.tsx" | grep -v node_modules
find app/ -name "page.tsx" -not -path "*/components/*"
# Every href target must have a corresponding page.tsx
```
