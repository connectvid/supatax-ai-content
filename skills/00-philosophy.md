---
skill: 00-philosophy
description: Core SEO philosophy, unbreakable rules, and hard-won lessons. Load first in every session.
version: 2.0.0
last-verified: 2026-03
source: Ahrefs + Koray GUBUR + wyomingllc.co hard lessons (6 months real data)
---

# Skill 00: Philosophy & Unbreakable Rules

## Why This File Exists

Every rule in this file was either validated by Ahrefs research, proven by Koray's topical authority framework, or LEARNED THE HARD WAY from 6 months building wyomingllc.co. The lessons marked [WYOMING LESSON] are things that cost weeks of rework. Never repeat them.

---

## The 10 Commandments

These are non-negotiable. Break any of them and you are setting up future rework.

**1. Map everything before writing anything.**
Create the full topical map + keyword-to-URL spreadsheet + content briefs BEFORE writing one word. The wyomingllc.co project created 7 cannibalization clusters and 236 orphaned pages because we skipped this step.

**2. No page under 1,500 words.**
[WYOMING LESSON] We launched 50+ country pages at 66-168 words. Google saw thin content. We had to expand ALL of them across two full rework phases. If you can't write 1,500 words on a topic, merge it into a parent page or don't create it.

**3. One keyword = one URL. No exceptions.**
[WYOMING LESSON] We created 20 pages all targeting "bank account for Wyoming LLC." This destroyed topical clarity. Before creating any page, check: does another page on this site already target this keyword? Use the 03-keyword-map.csv as the single source of truth.

**4. Every page links to 3+ other pages AND has 3+ pages linking to it.**
[WYOMING LESSON] 236 pages were orphaned — Google couldn't discover them. When you create a page, SIMULTANEOUSLY add it to its hub page, add it to sitemap, and link from 2-3 related pages.

**5. Hub pages link to ALL their spokes. Check weekly.**
[WYOMING LESSON] Our hub pages were missing links to 236 spoke pages. Hub completeness is not optional. Every time a spoke is created, the hub must be updated that same session.

**6. Design the conversion funnel before writing content.**
[WYOMING LESSON] A real user (JPCheng) spent 2+ hours on site, asked 25 WhatsApp questions, and didn't buy. The site was built for reading, not buying. Every page needs: above-fold CTA, sticky CTA on scroll, transparent pricing, WhatsApp within 1 tap on mobile.

**7. Start link building in Week 1. Not after content is done.**
[WYOMING LESSON] DR=0 after months of content. Content quality alone doesn't rank. Even 5 backlinks from DA30+ sites would have changed the trajectory entirely.

**8. Trailing slash, redirects, sitemap, schema — configure on Day 1.**
[WYOMING LESSON] Changing trailingSlash after launch required fixing 21 URL patterns across 200+ files. Set these once on Day 1, never change them.

**9. Customer questions become website content within 48 hours.**
[WYOMING LESSON] 25+ real customer questions were answered only on WhatsApp. These are the highest-value SEO content. Every customer question → FAQ entry → standalone page if volume > 200/month.

**10. Plan for 2x the time. Execute 10 pages perfectly not 100 poorly.**
Every phase took longer than planned. Prioritize ruthlessly. The top 3 highest-impact items before anything else.

---

## The SEO Truth Stack (Priority Order)

When rules conflict, this hierarchy decides:

1. **Crawlable + Indexable** — Nothing else matters if Google can't see the page
2. **Correct search intent match** — Wrong content type = zero ranking regardless of quality
3. **Topical authority** (Koray) — Cover the topic completely before scaling
4. **EEAT signals** — Trust signals for YMYL, author credentials, entity establishment
5. **On-page optimization** — Title, meta, schema, internal links
6. **Content quality** — Depth, accuracy, answer capsules, FAQs
7. **AI visibility** — GEO/AEO signals (ranks in Google first = appears in AI)

---

## Ahrefs' 8 Non-Negotiable Facts (Jan 2026)

These come directly from Ahrefs research, not opinion:

1. **90.63% of pages get zero traffic** — because they target what nobody searches. Every page needs real keyword volume.
2. **Pages need to be crawlable and indexable before anything else matters.**
3. **Most LLMs don't render JavaScript** — navigation and key content must be in server-rendered HTML.
4. **AI-generated content can and does rank well** — quality and intent match matter more than origin.
5. **Google gets 373x more searches/day than ChatGPT** — build for Google first, AI visibility follows.
6. **LLMs.txt is not worth the effort** — skip it.
7. **Meta descriptions influence ChatGPT citation selection** — write them as if AI is reading them to decide relevance.
8. **FAQPage schema = 3.2x AI citation rate uplift** — not for SERP rich results, for AI Overviews.

---

## The Koray Thesis (One Sentence)

Cover a topic COMPLETELY across an interconnected network of pages, and Google will grant topical authority that no individual page can earn alone.

What "completely" means: every entity, every attribute, every audience segment, every comparison, every use case, every process step — each on its own URL if search volume exists.

---

## What NEVER to Do

From wyomingllc.co real mistakes:

- Never publish a page and "expand it later" — expand it before publishing
- Never create a new page without first checking the keyword-to-URL map
- Never launch without building all components: Navbar (server-rendered), Footer (server-rendered), StickyCTA, WhatsApp button, FAQ component, Breadcrumbs
- Never have inconsistent pricing anywhere on the site — one wrong number destroys trust
- Never publish off-topic content on a niche domain (e.g., ITIN content on wyomingllc.co diluted topical authority)
- Never use `new Date()` in sitemap — use actual file modification times
- Never create static XML sitemaps alongside dynamic `app/sitemap.ts`
- Never have trailing slash inconsistency — set in next.config.mjs on Day 1, never change
- Never link to pages that don't exist — audit all href values before launch
