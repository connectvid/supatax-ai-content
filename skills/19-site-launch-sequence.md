---
skill: 16-site-launch-sequence
description: Exact launch sequence for new sites. Every step must be completed in order. Encodes the wyomingllc.co failure pattern as the anti-pattern to never repeat.
version: 2.0.0
last-verified: 2026-03
source: Ahrefs Technical SEO Guide + wyomingllc.co anti-patterns
---

# Skill 16: Site Launch Sequence

## The Anti-Pattern (wyomingllc.co)

[WYOMING LESSON] The wrong sequence:
1. Register domain
2. Build 480 pages immediately
3. Publish everything
4. Wonder why nothing is indexed
5. Discover 236 orphaned pages
6. Discover 8 broken 404s with 26 links
7. Discover thin content on 50+ pages
8. Spend 2 phases doing rework

Cost: months of rework, delayed rankings, frustrated customers.

## The Correct Sequence

**Phase 0 → Phase 1 → Index Gate → Phase 2 → Index Gate → Phase 3+**

Never skip the index gates. Never.

---

## Phase 0: Infrastructure (Before Any Content)

**Do ALL of this before writing one word of content.**

### Day 0: Project Setup
- [ ] Domain purchased and pointed to Vercel
- [ ] SSL certificate active (Vercel auto-configures)
- [ ] Repository created in GitHub
- [ ] Next.js 15 project initialized (App Router, TypeScript, Tailwind)

### Day 0: Configuration (NEVER CHANGE AFTER THIS)
- [ ] `trailingSlash: true` in next.config.mjs — PICK ONE, LOCK IT
- [ ] All synonym redirects defined in next.config.mjs
- [ ] Security headers configured in next.config.mjs
- [ ] Image optimization configured

### Day 0: SEO Infrastructure
- [ ] `app/sitemap.ts` dynamic (real mtime, NOT `new Date()`)
- [ ] `app/robots.ts` (blocks /components/, /lib/, /api/)
- [ ] No static XML sitemaps in /public/ — delete if exist
- [ ] `app/not-found.tsx` custom 404 page with popular links and search

### Day 0: Analytics & Tracking
- [ ] Google Search Console property created
- [ ] GSC verification code in layout.tsx metadata (real code, not placeholder)
- [ ] GA4 script in layout.tsx
- [ ] Plausible script in layout.tsx
- [ ] Microsoft Clarity script in layout.tsx

### Day 0: Components Built
Build these BEFORE any content page:
- [ ] Navbar with server-rendered links to all hub pages
- [ ] Footer with server-rendered links to all hubs + legal + contact
- [ ] StickyCTA component (floating, follows scroll)
- [ ] FloatingWhatsApp button (always visible, bottom-right)
- [ ] FAQSection component (renders FAQ + auto-generates FAQPage JSON-LD)
- [ ] Breadcrumbs component (renders + auto-generates BreadcrumbList JSON-LD)
- [ ] PricingTable component (full breakdown transparency)
- [ ] TrustBar component (client count, rating, guarantee)
- [ ] LastUpdated component
- [ ] TableOfContents component (auto-generated from H2s)

### Day 0: Server Rendering Verification
Before publishing: verify all navigation is server-rendered:
```bash
curl -s https://yourdomain.com/ | grep 'href="/'
```
If this returns empty or few results: critical bug — fix before continuing.

---

## Phase 1: Foundation (3-5 Quality Pages)

[AHREFS RULE] Establish crawlable, quality content before scaling. Never skip this phase.

### Day 1-3: First Pages
Build exactly 3 high-quality pages:
1. **Homepage** — clear value proposition, links to all hub pages, above-fold CTA
2. **First pillar page** — fully complete (2,500+ words, schema, FAQ, OG image, 3+ internal links)
3. **About/Contact page** — real entity information, CAA credentials, contact methods

### Day 1-3: Day 1 Verification
- [ ] HTTPS working and redirecting correctly
- [ ] sitemap.xml accessible at /sitemap.xml
- [ ] robots.txt accessible at /robots.txt
- [ ] GSC sitemap submitted
- [ ] Bing Webmaster Tools sitemap submitted
- [ ] All 3 Phase 1 pages submitted individually via GSC URL Inspection
- [ ] Schema validated with Google Rich Results Test on all 3 pages
- [ ] Lighthouse score 90+ on homepage

### Day 1-3: Foundational Link Building (Start NOW, not later)
- [ ] Twitter/X profile created with site link
- [ ] LinkedIn company page created with site link
- [ ] ProductHunt submission scheduled (not posted yet — needs content first)
- [ ] Relevant directory submissions started (Toolify.ai, AlternativeTo, etc.)
- [ ] HARO account created and alerts set

---

## INDEX GATE 1 — Wait for Phase 1 Indexing

