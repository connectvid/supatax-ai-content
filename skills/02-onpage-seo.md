---
name: onpage-seo
description: Apply when writing title tags, meta descriptions, H1 tags, URL slugs, Open Graph tags, heading structure, keyword placement, or any on-page optimization. Triggers on: title, meta description, H1, URL slug, heading, OG tag, keyword, on-page, SERP snippet.
---
# Skill 02: On-Page SEO
## Source: Ahrefs On-Page SEO Guide (Aug 2025) + On-Page SEO Checklist (March 2026)

---

## Core Principle (from Ahrefs)

"Small changes to your page can have a big impact on its rankings, traffic, and visibility in AI.
On-page SEO is like icing on a cake. To get the most from it, you need helpful, accurate
content that matches the intent of the keyword you're targeting." — Ahrefs On-Page SEO Guide

On-page SEO is not just for Google. Ahrefs (2026): "Many of the best practices that help you
rank well in search also help you appear in AI." Meta descriptions now influence whether
ChatGPT cites your page.

---

## 1. Title Tags

Ahrefs: "Title tags are often the main piece of information audiences use when deciding
whether to click on your site."

Google rewrites titles 61.6% of the time — but still uses your original title for ranking.
So write it well.

### The ABC Formula (from Ahrefs)
`Adjective + Benefit + Confidence Booster`

Example: "10 Easy SEO Tips for More Traffic (Tried and Tested)"
- Easy = Adjective
- for More Traffic = Benefit
- (Tried and Tested) = Confidence Booster

### Rules
- Under 70 characters to avoid truncation
- Include primary keyword or close variation
- Include year for freshness-sensitive topics: `Tax Calculator (2026)`
- Match search intent — tell searchers you have what they want
- Do not stuff keywords — one natural mention is enough
- Every indexable page must have a unique title tag

---

## 2. Meta Descriptions

Ahrefs: "Meta descriptions aren't a ranking factor, but they can bring more clicks."
Google uses them for snippets 37.22% of the time.

Critical 2026 update from Ahrefs: "ChatGPT selects the best source to cite based on:
URL → Title → Snippet (meta description) → Ranking position → Metadata"

Meta descriptions directly influence whether AI cites your page.

### Rules
- Under 160 characters
- Expand on the title tag — add information the title doesn't contain
- Match search intent — double down on what searchers want
- Use active voice, address the searcher directly
- Include primary keyword — Google bolds it in results
- End with a soft CTA or include "Free" / "No signup required"

---

## 3. H1 Tag

Ahrefs: "Use one H1 tag per page" — Google recommends this explicitly.
Most CMS/frameworks set H1 automatically — verify it is actually H1, not H2 or a div.

### Rules
- Exactly ONE H1 per page
- H1 must match or closely match the primary keyword
- H1 is the first heading visible on the page
- Do NOT put brand name in H1

---

## 4. Header Structure

Ahrefs: "Header tags help Google and AI assistants understand the content on your pages."

Structure:
```
H1 — Primary keyword / page title (one only)
  H2 — Major sections
    H3 — Sub-sections within H2
```

Ahrefs: "Make sure subheadings are clear and descriptive — not cryptic."
Test: can a reader understand what each section contains just by reading the subheadings?

For every tool page, minimum headers:
- H1: Tool name
- H2: How to use [Tool Name]
- H2: What is [concept]?
- H2: Frequently Asked Questions

---

## 5. Keywords in Content

Ahrefs: "SEO is not just about repeating one exact keyword anymore. It's about covering
topics comprehensively and matching what users are searching."

Where primary keyword must appear:
- Page title
- URL slug
- H1
- First paragraph (within first 100 words)
- At least one H2
- Image alt text
- Meta description

Ahrefs on AI visibility: "AI assistants prioritize content that covers subjects thoroughly."
Cover the topic completely, not just the exact keyword phrase.

### What to Avoid
- Never repeat the same keyword in back-to-back sentences
- Never bold keywords in body text for SEO purposes
- Never stuff keywords — Ahrefs warns against using on-page optimization tools blindly:
  "It's very easy to create content that's a nonsensical mish-mash of everyone else's content"

---

## 6. Get to the Point Fast

Ahrefs On-Page Checklist: "Don't kick things off with a load of fluff. Get straight to the
point and give the reader what they came for in the first sentence."

For tool pages: the tool widget itself is the answer. Put it first.
The supporting content (how it works, what the concept means) comes after.

Bad opening: "In this comprehensive guide, we'll walk you through everything you need to
know about markup calculations and how our free tool can help your business."

Good opening: "Enter your cost price and markup percentage below to calculate your selling
price instantly."

---

## 7. Open Graph Tags — Required on Every Page

Ahrefs (Jan 2026): Meta descriptions and OG tags influence AI citation decisions.

Every page needs:
```tsx
openGraph: {
  title: 'Page Title',
  description: 'Description under 160 chars',
  url: 'https://yourdomain.com/page-slug/',
  siteName: 'SiteName',
  images: [{ url: '...og-image.png', width: 1200, height: 630 }],
  type: 'website',
},
twitter: {
  card: 'summary_large_image',
  title: 'Page Title',
  description: 'Description',
  images: ['...og-image.png'],
}
```

OG image: 1200×630px, readable at small size, includes tool name.
Generate programmatically with Next.js `opengraph-image.tsx` on every tool page.

---

## 8. Content Freshness

Ahrefs: Include year in title for freshness-sensitive content. Update annually.
Add `Last updated: Month Year` to tool pages — especially calculators where rates change.

---

## On-Page Checklist Per Page (from Ahrefs March 2026)

- [ ] Short, descriptive URL using target keyword
- [ ] Compelling title tag (under 70 chars, ABC formula)
- [ ] Meta description (under 160 chars, expands on title)
- [ ] Title wrapped in H1 (only one H1 on page)
- [ ] Gets to the point in first sentence — no fluff intro
- [ ] Descriptive subheadings (H2, H3) that are clear without context
- [ ] Primary keyword in title, URL, H1, first paragraph, one H2
- [ ] Images have descriptive alt text with keyword
- [ ] OG tags set (og:title, og:description, og:image 1200×630)
- [ ] Canonical tag pointing to own URL
- [ ] Internal links to 2+ other relevant pages on same site
- [ ] Schema markup (FAQPage, SoftwareApplication, BreadcrumbList)
