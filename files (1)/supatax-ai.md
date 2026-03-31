# supatax-ai.md
## Site Context Document — Read This Before Building Any Page

---

## WHAT THIS SITE IS

**Domain:** supatax.ai  
**CMS:** WordPress (SaaS Company theme by Ovation Themes)  
**Goal:** 5,000–6,000 Ahrefs organic traffic within 90 days — primarily for link selling (traffic + DR metrics matter most)  
**Owner:** Zawwad (zawwad@topslice.io)

---

## CURRENT SITE STATE

### Navigation
Home | Features | All Tools | Blog | Pricing

### Existing Pages (live)
| URL | Description |
|---|---|
| supatax.ai/ | Homepage — AI tax research SaaS product |
| supatax.ai/features/ | Features page |

| supatax.ai/blog/ | Blog index |
| supatax.ai/pricing/ | Pricing page |
| supatax.ai/about-us/ | About page |

### Existing Blog Posts (live — need interlink updates in Phase 1)
| URL | Title | Action Needed |
|---|---|---|
| /hello-world/ | "What Does IRS TREAS 310 Deposit Today Mean?" | Add I-node links → /tax-answers/irs-treas-310-tax-ref/ and /tax-answers/irs-treas-310/ |
| /what-is-tax-exempt-interest-income/ | "What Is Tax-Exempt Interest Income" | Add I-node links → /tax-answers/tax-exempt-interest-income/ and /tax-answers/taxable-interest/ |
| /does-florida-tax-social-security-why-retirees-love-the-sunshine-state/ | "Does Florida Tax Social Security?" | Add I-node links → /tax-answers/capital-gains-tax-florida/ and /tax-answers/does-california-tax-social-security/ |
| /how-to-calculate-tax-on-life-insurance-cash-surrender-value-complete-guide-with-examples-and-irs-insights/ | "How to Calculate Tax on Life Insurance Cash Surrender Value" | Add I-node links → /tax-answers/are-disability-benefits-taxable/ and /tax-answers/is-severance-pay-taxable/ |

---

## ⚠️ TOPICAL FOCUS REMINDER

**What supatax.ai covers:**
- US federal income tax Q&A
- State-specific tax rules (California, Florida, Tennessee focus)
- IRS processes and codes
- Tax deductions and eligibility
- AI-powered tax research and information

**What supatax.ai does NOT cover:**
- Non-tax AI tools or utilities
- General-purpose AI generators
- Non-tax software or services

**All content stays within the tax knowledge domain.** No external tool links, no off-topic references.

---

## URL ARCHITECTURE FOR NEW CONTENT

```
supatax.ai/tax-answers/           → Q&A hub page
supatax.ai/tax-answers/[slug]/    → Individual Q&A answer pages (primary traffic engine)
supatax.ai/guides/                → Pillar guide hub
supatax.ai/guides/[slug]/         → Individual pillar guides
```

### WordPress Implementation
- Create a **WordPress Page** named "Tax Answers" at slug `/tax-answers/`
- Create a **Custom Post Type** called `tax_answer` with URL structure `/tax-answers/%postname%/`  
  OR use a WordPress Page template with child pages under /tax-answers/
- Create a **WordPress Page** named "Guides" at slug `/guides/`
- Create individual guide pages as children of /guides/

---

## SOURCE CONTEXT

**What supatax.ai IS about (in Google's eyes we're building):**
- US federal income tax Q&A
- State-specific tax rules (California, Florida, Tennessee focus)
- IRS processes and codes
- Tax deductions and eligibility
- AI-powered tax research tools

**What supatax.ai is NOT about (topical borders — never publish):**
- Payroll software tutorials
- Accounting software (QuickBooks, Xero)
- International tax
- Business formation (LLC setup) — this is suparank.co territory
- Cryptocurrency tax in depth (mention in passing only)
- Immigration and tax
- Estate planning (mention deductibility rules only, not full estate planning)

---

## INTERNAL LINK RULES (STRICTLY FOLLOW)

Based on Koray Tuğberk GÜBÜR's I-node architecture:

1. **Header:** Links to homepage ONLY — no exceptions
2. **Footer:** Links to homepage ONLY — no exceptions
3. **Sidebar:** If exists — link to 5 most recent posts only
4. **Max 3 contextual I-node links per Q&A page** — in main body prose only
5. **Anchor text:** Near-exact match of the destination page's target keyword
6. **Annotation text:** The sentence surrounding the link must reinforce the semantic connection
7. **Each new page published:** Immediately go back and add 2 links FROM existing pages TO the new page
8. **Homepage direct links:** Only to /tax-answers/ hub, /guides/ hub, and top 3 highest-volume Q&A pages

