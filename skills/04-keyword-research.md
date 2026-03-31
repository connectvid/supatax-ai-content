---
name: keyword-research
description: Apply when selecting target keywords, evaluating KD scores, interpreting DataForSEO data, clustering keywords, or deciding which tools to build next. Triggers on: keyword, KD, search volume, opportunity score, DataForSEO, which tool to build, keyword cluster.
---
# Skill 04: Keyword Research
## Source: Ahrefs Keyword Research Guide (Dec 2024) + Keyword Difficulty Guide (Dec 2025)

---

## Core Principle (from Ahrefs)

"90.63% of pages on the internet get no traffic from Google — because they target topics nobody searches for."

Every page must target a keyword with verified search volume. No exceptions. Publishing without keyword research = joining the 90% that get zero traffic.

---

## How Keyword Difficulty Works at Ahrefs (Critical for Tool Sites)

Ahrefs KD is based on ONE thing: how many referring domains link to the top-10 ranking pages.

- KD 0–5: top-ranking pages have almost no backlinks
- KD ~50: top-ranking pages have a few hundred backlinks
- KD 90+: top-ranking pages have thousands of backlinks

**KD is an absolute metric, not relative.** It tells you the average difficulty — not your specific difficulty.

Ahrefs Dec 2025: "Think of KD like a speed limit sign. The sign says 70 MPH — but your personal difficulty depends on the car you're driving. In a Formula 1 car (high authority, strong topical relevance), 70 MPH is effortless. On a bike (new domain), even 30 MPH is impossible."

**For new sites (DR 0–15):**
- Target KD 0–15 only in the first 3–6 months
- KD 15–30 becomes achievable once you have 3+ indexed pages and growing DR
- KD 30+ requires real domain authority — 6–12+ months on a new domain

**For sites with DR 20+ and topical authority:**
- KD up to 30–35 is achievable
- Topical authority reduces effective difficulty — if you already rank for 10 markup-related keywords, the 11th is easier

---

## Seed Keyword Method (from Ahrefs)

Step 1: Think about what your target audience types to find the tool.
Step 2: Use DataForSEO or Ahrefs Keywords Explorer with seed keywords.
Step 3: Look at "Matching Terms" and "Related Terms" to expand.

Good seed keywords for tool sites:
- `markup calculator`
- `yes or no wheel`
- `gamertag generator`
- `bonus tax calculator`

Ahrefs tip: "ChatGPT can be useful for brainstorming seeds. But it won't give you real search volumes — use it for ideas, then validate with DataForSEO."

---

## Keyword Clustering (from Ahrefs)

Ahrefs: "You probably don't want to create a thousand pages to target all those keywords. Use keyword clustering to simplify your list."

Keyword clustering = grouping keywords that have the same search intent and should be targeted by one page.

Example cluster for `markup calculator`:
- markup calculator → PRIMARY (target with tool page)
- markup percentage calculator → SAME PAGE
- markup formula → SAME PAGE (FAQ or supporting content)
- markup vs margin calculator → SAME PAGE (supporting content)
- free markup calculator → SAME PAGE (meta description angle)

One page targets the entire cluster. Don't create separate pages for each variation.

How to identify a cluster: if all keywords would be equally satisfied by the same tool page, they belong in one cluster.

---

## Traffic Potential vs Search Volume (from Ahrefs)

Ahrefs: "Search volume alone doesn't tell you how much traffic a page will get. A page can rank for dozens of related keywords."

Use "Traffic Potential" not just "Search Volume" to estimate real opportunity:
- Look at the top-ranking page for a keyword
- Check how many total keywords it ranks for and total estimated traffic
- That's your real traffic ceiling

For `markup calculator` — the top-ranking page probably ranks for:
- markup calculator (22,200)
- markup percentage calculator (8,100)
- how to calculate markup (4,400)
- markup formula (3,600)
- etc.

Total traffic potential: 40,000+/month — much more than the head term alone.

---

## KD Interpretation for the 8-Site Network

Based on the DataForSEO data we pulled:

**Build immediately (KD 0–10):**
- Yes/No wheel (KD 8) — tweetsy.io
- Gamertag generator (KD 0) — tweetsy.io
- Rap name generator (KD 0) — tweetsy.io
- Markup calculator (KD 1) — ecomstudio.ai
- Bonus tax calculator (KD 0) — supatax.ai
- No tax on overtime calculator (KD 9) — supatax.ai
- CPM calculator (KD 7) — crazyads.io
- CTR/ROAS calculators (KD 0) — crazyads.io
- AI content detector (KD 2) — mailtoon.io
- Essay title generator (KD 0) — mailtoon.io
- Page speed checker (KD 0) — suparank.co
- Sitemap checker (KD 3) — suparank.co

**Build second (KD 11–25):**
- Instagram caption generator (KD 4) — tweetsy.io
- IRR calculator (KD 0) — ecomstudio.ai
- Etsy fee calculator (KD 6) — ecomstudio.ai
- YouTube earnings calculator (KD 2) — crazyads.io
- MX record checker (KD 25) — maillead.io
- Domain age checker (KD 24) — serpapis.com
- Redirect path checker (KD 14) — serpapis.com

---

## The Opportunity Score Formula

We use this to rank tool opportunities across the 8 sites:
**Opportunity Score = Volume ÷ (KD + 1)**

Higher score = better opportunity. Used in all our DataForSEO keyword research.

Example:
- Yes/No wheel: 201,000 ÷ (8+1) = 22,333 ← highest opportunity in the network
- Markup calculator: 22,200 ÷ (1+1) = 11,100 ← second highest
- No tax on overtime: 201,000 ÷ (16+1) = 11,824 ← third highest

---

## SERP Analysis Before Building (from Ahrefs)

Before spending time building any tool, check the actual SERP:
1. What type of content ranks? (If it's all tools, you must build a tool)
2. What are the DR/backlink profiles of competing pages? (Tells you real competition)
3. Are the top results from small independent sites or large brands? (Small = more beatable)
4. Is there a featured snippet or PAA box? (Win these with structured FAQs)

For KD 0 keywords: the SERP is often dominated by low-quality or old pages. This is the opportunity — replace them with something better.

For KD 0 on `bonus tax calculator`: means top-ranking pages have almost no backlinks. A well-built tool page on a site with DR 20+ topical relevance should rank within weeks.
