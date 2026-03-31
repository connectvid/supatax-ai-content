---
name: technical-seo
description: Apply when building any page, configuring robots.txt, sitemap, canonical tags, server rendering, Next.js dynamic/static settings, GSC setup, HTTPS, URL structure, or diagnosing crawling/indexing problems. Triggers on: robots, sitemap, canonical, crawl, index, noindex, GSC, server render, curl check, JavaScript links.
---
# Skill 01: Technical SEO
## Source: Ahrefs Technical SEO Guide (updated Aug 2025) + What AI Means for SEO (Jan 2026)

---

## Core Principle (from Ahrefs)

"Technical SEO is the most important part of SEO until it isn't. Pages need to be crawlable
and indexable to even have a chance at ranking, but many other activities will have minimal
impact compared to content and links." — Patrick Stox, Ahrefs

Priority order: Crawlable → Indexable → Content → Links.
If a page cannot be crawled and indexed, nothing else matters.

---

## Crawling

### Robots.txt
- Every site needs a robots.txt at /robots.txt
- Must include: `Sitemap: https://yourdomain.com/sitemap.xml`
- Default: `User-agent: * Allow: /`
- Do NOT block Googlebot or AI crawlers (GPTBot, Bingbot, etc.)
- Ahrefs: "If you block search engines and LLMs from using your website, you limit your
  chances of becoming visible in their responses"

### JavaScript — Critical Warning
Ahrefs (Jan 2026): "Most LLMs don't render JavaScript. If key content or navigation only
appears after JavaScript loads, there's a risk some AI crawlers won't see it."

Rule: ALL navigation links, footer links, and key internal links MUST be present in
server-rendered HTML — not reliant on JavaScript to appear.

Verify with:
```bash
curl -s https://yourdomain.com/ | grep 'href="/'
```
Every important page must appear in this output.

### Crawl Budget
- More popular and frequently updated pages get crawled more often
- Thin, duplicate, or unlinked pages waste crawl budget
- Never publish 50+ pages before establishing 3–5 quality indexed pages
- If "Crawled not indexed" grows faster than "Indexed" in GSC — STOP and diagnose

---

## Indexing

### Canonical Tags
Every page must have a self-referencing canonical. Ahrefs: canonicalization is how Google
selects which URL to index when duplicates exist.

```tsx
export const metadata = {
  alternates: { canonical: 'https://yourdomain.com/page-slug/' }
}
```

### Robots Meta Tag
Default for all pages:
```tsx
robots: { index: true, follow: true,
  googleBot: { index: true, follow: true, 'max-image-preview': 'large' } }
```
Only noindex: admin pages, thank-you pages, exact duplicates.

### Sitemap
- Generate dynamically in app/sitemap.ts
- Include ONLY indexable pages
- Submit to GSC on day 1
- Verify: `curl -s https://yourdomain.com/sitemap.xml | grep -c "<loc>"`

### GSC Verification
- Set up Google Search Console on day 1 of every site
- Use HTML tag method: `metadata.verification.google = 'ACTUAL_CODE'`
- NEVER leave placeholder text `your-google-verification-code`
- Submit sitemap immediately after verification

---

## Core Web Vitals (from Ahrefs On-Page SEO Guide, updated 2026)

Ahrefs: "In 2025, Google increased the weight of these signals."

- LCP (Largest Contentful Paint): under 2.5 seconds
- INP (Interaction to Next Paint): under 200ms — replaced FID in March 2024
- CLS (Cumulative Layout Shift): under 0.1

To hit targets:
- Set explicit width and height on ALL images (prevents CLS)
- Use `priority={true}` on above-fold images only
- Use `export const dynamic = 'force-static'` on tool pages
- Avoid layout shifts from dynamic content loading after render

---

## Technical SEO for AI Search (Ahrefs Jan 2026)

AI assistants (ChatGPT, Gemini, Perplexity, Claude) ground their responses using web search.
Sites that rank well in Google are more likely to appear in AI answers.

"Websites that rank highly for relevant topics in search engines are more likely to have
their pages retrieved and used by AI assistants." — Ahrefs, Jan 2026

What this means practically:
- Same technical SEO principles apply to both Google and AI visibility
- Do NOT block AI crawlers (GPTBot, Applebot, ClaudeBot, PerplexityBot)
- Keep navigation and key content in server-rendered HTML, not JS-only
- Fast, well-structured, crawlable pages = visible in both Google and AI

LLMs.txt: Ahrefs says "not especially effective and likely not worth the effort." Skip it.

---

## Redirects

Ahrefs: "Reclaiming lost links via redirects is the fastest link building you will ever do."

Rules:
- 301 redirect every deleted or moved page to the correct current URL
- Never delete a page without adding a redirect
- Never change a URL without adding a redirect from the old URL
- Check for 404 pages regularly — each one is a lost link and lost ranking signal

---

## HTTPS
- Every site must use HTTPS (SSL/TLS certificate)
- Vercel handles this automatically — nothing to configure
- Ahrefs: "HTTPS is a trust signal for both users and search engines"

---

## URL Structure (from Ahrefs)

Ahrefs recommends: short, descriptive, keyword-matching URLs.

Rules:
- Use target keyword as URL slug
- Lowercase only, hyphens between words
- No dates in URLs (`/2024/markup-calculator/` → `/markup-calculator/`)
- No IDs or random strings
- No word repetition (`/tools/markup-calculator-tool/` → `/markup-calculator/`)
- Consistent trailing slash — always use or never use
- Ahrefs (2026): "There are theories that keeping URLs short and clean can positively
  impact visibility in AI too"

Good: `/markup-calculator/`
Good: `/yes-or-no-wheel/`
Bad: `/tools/free-markup-calculator-2026/`
Bad: `/markup_calculator`