### GOOD internal link example:
```
Homeowners insurance is not deductible for personal residences. 
If you're unsure about other property-related costs, our guide to 
[whether closing costs are tax deductible](/tax-answers/are-closing-costs-tax-deductible/) 
covers each line item from your settlement statement.
```

### BAD internal link example (DO NOT DO):
```
Click here to learn more. [Learn more](/tax-answers/are-closing-costs-tax-deductible/)
```

---

## CONTENT QUALITY STANDARDS

Every page must beat TaxGPT on at least ONE of these dimensions:

| Dimension | Required Standard |
|---|---|
| Tax year accuracy | Always reflect 2025 or 2026 tax year. Flag 2024 vs 2025 changes explicitly. |
| Answer immediacy | First 2 sentences answer the question — zero preamble, zero "In this article" |
| IRS form reference | Always name the specific IRS form when applicable (Form 1040, Schedule E, Form W-9, etc.) |
| Dollar/percentage specificity | Include exact rates, thresholds, and limits with the year (e.g., "24% flat rate for 2025") |
| State-specific note | Flag where state rules differ from federal, especially CA, NY, TX, FL |
| Edge case coverage | Cover at least one exception or edge case TaxGPT's equivalent page misses |
| Actionable Next Step | Clear guidance on what to do next (which form to file, deadline to meet, calculation to make) |

---

## SCHEMA REQUIREMENTS

### All Q&A Pages (/tax-answers/)
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "[H1 as a question]",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "[First paragraph — plain text, no HTML]"
    }
  }]
}
```
Also add: `Article`, `BreadcrumbList`

### Pillar Guides (/guides/)
```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "[H1]",
  "author": {
    "@type": "Person",
    "name": "Zawwad",
    "url": "https://supatax.ai/author/zawwad-ul-sami/"
  },
  "datePublished": "[ISO date]",
  "dateModified": "[ISO date]"
}
```
Also add: `FAQPage` (for FAQ section), `BreadcrumbList`

### Homepage
```json
{
  "@context": "https://schema.org",
  "@type": "WebApplication",
  "name": "SupaTax AI",
  "applicationCategory": "FinanceApplication",
  "offers": { "@type": "Offer", "price": "0", "priceCurrency": "USD" }
}
```
Also add: `Organization`, `FAQPage`

---

## COMPETITORS TO MONITOR

| Competitor | Domain | Notes |
|---|---|---|
| TaxGPT | taxgpt.com | Primary competitor. 5,510 keywords in our dataset. Their /answer/ pages = their traffic engine. |
| TurboTax | turbotax.intuit.com | High DR — don't compete on same KDs they own. Stick to KD ≤ 20. |
| H&R Block | hrblock.com | Same as TurboTax — avoid their core terms |
| IRS.gov | irs.gov | Government source — will rank above us for official procedure queries. Avoid. |
| NerdWallet | nerdwallet.com | High DR finance publisher — avoid their high-KD terms |

**TaxGPT Gap Strategy:** Where TaxGPT ranks position 8–20 on high-volume KD≤15 keywords = our priority targets. Their `/answer/` pages generate 6,422 traffic from 2,788 keywords = 2.3 traffic/page average. Our target: 30–40 traffic/page by targeting more precisely.

---

## WORDPRESS TECHNICAL NOTES

- **Permalink structure:** Set to `/%postname%/` for all post types
- **Sitemap:** Ensure Yoast SEO or Rank Math generates XML sitemap. Submit to GSC.
- **Robots.txt:** Block /wp-admin/, /wp-login.php. Block any non-tax content pages to preserve crawl budget for tax content.
- **Page speed:** Current theme (SaaS Company by Ovation Themes) is lightweight. Ensure no unnecessary JS plugins.
- **Author pages:** Ensure zawwad-ul-sami author page is visible and contains Person schema.

---

## TRAFFIC & DR TARGETS

| Metric | Current (estimated) | 30-day target | 60-day target | 90-day target |
|---|---|---|---|---|
| Ahrefs organic traffic | <500 | 1,000–1,500 | 2,500–3,500 | 5,000–6,000 |
| Ahrefs DR | Unknown | 15+ | 20+ | 25+ |
| Pages indexed | ~10 | 30+ | 60+ | 80+ |
| Keywords ranking top 20 | <20 | 40+ | 80+ | 120+ |
