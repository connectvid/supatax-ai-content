---
skill: 14-technical-nextjs
description: Next.js 15 technical SEO implementation. Updated with real mistakes from wyomingllc.co. Load for all Next.js builds.
version: 2.0.0
last-verified: 2026-03
source: wyomingllc.co lessons + Ahrefs Technical SEO Guide (Aug 2025) + Next.js 15 docs
---

# Skill 14: Technical SEO — Next.js Implementation

## The Most Expensive Technical Mistakes (From Real Project)

[WYOMING LESSON 1] **Trailing slash inconsistency** — required fixing 21 URL patterns across 200+ files. Set `trailingSlash: true` in next.config.mjs on Day 1, never change.

[WYOMING LESSON 2] **Client-side only links on homepage** — Google crawler saw zero links to content pages. ALL navigation must be server-rendered. Test with curl.

[WYOMING LESSON 3] **Static sitemaps conflicting with dynamic** — 521 phantom URLs blocking real pages. Use ONLY `app/sitemap.ts`. Delete all static XML files.

[WYOMING LESSON 4] **Generic schema across all pages** — all had `headline: "Wyoming LLC Guide"`. Every page needs unique schema. Schema headline = H1 exactly.

[WYOMING LESSON 5] **No custom 404 page** — 8 broken pages with 26 links pointing to them. Always build `app/not-found.tsx` before launch.

---

## Day 1 Configuration — next.config.mjs

Set ALL of this before writing any content. Never change trailingSlash after launch.

```javascript
const nextConfig = {
  trailingSlash: true,  // PICK ONE AND NEVER CHANGE AFTER LAUNCH

  images: {
    formats: ['image/avif', 'image/webp'],
    deviceSizes: [640, 750, 828, 1080, 1200],
    remotePatterns: [], // add external image domains here
  },

  compress: true,

  async redirects() {
    return [
      // Set up ALL synonym redirects here on Day 1
      // Example for itin.so:
      { source: '/get-itin', destination: '/apply/', permanent: true },
      { source: '/obtain-itin', destination: '/apply/', permanent: true },
      { source: '/itin-application-online', destination: '/apply/', permanent: true },
    ];
  },

  async headers() {
    return [
      {
        source: '/(.*)',
        headers: [
          { key: 'X-DNS-Prefetch-Control', value: 'on' },
          { key: 'Strict-Transport-Security', value: 'max-age=63072000; includeSubDomains; preload' },
          { key: 'X-Content-Type-Options', value: 'nosniff' },
          { key: 'X-Frame-Options', value: 'DENY' },
          { key: 'X-XSS-Protection', value: '1; mode=block' },
          { key: 'Referrer-Policy', value: 'strict-origin-when-cross-origin' },
        ],
      },
      {
        source: '/(.*)\\.(js|css|png|jpg|gif|svg|woff|woff2)',
        headers: [
          { key: 'Cache-Control', value: 'public, max-age=31536000, immutable' },
        ],
      },
    ];
  },
};

export default nextConfig;
```

---

## Dynamic Sitemap — app/sitemap.ts

CRITICAL: Use real file modification times. Never use `new Date()`.
CRITICAL: ONE sitemap source only — delete any static XML files in /public/.

```typescript
import { MetadataRoute } from 'next'
import fs from 'fs'
import path from 'path'

// Pages to EXCLUDE from sitemap (noindex pages)
const NOINDEX_SLUGS = [
  '/api',
  '/components',
  '/lib',
  '/thank-you',
  '/lp-google',
]

// Hub pages get higher priority
const HIGH_PRIORITY_SLUGS = [
  '/',
  '/apply/',
  '/what-is-itin/',
  '/how-to-get-itin-number/',
  '/who-needs-itin/',
  '/what-can-you-do-with-itin/',
  '/itin-vs-ein/',
]

function getPageFiles(dir: string, baseDir: string): string[] {
  const files: string[] = []
  const items = fs.readdirSync(dir)

  for (const item of items) {
    const fullPath = path.join(dir, item)
    const stat = fs.statSync(fullPath)

    if (stat.isDirectory()) {
      files.push(...getPageFiles(fullPath, baseDir))
    } else if (item === 'page.tsx' || item === 'page.ts') {
      const relativePath = fullPath
        .replace(baseDir, '')
        .replace('/page.tsx', '')
        .replace('/page.ts', '') || '/'
      files.push(relativePath)
    }
  }
  return files
}

export default function sitemap(): MetadataRoute.Sitemap {
  const appDir = path.join(process.cwd(), 'app')
  const pages = getPageFiles(appDir, appDir)

  return pages
    .filter(slug => !NOINDEX_SLUGS.some(noindex => slug.startsWith(noindex)))
    .map(slug => {
      const pagePath = path.join(appDir, slug === '/' ? '' : slug, 'page.tsx')
      const stat = fs.existsSync(pagePath) ? fs.statSync(pagePath) : null

      return {
        url: `https://yourdomain.com${slug}`,
        lastModified: stat ? stat.mtime : new Date(),
        changeFrequency: slug === '/' ? 'daily' : 'weekly',
        priority: HIGH_PRIORITY_SLUGS.includes(slug) ? 0.9 : 0.7,
      }
    })
}
```

---

## robots.ts — Block Non-Content Paths

```typescript
import { MetadataRoute } from 'next'

