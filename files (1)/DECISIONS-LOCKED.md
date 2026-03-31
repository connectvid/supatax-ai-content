# DECISIONS-LOCKED.md
## Non-Negotiable Decisions — Do Not Change Without Explicit Approval

These decisions are locked. They were made based on keyword data analysis, competitor gap analysis, and Koray Tuğberk GÜBÜR's Holistic SEO methodology. Do not modify these without explicit sign-off.

---

## DECISION 1: URL STRUCTURE
**Locked:** New Q&A pages go under `/tax-answers/[slug]/`  
**Locked:** Pillar guides go under `/guides/[slug]/`  
**Reason:** Creates clear content-type signal, groups semantically related pages under a common parent, enables /tax-answers/ hub to serve as a cluster index.  
**Do NOT change to:** `/blog/`, `/[slug]/` (flat root), `/qa/`, `/questions/`

---

## DECISION 2: PUBLICATION ORDER FOLLOWS 04-BUILD-ORDER.CSV
**Locked:** Pages must be built in the sequence specified in 04-build-order.csv.  
**Reason:** Each phase establishes topical authority at the micro level before building toward head terms. Publishing head-term pages before micro-topic pages is a confirmed negative ranking state trigger (Koray's research).  
**Do NOT change to:** Random order, alphabetical, or "highest volume first"  
**Exception allowed:** If Google Search Console shows a specific cluster gaining traction faster than expected, priority within that cluster's build order can be accelerated — but the cluster-first, guide-last sequence must be preserved.

---

## DECISION 3: MAX 3 I-NODE LINKS PER Q&A PAGE
**Locked:** Q&A pages contain a maximum of 3 contextual body links.  
**Reason:** Koray's I-node research shows that fewer links per page = more PageRank per link. Over-linking dilutes both source and destination.  
**Do NOT change to:** 5+ links per page, full link lists, or "Related Articles" widgets with 10+ links

---

## DECISION 4: HEADER AND FOOTER LINK TO HOMEPAGE ONLY
**Locked:** Site-wide nav header and footer must link only to the homepage.  
**Reason:** S-nodes (sitewide links) have minimal PageRank value per link. Every S-node link not going to the homepage is wasted signal.  
**Do NOT change to:** Header with 10 nav links, footer with all page links, sitewide "Popular Posts" widget

---

## DECISION 5: STRICT TOPICAL BORDERS — NO OFF-TOPIC CONTENT
**Locked:** All content stays within US tax knowledge domain. No links to non-tax content.  
**Reason:** Koray's Source Context rule — expanding beyond your established topical identity without proper contextual bridges destroys topical authority. Google cannot reconcile "tax AI" with "fanfiction generator" or other non-tax topics.  
**Action required:**  
1. No links from /tax-answers/ or /guides/ to any non-tax pages  
2. Focus 100% on tax Q&A content and pillar guides  
3. Build topical authority through content depth, not tool features

---

## DECISION 6: ALL Q&A PAGES USE FAQPAGE SCHEMA
**Locked:** Every /tax-answers/ page includes FAQPage JSON-LD schema with the H1 question as the main entity.  
**Reason:** FAQPage schema directly enables featured snippets and AI Overview appearances, which are the fastest path to high-CTR positions on low-KD informational queries.  
**Do NOT change to:** Skipping schema, using only Article schema, or manually adding FAQ sections without schema

---

## DECISION 7: TARGET KEYWORD SET IS KD ≤ 20 ONLY FOR FIRST 90 DAYS
**Locked:** No content targeting keywords with KD > 20 during phases 1–3.  
**Reason:** The 5–6K traffic goal in 90 days is only achievable via KD ≤ 20 keywords. High-KD keywords will not rank in time to contribute to the 90-day goal.  
**The one exception:** Homepage targets "ai tax preparation" (KD 52) because it's a commercial term and the homepage already exists.  
**Do NOT change to:** "Let's also write a 3,000-word guide about TurboTax alternatives" (KD 68)

---

## DECISION 8: GUIDES ARE PUBLISHED AFTER ALL Q&A PAGES IN THEIR CLUSTER ARE LIVE
**Locked:** The /guides/irs-treas-310/ pillar guide is published ONLY after all 4 IRS refund Q&A pages are live. Same rule for all other guides.  
**Reason:** Guides derive authority from the Q&A cluster they link to. Publishing a guide before the cluster exists means it has nowhere to send link equity. Also, it establishes topical authority at the micro level first — Koray's core rule.

---

## DECISION 9: AUTHOR = ZAWWAD ON ALL CONTENT
**Locked:** All content is attributed to the supatax.ai author "zawwad-ul-sami."  
**Reason:** Google's Author Rank patents track content quality signals per author entity. Consistent authorship builds an Author Rank signal over time. Mixing anonymous content with bylined content sends inconsistent signals.  
**Action required:** Ensure zawwad-ul-sami author page has full bio + Person schema markup.

---

## DECISION 10: EXISTING BLOG POSTS ARE UPDATED IN WEEK 1 (NOT DELETED)
**Locked:** The 4 existing blog posts at root URLs (/hello-world/, /what-is-tax-exempt-interest-income/, etc.) are kept and updated with I-node links in Week 1. They are NOT deleted or redirected.  
**Reason:** These posts represent existing historical data in Google's index. Deleting them removes any authority signals they've accumulated. Adding links from them to new Q&A pages turns them into PageRank sources.  
**Do NOT change to:** Delete old posts, redirect them to new Q&A pages, or ignore them.

---

## TRAFFIC PROJECTION (LOCKED ASSUMPTIONS)

These are the conservative projections used to validate the 5–6K goal. Do not expect faster results — but these ARE achievable.

| Page Type | Count | Avg Monthly Traffic/Page | Total |
|---|---|---|---|
| Tier 1 Q&A flagship pages | 15 | 150–400 | 2,250–6,000 |
| Tier 2 Q&A supporting pages | 35 | 20–60 | 700–2,100 |
| Pillar guides | 7 | 50–200 | 350–1,400 |
| Existing blog (with interlinks) | 4 | 20–60 | 80–240 |
| Homepage (commercial) | 1 | 100–300 | 100–300 |
| **TOTAL** | **62** | | **3,480–10,040** |

**Conservative target: 5,000. Realistic range: 4,500–7,000 at 90 days.**

---

*Last updated: 2026-03-31*  
*Approved by: Zawwad*  
*Do not modify without approval.*
