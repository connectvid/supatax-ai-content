---
name: core-web-vitals
description: Apply when optimizing page speed, LCP, INP, CLS, image dimensions, static generation, tool widget performance, or PageSpeed scores. Triggers on: LCP, INP, CLS, Core Web Vitals, page speed, PageSpeed, layout shift, performance, force-static, priority image.
---
# Skill 10: Core Web Vitals
## Source: Ahrefs Core Web Vitals Guide by Patrick Stox (Jan 2025) + Google Search Central

---

## What Core Web Vitals Are (from Ahrefs)

Three metrics Google uses to measure user experience. Used as ranking signals since May 2021 (mobile) and February 2022 (desktop). In 2025, Google increased the weight of these signals.

| Metric | What It Measures | Good | Needs Work | Poor |
|--------|-----------------|------|------------|------|
| LCP | Largest visible element loads | ≤2.5s | 2.5–4s | >4s |
| INP | Response to user interactions | ≤200ms | 200–500ms | >500ms |
| CLS | Layout stability during load | ≤0.1 | 0.1–0.25 | >0.25 |

**INP replaced FID on March 12, 2024.** Any skill or guide still referencing FID is outdated.

Global pass rates as of early 2026: 68% pass LCP, 87% pass INP, 81% pass CLS. Only 56% pass all three. Your competition is better than you think.

---

## LCP — Largest Contentful Paint

"The amount of time it takes to load the single largest visible element in the viewport." — Ahrefs

The LCP element is usually:
- Hero/featured image
- H1 tag (when it's the largest element)
- Any `<img>` element
- Background image loaded with `url()` function

**Why it fails and how to fix it for Next.js tool sites:**

The most common LCP element on a tool page is either the H1 or the hero image. For tool pages, keep it simple — the H1 should be the LCP element, which means no large hero image above the fold.

Fixes:
- Use `priority={true}` on any above-fold image (tells Next.js to preload it)
- Use `export const dynamic = 'force-static'` on all tool pages — static pages = fast TTFB = fast LCP
- Never fetch external data server-side on tool pages — pre-render everything
- Enable AVIF/WebP in next.config.js — smaller files load faster

```js
// next.config.js
module.exports = {
  images: { formats: ['image/avif', 'image/webp'] }
}
```

---

## CLS — Cumulative Layout Shift

"Measures the visual stability of a page as it loads." — Ahrefs

Ahrefs on CLS causes:
- **Images without dimensions** — the #1 cause. Browser doesn't know how much space to reserve.
- Ads, embeds, and iframes without dimensions
- Injecting content with JavaScript after page load
- Applying fonts or styles late in the load

**The fix is non-negotiable:** Always set explicit `width` and `height` on every image.

```tsx
// CORRECT - browser reserves space before image loads
<Image
  src="/markup-calculator-example.png"
  alt="Markup calculator example"
  width={800}
  height={450}  // ALWAYS set this
/>

// WRONG - causes layout shift
<Image src="/example.png" alt="..." />  // No dimensions = CLS
```

For web fonts: use `font-display: swap` in CSS. This prevents invisible text during font load.

---

## INP — Interaction to Next Paint

"Measures how quickly a website responds to user interactions." — Ahrefs

Replaced FID in March 2024. Measures ALL user interactions throughout the page lifetime, not just the first one. Clicks, taps, keyboard inputs all count.

Target: ≤200ms for every interaction.

**Why this matters for tool sites:**
Tool pages are interactive by definition. When a user types into the markup calculator, the result must update in ≤200ms or Google considers the experience poor.

**The key cause:** JavaScript competing for the main thread. Long JS tasks block the page from responding.

Fixes for tool widgets:
- Calculate results client-side using plain JavaScript — no API calls for simple math
- Use `debounce` on input handlers — wait 150ms after user stops typing before calculating
- Don't load heavy libraries (lodash, moment.js) for simple calculations
- Keep the tool widget JS bundle small — split it from the rest of the page code

```tsx
// Fast client-side calculation - no API needed
function calculateMarkup(cost: number, markupPercent: number) {
  return cost * (1 + markupPercent / 100)  // Runs in microseconds
}
```

---

## How to Check Core Web Vitals

1. **PageSpeed Insights** (free) — pagespeed.web.dev — checks individual pages
   - Shows both lab data (Lighthouse) and field data (real Chrome users)
   - Field data is what Google actually uses for ranking

2. **Google Search Console** — Core Web Vitals report
   - Shows all pages grouped by issue type
   - Fix the issue in the template and it fixes all pages in the group

3. **Ahrefs Webmaster Tools** (free) — connects to PageSpeed Insights API
   - Shows CWV data at scale across all pages

**Lab vs Field data (from Ahrefs):**
- Field data: real Chrome users, what Google uses for ranking, 28-day rolling average
- Lab data: Lighthouse test, consistent conditions, useful for immediate feedback
- Changes take weeks to show in field data — use lab data to test your fixes

---

## CWV Quick Checklist for Every Tool Page

- [ ] LCP element identified (usually H1 or first image)
- [ ] If hero image exists: `priority={true}` set on the `<Image>` component
- [ ] ALL images have explicit `width` and `height` attributes
- [ ] Tool widget uses client-side calculation only (no API calls)
- [ ] No layout shifts from dynamic content injected after page load
- [ ] `export const dynamic = 'force-static'` on all tool pages
- [ ] AVIF/WebP enabled in next.config.js
- [ ] Font loading uses `font-display: swap`
- [ ] PageSpeed Insights score: Mobile 70+, Desktop 85+ before launch

---

## CWV and AI Visibility (2026)

From third-party analysis: 97% of sources cited in AI Overviews come from the top 20 organic results. Better CWV → better rankings → more likely to appear in AI answers.

The pipeline: Good CWV → better Google ranking → higher AI citation probability.

Google's official documentation states CWV are not direct criteria for AI Overviews selection — but they matter indirectly through organic rankings.
