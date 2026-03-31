# Skills Library — Topslice Network
## 24 skill files. Load these before building anything.

> Every skill marked [UPDATED] has been rewritten with hard lessons from wyomingllc.co.
> Skills marked [CRITICAL] must be loaded for every single session, no exceptions.

---

## Quick Load Guide — Copy the right line for your task

**Starting a new site:**
`00 + 19 + 20 + 01 + 14 + 17`

**Writing any content page:**
`00 + 03 + 04 + 08 + 09 + 11 + 12 + 13 + 15 + 18`

**Building a service/pricing page:**
`00 + 02 + 06 + 11 + 16 + 18`

**Building technical infrastructure (Next.js):**
`00 + 01 + 10 + 17 + 19`

**Building a free tool page:**
`00 + 02 + 06 + 10 + 14 + 18`

**Checking before any deploy:**
`18 + 20` (completeness checklist + lessons)

**Building link selling readiness:**
`00 + 05 + 22 + 19`

---

## Full Skill Index

### TIER 1 — Foundations (load always)

| File | What it covers | When to load |
|------|---------------|--------------|
| `00-philosophy.md` | 10 commandments, hard rules, Ahrefs facts, Koray thesis | **ALWAYS — every session** |
| `01-technical-seo.md` | Crawling, indexing, robots.txt, JS rendering, AI crawlers | Technical work |
| `02-onpage-seo.md` | Title tags, meta, H1, URLs, OG tags, keywords | Any page build |
| `03-content-writing.md` | Search intent (3 Cs), EEAT, FAQ writing, AI content rules | Content writing |
| `04-keyword-research.md` | Seed keywords, KD, clustering, Opportunity Score formula | Research tasks |
| `05-link-building.md` | Foundational links, outreach, link selling hygiene | Link building |
| `06-schema-markup.md` | FAQPage, Article, Service, HowTo, BreadcrumbList JSON-LD | Any page with schema |
| `07-images-media.md` | Alt text, OG images, Next.js Image, Unsplash/Flux routing | Image work |
| `08-internal-linking.md` | Hub-and-spoke, anchor text, PageRank flow, server rendering | Linking any page |
| `09-ai-seo-geo-aeo.md` | AI Overviews, GEO, LLM crawling, answer capsules, meta as AI signal | All content |
| `10-core-web-vitals.md` | LCP ≤2.5s, INP ≤200ms, CLS ≤0.1, Next.js fixes | Performance work |
| `11-eeat-trust.md` | Experience, Expertise, Authority, Trust — YMYL rules | Service/YMYL pages |

### TIER 2 — Strategy

| File | What it covers | When to load |
|------|---------------|--------------|
| `12-topical-authority-koray.md` | Koray's framework — topic webs, semantic networks, entity coverage | Planning content |
| `13-search-intent.md` | Beyond 3 Cs — SERP volatility, mixed intent, micro-intent | Keyword planning |
| `14-tool-page-template.md` | Complete tool page structure for free tools | Building tools |

### TIER 3 — Wyomingllc Lessons [UPDATED] [CRITICAL]

These 6 files are the most important additions. Built from real failures.

| File | What it covers | When to load |
|------|---------------|--------------|
| `15-cannibalization-prevention.md` | One keyword = one URL. Real cluster examples from wyomingllc.co | Before ANY new page |
| `16-conversion-cta.md` | CTA placement, pricing transparency, real customer failure analysis | Service pages |
| `17-technical-nextjs.md` | next.config.mjs, sitemap.ts, trailing slash, server rendering test | Next.js builds |
| `18-content-completeness.md` | Pre-deploy checklist — every required element on every page | Before every deploy |
| `19-site-launch-sequence.md` | Phase 0 → index gate → scale. The anti-pattern is encoded here | New site launch |
| `20-lessons-learned-wyomingllc.md` | All 15 mistakes, what they cost, how to prevent | **New projects always** |

### TIER 4 — Operational

| File | What it covers | When to load |
|------|---------------|--------------|
| `21-brand-voice.md` | Per-site voice profiles for all domains | Content writing |
| `22-link-selling-readiness.md` | DR thresholds, marketplace setup, outreach templates | Link selling prep |
| `23-verification-scripts.md` | Shell scripts: curl checks, GSC verification, health checks | Debugging/QA |

---

## The 3 Files You Must Never Skip

1. `00-philosophy.md` — The rules. Read first, every session.
2. `19-site-launch-sequence.md` — The correct build order. Skipping this = wyomingllc.co disaster.
3. `20-lessons-learned-wyomingllc.md` — 6 months of real mistakes. Read before every new project.

---

## How to Use in Claude Code

Place this entire `skills/` folder in your project root.

In `CLAUDE.md`, add:
```
Before doing anything, read skills/ files relevant to this task.
Always start with 00-philosophy.md and 20-lessons-learned-wyomingllc.md.
```

For new sites, read 19-site-launch-sequence.md before writing one line of code.
