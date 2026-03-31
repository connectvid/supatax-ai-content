---
skill: 17-lessons-learned-wyomingllc
description: Hard-won lessons from 6 months building wyomingllc.co. Load for every new project. These mistakes cost weeks of rework — never repeat them.
version: 1.0.0
last-verified: 2026-03
source: wyomingllc.co project — 6 months real data, real customers, real failures
---

# Skill 17: Lessons Learned — wyomingllc.co

> Every rule here cost weeks of rework. Read before building anything.

---

## The 15 Mistakes — Never Repeat

### Mistake 1: Thin Pages Published, Expanded Later
**Cost:** 2 full rework phases (Phase A + Phase B). 78 pages, 47K lines added.
**Rule:** NEVER publish under 1,500 words. If topic can't fill 1,500 words, merge into parent or skip.

### Mistake 2: Cannibalization Clusters
**Cost:** 7 major cannibalization clusters including 20 pages competing for "bank account for Wyoming LLC."
**Rule:** Before ANY new page: check keyword-to-URL map. One keyword = one URL. Map EVERYTHING before writing.

### Mistake 3: 0% Conversion Rate Despite Traffic
**Cost:** Real customer (JPCheng) spent 2+ hours, asked 25 WhatsApp questions, still didn't buy.
**Root causes:** No sticky CTA, CTA below fold on mobile, pricing discrepancy destroyed trust, no "What's Included" breakdown.
**Rule:** Design conversion funnel BEFORE writing content. Every page needs: above-fold CTA + sticky CTA + transparent pricing + WhatsApp within 1 tap.

### Mistake 4: 236 Orphaned Pages
**Cost:** 236 pages Google couldn't discover. Had to manually audit and add every missing hub link.
**Rule:** When you create a page, SIMULTANEOUSLY: add to hub page + add to sitemap + link from 2-3 related pages + link from new page to 2-3 related pages.

### Mistake 5: Client-Side Only Homepage Links
**Cost:** Google crawler saw zero links from homepage. Content pages invisible to Google.
**Rule:** ALL internal links must be server-rendered. Test with: `curl -s https://yourdomain.com/ | grep 'href="/'` — every important page must appear in this output.

### Mistake 6: Trailing Slash Chaos
**Cost:** Mixed formats required fixing 21 URL patterns across 200+ files.
**Rule:** Set `trailingSlash: true` in next.config.mjs on Day 1. Never change after launch.

### Mistake 7: Conflicting Static + Dynamic Sitemaps
**Cost:** 521 phantom URLs blocking real pages from being crawled.
**Rule:** ONE sitemap source — `app/sitemap.ts` only. Delete any static XML files in /public/.

### Mistake 8: No Backlinks Until Too Late
**Cost:** DR=0 after months of content. Rankings stalled.
**Rule:** Start link building Week 1. Even 5 DA30+ backlinks changes the trajectory.

### Mistake 9: Off-Topic Content on Niche Domain
**Cost:** 8 ITIN/crypto pages diluted wyomingllc.co topical authority. Had to noindex all.
**Rule:** Every page must serve the site's primary topical authority. Wrong domain = publish on correct domain instead.

### Mistake 10: Formation Synonym Explosion
**Cost:** Needed 60+ redirects post-launch for "form/create/open/start/register/set up LLC."
**Rule:** Brainstorm ALL synonyms for primary actions BEFORE launch. Set up redirects in next.config.mjs from Day 1.

### Mistake 11: Generic Schema Markup
**Cost:** All pages had `headline: "Wyoming LLC Guide"` — Google couldn't differentiate pages.
**Rule:** Every page gets unique schema. Schema headline must match H1 exactly. No copy-paste between pages.

### Mistake 12: Customer Questions Not on Website
**Cost:** 25+ real customer questions answered only on WhatsApp. Wasted SEO gold.
**Rule:** Every customer question → website content within 48 hours. WhatsApp question → FAQ entry → standalone page if volume > 200/month.

### Mistake 13: Links to Non-Existent Pages
**Cost:** 8 broken 404 pages with 26 links pointing to them. Wasted crawl budget.
**Rule:** Before launch, audit all href= values. Every link target must exist. Run: `grep -r 'href="/' app/` and verify every page.tsx exists.

### Mistake 14: Pricing Transparency Failure
**Cost:** Customer caught $60 vs $100 discrepancy. Lost trust instantly. Lost sale.
**Rule:** Radical pricing transparency — show exact breakdown, Year 1 AND Year 2+, what's included vs not. Zero conflicting numbers anywhere.

### Mistake 15: Overly Ambitious Timeline
**Cost:** Burnout risk, incomplete execution, phases taking 2-3x longer than planned.
**Rule:** Plan for 2x the time. Execute 5 pages perfectly > 50 pages poorly.

---

## What Actually Worked

### Koray's Semantic SEO Framework
- Question-format H2s rank for featured snippets
- 40-word extractive answers in first sentence of each H2
- Entity-Attribute-Value (EAV) coverage for topical authority
- No hedging language ("costs $100" not "typically costs around $100")
- Tables for comparisons (not prose)
- Numbered lists for processes, bullet lists for attributes

