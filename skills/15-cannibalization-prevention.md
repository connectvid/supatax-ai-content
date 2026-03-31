---
skill: 12-cannibalization-prevention
description: Preventing and fixing keyword cannibalization. Updated with real wyomingllc.co cannibalization clusters. Most critical skill to read before creating any new page.
version: 2.0.0
last-verified: 2026-03
source: wyomingllc.co real cannibalization audit + Ahrefs
---

# Skill 12: Cannibalization Prevention

## The Real Cost of Not Following This

[WYOMING LESSON] We created 7 major cannibalization clusters on wyomingllc.co:
- **Banking:** 20 pages competing for "bank account for Wyoming LLC" — 9 hub-level pages competing with each other
- **Cost:** 3 pages (cost, cost-breakdown, pricing) all targeting "Wyoming LLC cost"
- **Tax:** 8 overlapping pages
- **EIN:** 4 pages, 2 very thin
- **Annual Report:** 3 near-identical pages
- **Stripe:** 3 pages, 2 on same topic
- **State Comparisons:** 3 dangerously thin competing pages

Fixing this required: merging pages, 301 redirects, noindexing duplicates. Weeks of rework.

**Prevention is 10x easier than cleanup. Map everything first.**

---

## The One Rule That Prevents Everything

**Before creating any page, check: does another page on this site already target this keyword or intent?**

Use 03-keyword-map.csv as the single source of truth.
If a keyword is already assigned to a URL, it CANNOT be the primary keyword for any other page.

---

## The Keyword-to-URL Registry

This is the most important file in the project. Keep it updated.

Every row:
```
Primary Keyword | Assigned URL | Secondary Keywords | Status
```

Before creating any page:
1. Search the registry for the keyword
2. Search the registry for similar keywords
3. Search the registry for same intent keywords
4. If any match exists: do NOT create a new page — add content to existing page

---

## The 5 Cannibalization Red Flags

Check before publishing any page:

1. **Two pages with similar H1 titles** — if H1s could be confused, they're competing
2. **Two pages targeting the same People Also Ask questions** — same PAA = same intent
3. **A page's meta description that could apply to another page** — too generic
4. **Content sections that repeat across pages** — merge or differentiate
5. **Multiple pages appearing for same query in Search Console** — check monthly

---

## How We Fixed Cannibalization on wyomingllc.co

These are the specific fixes — use as reference:

```
- cost-breakdown → cost (301 redirect, merge content)
- annual-fee → cost (301 redirect, merge content)
- annual-report-due-date → annual-report (301 redirect)
- 20 can-form-llc-[country] pages → main country pages (delete + redirect)
- 10 best-bank-[country] pages → noindex (64-71% duplicate content)
- 8 off-topic pages (ITIN, crypto, DeFi) → noindex (wrong domain)
- 60+ formation synonyms → single canonical URL with redirects
```

---

## Redirect Strategy for Synonyms

[WYOMING LESSON] We needed 60+ redirects post-launch because we didn't plan synonyms upfront.

For every site, BEFORE launch, brainstorm all action synonyms:

For itin.so:
```javascript
// In next.config.mjs redirects():
{ source: '/get-itin', destination: '/apply/', permanent: true },
{ source: '/obtain-itin', destination: '/apply/', permanent: true },
{ source: '/itin-number-application', destination: '/apply/', permanent: true },
{ source: '/itin-online', destination: '/apply/', permanent: true },
{ source: '/apply-itin', destination: '/apply/', permanent: true },
```

For wyomingllc.co (example):
```javascript
{ source: '/form-wyoming-llc', destination: '/form/', permanent: true },
{ source: '/create-wyoming-llc', destination: '/form/', permanent: true },
{ source: '/open-wyoming-llc', destination: '/form/', permanent: true },
{ source: '/start-wyoming-llc', destination: '/form/', permanent: true },
{ source: '/register-wyoming-llc', destination: '/form/', permanent: true },
```

---

## Expand vs Create Decision Tree

Before creating any new page, ask:

```
Is this topic a subtopic of an existing page?
  YES → Add as H2 section to existing page, not new page

Does it have <200/month search volume?
  YES → Add to most relevant existing page

Is it a long-tail variant of existing keyword?
  YES → Add to existing page targeting the parent keyword

Can I write 1,500+ unique words on this topic alone?
  NO → Merge into parent page

Does it cannibalize any existing page?
  YES → Do NOT create. Redirect the intent to existing page.

PASSES ALL CHECKS → Create new page
```

---

## Monthly Cannibalization Audit

Run this in GSC every month:

1. Go to Search Console → Performance
2. Look for queries where 2+ URLs are appearing
3. Look for queries ranking position 15-30 where you have a page targeting it — often means cannibalization is limiting the ranking
4. For any issue found: decide merge or redirect

---

## Content Differentiation Rules

When two pages are on related topics and can't be merged:

- Page A and Page B must target DIFFERENT primary keywords
- Page A must NOT answer the central question of Page B
- Page A and Page B link to each other contextually (not competitively)
- Each page has at least 60% unique content not found on the other

Example — itin.so:
- `/itin-application-status/` — "How to check ITIN application status"
- `/itin-application-tracking/` — "How to track ITIN application step by step"
These are similar but can be differentiated: status = checking codes, tracking = proactive monitoring steps.
