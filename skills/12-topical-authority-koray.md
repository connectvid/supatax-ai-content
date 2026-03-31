---
name: topic-clusters
description: Apply when planning site architecture, creating category hub pages, structuring tool clusters, deciding what belongs on which site, or building pyramid link structure. Triggers on: topic cluster, site architecture, category hub, pillar page, topical boundary, site structure, pyramid.
---
# Skill 12: Topic Clusters and Site Architecture
## Source: Ahrefs "How to Build a Topic Cluster in 10 Minutes" + Internal Links Guide

---

## What Topic Clusters Are (from Ahrefs)

"Topic clusters are interlinked pages about a particular subject." — Ahrefs

Other names for the same thing: content hubs, pillar pages, hub and spoke. All mean the same thing: topically grouped pages designed to cover a subject and rank.

Three components:
1. A pillar page focused on the broad topic
2. A cluster of supporting pages covering related subtopics
3. Internal linking between all pages

---

## Why Topic Clusters Matter for Tool Sites

Ahrefs: "Topic clusters may help search engines see your site as an authority on a specific subject."

Google: "Design your site to have a clear conceptual page hierarchy." (Webmaster Guidelines)

For tool sites, the topic cluster structure is natural:
- Pillar: The site's home page or a category hub (e.g., "Free Ecommerce Calculators")
- Cluster: Individual tool pages (markup calculator, gross margin calculator, COGS calculator)
- Sub-cluster: Supporting content pages (what is markup, markup vs margin explained)

Each cluster tells Google: "This site is specifically about ecommerce calculations. Trust it for these queries."

---

## The Pyramid Structure (from Ahrefs Internal Links Guide)

John Mueller, Google: "The top-down approach or pyramid structure helps us a lot more to understand the context of individual pages within the site."

```
Homepage
├── Category Hub: Ecommerce Calculators
│   ├── Markup Calculator (tool)
│   ├── Gross Margin Calculator (tool)
│   ├── Break-Even Calculator (tool)
│   └── COGS Calculator (tool)
├── Category Hub: Shipping Tools
│   ├── UPS Shipping Calculator (tool)
│   ├── Dimensional Weight Calculator (tool)
│   └── Pallet Calculator (tool)
└── Category Hub: Fee Calculators
    ├── Etsy Fee Calculator (tool)
    ├── Amazon FBA Calculator (tool)
    └── Stripe Fee Calculator (tool)
```

Every tool links back to its category hub.
Every category hub links back to the homepage.
Homepage links to every category hub.
All links are server-rendered (visible in curl output).

---

## When to Create Category Hubs

Ahrefs guidance: Create hub pages when you have 6+ pages in the same topic cluster.

For sites starting out with 2–3 tools: Link directly from homepage to tool pages. No hub needed yet.

For sites with 6+ tools: Create category hub pages. These give Google a single page that establishes topical authority for the entire cluster.

Hub page format:
- H1: "Free [Category] Tools"
- Brief intro explaining what the tools are for
- Grid or list of all tools in the category with brief descriptions
- Each tool linked with descriptive anchor text

---

## Internal Linking Rules from Ahrefs (Critical)

John Mueller: "Internal linking is super critical for SEO. It's one of the biggest things you can do on a website."

Key Ahrefs data: "Pages with at least one exact match anchor text internal link had at least 5x more traffic than pages without."

### Rules

1. **Every new page gets at least one internal link pointing to it within 48 hours of publishing.**
   No orphan pages. Google cannot find pages it cannot crawl to.

2. **Use descriptive, exact-match anchor text wherever natural.**
   Good: `<a href="/markup-calculator/">markup calculator</a>`
   Bad: `<a href="/markup-calculator/">click here</a>`

3. **Link from high-traffic pages to new pages.**
   Pages with more traffic have more PageRank. Link from your best-performing page to your newest page.

4. **Maximum 3–5 contextual links in the body content of any single page.**
   More than this starts to dilute the signal. Footer links don't count toward this limit.

5. **Footer links must be server-rendered and link to all major tools.**
   Footer is always server-rendered in Next.js. Use it as your global internal link structure.

6. **Breadcrumbs are internal links.**
   Google treats breadcrumbs as normal links in PageRank computation. Implement on every tool page.

---

## Topic Cluster Architecture for the 8-Site Network

Each site has a clear topical focus. Never mix topics across sites (the wyomingllc.co violation).

| Site | Topical Cluster | Do Not Add |
|------|----------------|------------|
| ecomstudio.ai | Ecommerce tools, business calculators | Tax tools, social tools |
| tweetsy.io | Social generators, fun tools, random tools | SEO tools, email tools |
| supatax.ai | Tax calculators, payroll tools | Ecommerce tools |
| crazyads.io | Advertising calculators, creator tools | SEO tools |
| mailtoon.io | Email writing, content generators | Email validation, SEO |
| maillead.io | Email validation, outreach tools | Email writing |
| suparank.co | SEO tools, content analysis | Ads, email |
| serpapis.com | SERP data, technical web tools | Social, ecommerce |

If a tool idea doesn't fit the topical cluster — it goes on a different site or not at all. Topical dilution is the second most common indexation killer after JS-only internal links.

---

## Using Wikipedia for Topical Cluster Planning (Ahrefs Tip)

Ahrefs recommends using Wikipedia as a cluster planning tool:
"Wikipedia is the ultimate topic cluster. Every article fully covers a topic and interlinks between supporting subtopics."

For a new site, look up your niche on Wikipedia and:
1. Find all internal links on the main article — these are subtopics to consider
2. Look at the page structure — these sections are natural cluster pieces
3. Use the Related Articles section — these are adjacent clusters to potentially build later

For ecomstudio.ai: search Wikipedia for "markup (business)" to find all the subtopics worth covering.
For supatax.ai: search Wikipedia for "income tax" to find the subtopics.