### Programmatic Content at Scale
- Next.js dynamic routes for pattern pages (country pages, state pages)
- Claude API + DataForSEO pipeline for keyword gap identification
- Agent-generated content with human review for quality gate

---

## Pre-Launch Checklist (Non-Negotiable)

### Before Any Code
- [ ] Complete keyword-to-URL map (every page planned before writing)
- [ ] Cannibalization check (no two URLs targeting same primary keyword)
- [ ] Full topical map drawn (hub-and-spoke diagram)
- [ ] Conversion funnel designed (Landing → Learn → Trust → Buy)
- [ ] Pricing documented with full transparency breakdown
- [ ] All synonym redirects planned

### Day 1 Technical Setup
- [ ] `trailingSlash: true` in next.config.mjs
- [ ] All synonym redirects in next.config.mjs
- [ ] Dynamic `app/sitemap.ts` (no static XML)
- [ ] `app/robots.ts` — block /components/, /lib/, /api/
- [ ] `app/not-found.tsx` — custom 404 with popular links
- [ ] GA4 + Plausible + Microsoft Clarity
- [ ] GSC verification (real code, not placeholder)
- [ ] All security headers configured

### Before Publishing First Page
- [ ] Navbar with server-rendered links to all hubs
- [ ] Footer with server-rendered links to all hubs + legal + contact
- [ ] StickyCTA component built
- [ ] WhatsApp floating button built
- [ ] FAQ component with auto FAQPage schema
- [ ] Breadcrumbs with auto BreadcrumbList schema
- [ ] ValueStack / pricing breakdown component

### Before Publishing Any Page
- [ ] Page is 1,500+ words
- [ ] Hub page already links to this page
- [ ] This page links to hub + 2-3 siblings
- [ ] Schema headline matches H1 exactly
- [ ] No pricing discrepancies with any other page
- [ ] All href= values point to pages that exist

---

## Content Standards (Updated from Real Experience)

### Minimum Word Counts
| Page Type | Minimum | Ideal |
|-----------|---------|-------|
| Hub/Pillar | 3,000 | 3,500+ |
| Spoke/Cluster | 1,500 | 2,000+ |
| Comparison | 2,500 | 3,000+ |
| Country/Region | 2,000 | 2,500+ |
| Tool page | 1,000 | 1,500+ |
| Blog post | 1,000 | 1,200+ |

### Minimum Internal Links Per Page
| Page Type | Minimum |
|-----------|---------|
| Hub/Pillar | 15+ |
| Spoke/Cluster | 8+ |
| Blog post | 5+ |
| Service page | 5+ |

### H2 Writing Rules
- Every H2 must be a question
- Must include the target entity in the question: "How much does a Wyoming LLC cost?" NOT "How much does it cost?"
- Answer in FIRST sentence after H2
- First answer must be ≤40 words (featured snippet extraction length)
- Expand with full detail after the 40-word answer

### Forbidden Language
Never write:
- "might," "could," "possibly," "perhaps," "generally," "typically," "usually"
- "click here," "learn more," "read more" as anchor text
- "In this guide, we will cover..."
- "In conclusion..."
- "It goes without saying..."
- Passive voice when active is possible

---

## Internal Link Audit Commands (Run Monthly)

```bash
# Find all internal links
grep -r 'href="/' app/ --include="*.tsx" | grep -v node_modules

# Find all pages that exist
find app/ -name "page.tsx" -not -path "*/components/*"

# Find all links to non-existent pages
# (compare output of both commands — every link target needs a page.tsx)
```

---

## The Conversion Template (Every Page)

Based on real customer failures, every page needs this structure:

```
1. Hero: H1 + 1-sentence value prop + PRIMARY CTA (above fold, mobile-visible)
2. Quick Answer: 40-word answer to main question
3. Table of Contents (auto-generated)
4. Core Sections with question H2s
5. Pricing section with FULL TRANSPARENCY breakdown:
   - What you pay (Year 1)
   - What each component costs
   - What's included vs not included
   - Year 2+ cost (never hide this)
6. FAQ: 8+ real customer questions
7. Trust signals: reviews, credentials, guarantees
8. Final CTA + WhatsApp option
```

---

## Month 1-3 Roadmap (Realistic)

### Month 1: Foundation (not speed)
- Week 1-2: 5-10 hub/pillar pages (3,000+ words each)
- Week 3-4: 15-20 spoke pages (1,500+ words each)
- Ongoing: Link building starts Week 1, not after content is done
- Gate: 0 thin pages, 0 orphaned pages, 5+ backlinks

### Month 2: Expansion
- Week 5-8: 20-30 more spoke pages + 10 comparison pages
- Gate: 10+ backlinks, first keywords appearing in GSC

### Month 3: Optimization
- Refresh Month 1 content with GSC data
- Double down on what's ranking
- Prune what has zero impressions after 90 days
- Gate: 5-10 keywords in top 20, first organic conversions