export default function robots(): MetadataRoute.Robots {
  return {
    rules: {
      userAgent: '*',
      allow: '/',
      disallow: ['/components/', '/lib/', '/api/', '/lp-google/'],
    },
    sitemap: 'https://yourdomain.com/sitemap.xml',
  }
}
```

**NEVER block AI crawlers.** GPTBot, ClaudeBot, PerplexityBot must be allowed.

---

## Server-Side Rendering Verification

[WYOMING LESSON] The homepage had client-side only links. Google saw nothing.

After every deployment:
```bash
curl -s https://yourdomain.com/ | grep 'href="/'
```

Every important page must appear in this output. If not: critical bug.

Required server-rendered in every layout:
- Navbar links to all hub pages
- Footer links to all hubs + legal + contact
- All CTA buttons with href attributes

---

## Metadata Template — Every Page Unique

```typescript
export const metadata: Metadata = {
  title: 'Primary Keyword — Brand Name',  // ≤60 chars
  description: 'Unique description matching page intent.',  // ≤155 chars

  alternates: {
    canonical: 'https://yourdomain.com/page-slug/',
    languages: {
      'en': 'https://yourdomain.com/page-slug/',
      'es': 'https://yourdomain.com/es/page-slug/',
    }
  },

  openGraph: {
    title: 'OG Title',
    description: 'OG Description',
    url: 'https://yourdomain.com/page-slug/',
    siteName: 'Brand Name',
    images: [{ url: '/og-page-slug.png', width: 1200, height: 630 }],
    type: 'website',
  },

  twitter: {
    card: 'summary_large_image',
    title: 'Twitter Title',
    description: 'Twitter Description',
    images: ['/og-page-slug.png'],
  },

  robots: {
    index: true,
    follow: true,
    googleBot: { index: true, follow: true, 'max-image-preview': 'large' },
  },

  verification: {
    google: 'ACTUAL_CODE_HERE',  // Never leave placeholder
  },
}
```

---

## Required Components — Build Before Any Content Page

[WYOMING LESSON] We built content first, components later. This is backwards.

Build these FIRST, before any content:

1. **Navbar** — server-rendered `<Link>` components to all hubs
2. **Footer** — server-rendered links to hubs + legal + contact
3. **StickyCTA** — floating button with WhatsApp + primary CTA
4. **FloatingWhatsApp** — always-visible bottom-right button
5. **FAQSection** — renders FAQ visually + generates FAQPage JSON-LD automatically
6. **Breadcrumbs** — renders visual + generates BreadcrumbList JSON-LD automatically
7. **PricingTable** — transparent breakdown component (use on every pricing mention)
8. **TrustBar** — client count, rating, guarantee
9. **LastUpdated** — shows content freshness date
10. **TableOfContents** — auto-generated from H2s

---

## Dynamic Routes (Use for Pattern Pages)

[WYOMING LESSON] We created 358 individual page directories for country/state/profession pages. This created file bloat and maintenance nightmare.

Instead:
```
app/
  itin-for/
    [audience]/
      page.tsx      ← generateStaticParams() renders all audience pages
```

```typescript
export async function generateStaticParams() {
  return [
    { audience: 'amazon-sellers' },
    { audience: 'freelancers' },
    { audience: 'real-estate-investors' },
    // etc.
  ]
}
```

---

## Pre-Launch Technical Checklist

### Day 1 (Before Any Content)
- [ ] `trailingSlash: true` in next.config.mjs
- [ ] All synonym redirects defined
- [ ] Security headers configured
- [ ] `app/sitemap.ts` with real file modification times
- [ ] `app/robots.ts` (no static robots.txt)
- [ ] No static XML sitemaps in /public/
- [ ] `app/not-found.tsx` custom 404 page
- [ ] GSC verification code — real code, not placeholder
- [ ] Analytics: GA4 + Plausible + Microsoft Clarity

### Before First Content Page
- [ ] All 10 required components built
- [ ] Navbar verified server-rendered via curl
- [ ] Footer verified server-rendered via curl
- [ ] Run: `curl -s https://domain.com/ | grep 'href="/'` — confirms links visible

### After Every Deployment
- [ ] Verify sitemap.xml is accessible and complete
- [ ] Verify robots.txt is correct
- [ ] Test all new pages have: title, meta, canonical, OG, schema
- [ ] Run Lighthouse on 3 key pages (target: 90+)
- [ ] Verify no new 404s: audit href= values against existing pages