**DO NOT BUILD PHASE 2 UNTIL THIS PASSES.**

Check GSC daily:
- Go to URL Inspection for each Phase 1 page
- Wait for status: "URL is on Google" (not "Crawled, not indexed")
- Typically takes 3-10 days for new domains
- DR0 domains with directory links: sometimes 1-3 days

If not indexed after 14 days:
1. Run: `curl -s https://domain.com/ | grep 'href="/'` — are links server-rendered?
2. Check robots.txt — is Googlebot accidentally blocked?
3. Check for accidental noindex tags on pages
4. Check GSC for crawl errors
5. Build 2-3 more foundational backlinks

---

## Phase 2: Topical Coverage (Hub Pages)

Only begin after INDEX GATE 1 passes.

### Week 3-5: Pillar Pages
Build all 5 pillar pages. Order matters — build parents before children.
Publish in batches of 3-5, not all at once.

After each batch:
- Submit each new URL via GSC URL Inspection → Request Indexing
- Wait for indexing signal before next batch
- Monitor Coverage report — "Crawled not indexed" growing faster than "Indexed" = STOP and diagnose

### Hub Page Checklist (Every Hub Page)
- [ ] 2,500-3,000 words minimum
- [ ] Answer capsule in first 100 words (40-80 words, direct answer)
- [ ] All cluster/spoke pages already listed in internal linking plan
- [ ] Links to ALL planned child spoke pages (even if spokes not built yet — link to where they'll be, fix broken links once built)
- [ ] FAQ section with 8+ real questions
- [ ] FAQPage + Article + BreadcrumbList schema
- [ ] Unique OG image 1200×630
- [ ] H2 questions format (every H2 is a question including the entity)
- [ ] CTA at bottom linking to /apply/ (or relevant service page)

---

## INDEX GATE 2 — Wait for Phase 2 Hub Indexing

**DO NOT BUILD SPOKE PAGES UNTIL HUB PAGES ARE INDEXED.**

Same check as Gate 1. Hubs should index faster than Gate 1 because domain now has history.

---

## Phase 3: Spoke Pages (Clusters)

Only begin after INDEX GATE 2 passes.

Build spokes in order of commercial priority (highest CPC keywords first).
Minimum 1,500 words per spoke page.
Every spoke page must:
- Link UP to parent hub
- Link SIDEWAYS to 2-3 sibling spokes
- Link DOWN to /apply/ or relevant service page
- Have 8+ internal links pointing to it across the site before indexing

---

## Phase 4: Tools, Spanish, Remaining Services

Only begin after core English spoke pages are indexed and showing GSC impressions.

---

## Phase 5: Scale (Blog + Long-Tail)

Only begin after Phase 3 pages are indexed and showing traffic signals.
Agent publishes 1 blog post per day at this stage.
Never skip this gate — publishing at scale before core is indexed wastes crawl budget.

---

## Weekly Monitoring (Every Monday)

Track these 5 numbers per site:
1. Ahrefs DR
2. Ahrefs organic traffic estimate
3. GSC impressions (last 28 days)
4. GSC clicks (last 28 days)
5. Pages published count vs. pages indexed count

**Red flag:** "Crawled not indexed" count growing faster than "Indexed"
Action: STOP all publishing on that site until diagnosed.

---

## Launch Week Checklist (Day-by-Day)

### Day 1: Deploy & Verify
- [ ] HTTPS working
- [ ] www redirect working
- [ ] sitemap.xml accessible
- [ ] Submit sitemap to GSC
- [ ] Submit sitemap to Bing Webmaster Tools
- [ ] All analytics tracking fires
- [ ] Test every link on homepage (no 404s)
- [ ] Test mobile rendering on real device
- [ ] Validate all schema with Google Rich Results Test

### Day 2: Content Audit
- [ ] Visit every page — check broken links, layout issues
- [ ] Every page has: meta title, meta description, canonical, OG tags
- [ ] Every page has: at least one CTA, proper schema, 3+ internal links
- [ ] Run Lighthouse on homepage and 3 key pages (target: 90+)

### Day 3: Indexing Push
- [ ] Submit all URLs via GSC URL Inspection (Phase 1 pages only)
- [ ] Submit to IndexNow for Bing/Yandex
- [ ] Verify robots.txt is correct

### Day 4-5: Conversion Testing
- [ ] Test conversion funnel on real mobile device (can you buy in <3 taps?)
- [ ] Test WhatsApp link works
- [ ] Test all pricing — no discrepancies between pages
- [ ] Have someone else attempt to "buy" and report friction

### Day 6-7: Link Building Kickoff
- [ ] Submit to first 5 directories
- [ ] Send first 10 broken link outreach emails
- [ ] Post first Reddit/Quora genuine answers (no spam)
