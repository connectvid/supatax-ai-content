---
name: schema-markup
description: Apply when implementing any structured data, JSON-LD, FAQPage, SoftwareApplication, BreadcrumbList, Organization, or WebSite schema. Triggers on: schema, JSON-LD, structured data, rich results, FAQPage, BreadcrumbList, SoftwareApplication, Organization schema.
---
# Skill 06: Schema Markup
## Source: Ahrefs "Schema Markup: What It Is & How to Implement It" (Updated Sep 2023) + Technical SEO Guide

---

## What Schema Does (from Ahrefs)

"Schema markup is code that helps search engines understand the information on a page. Google can use it to show rich results (rich snippets), which can earn a page more clicks." — Ahrefs

"Schema markup may also help LLMs correctly interpret your page content." — Ahrefs Technical SEO Guide

Always use JSON-LD format. John Mueller, Google: "We currently prefer JSON-LD markup. Most new structured data comes out for JSON-LD first. So that's what we prefer."

**IMPORTANT — FAQPage Update (August 8, 2023):**
Ahrefs: "Google significantly reduced visibility for HowTo and FAQs rich results on August 8, 2023. FAQ results will now only be shown for well-known, authoritative government and health sites."

FAQPage schema still helps Google understand page structure and may help LLMs parse your content — but expect less visual rich result display in SERPs. Still include it on every tool page.

---

## How to Implement in Next.js

Create a reusable JsonLd component:
```tsx
// components/JsonLd.tsx
export function JsonLd({ data }: { data: object }) {
  return (
    <script
      type="application/ld+json"
      dangerouslySetInnerHTML={{ __html: JSON.stringify(data) }}
    />
  )
}
```

Place schema in the page component, not in layout. This allows different schema per page.
Google confirmed: schema can go in either `<head>` or `<body>`.

---

## Required Schema Per Page Type

### Every Site (add to root layout.tsx)

**Organization Schema:**
```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "EcomStudio",
  "url": "https://ecomstudio.ai",
  "logo": "https://ecomstudio.ai/logo.png",
  "sameAs": [
    "https://twitter.com/ecomstudio",
    "https://linkedin.com/company/ecomstudio"
  ]
}
```

**WebSite Schema:**
```json
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "EcomStudio",
  "url": "https://ecomstudio.ai"
}
```

---

### Every Tool Page

**SoftwareApplication Schema:**
```json
{
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "Markup Calculator",
  "applicationCategory": "BusinessApplication",
  "operatingSystem": "Web Browser",
  "offers": {
    "@type": "Offer",
    "price": "0",
    "priceCurrency": "USD"
  },
  "description": "Free markup calculator. Enter cost price and markup percentage to calculate selling price instantly.",
  "url": "https://ecomstudio.ai/markup-calculator/"
}
```

**FAQPage Schema (5+ Q&As minimum):**
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is the markup formula?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Selling Price = Cost Price × (1 + Markup%). A $10 cost with 50% markup gives a $15 selling price."
      }
    },
    {
      "@type": "Question",
      "name": "What is the difference between markup and margin?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Markup is calculated on the cost price. Margin is calculated on the selling price. A 50% markup on a $10 item gives $15. A 50% margin on a $10 item gives $20."
      }
    }
  ]
}
```

**BreadcrumbList Schema (every page except homepage):**
```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://ecomstudio.ai/"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Markup Calculator",
      "item": "https://ecomstudio.ai/markup-calculator/"
    }
  ]
}
```

---

## FAQ Schema Rules

1. Questions must exactly match how someone would type them in Google
2. First sentence of each answer directly answers the question
3. Answers: 2–4 sentences, 50–100 words each
4. FAQs must ALSO appear visibly on the page as rendered HTML — schema alone is not enough
5. Check Google's "People Also Ask" results for the target keyword to find the right questions
6. Validate at: https://search.google.com/test/rich-results after publishing

---

## Schema Validation (from Ahrefs)

Test every page's schema before considering it done:
1. Google's Rich Results Test: https://search.google.com/test/rich-results
2. Schema Validator: https://validator.schema.org/

These tools will show errors and warnings. Zero errors is the standard.

Common errors to watch for:
- Missing required properties (e.g., `offers` on SoftwareApplication)
- Invalid date formats
- Empty required fields
- Nested JSON syntax errors

---

## Schema Checklist Per Tool Page

- [ ] SoftwareApplication schema — price: "0", applicationCategory set
- [ ] FAQPage schema — 5+ Q&As, questions match actual search queries
- [ ] FAQs visible on page as HTML (not just in JSON-LD)
- [ ] BreadcrumbList schema — positions correct, URLs absolute
- [ ] Organization + WebSite schema in root layout (done once per site)
- [ ] Validated with Rich Results Test — zero errors
- [ ] JSON-LD format (not microdata or RDFa)
- [ ] Script tag type="application/ld+json"
