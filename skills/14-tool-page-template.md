---
name: tool-page-template
description: Apply when building any new tool page from scratch. This is the master template with complete Next.js code. Triggers on: build tool page, new tool, page.tsx, create calculator, create generator, create checker, build tool.
---
# Skill 14: Tool Page Template — Complete Next.js Implementation
## This is the master template. Copy it for every new tool. Never deviate from the structure.

---

## File Structure for Every Tool

```
app/
  [tool-slug]/
    page.tsx              ← Main page (this template)
    opengraph-image.tsx   ← Auto-generated OG image
components/
  tools/
    [ToolName]Tool.tsx    ← Interactive tool widget (client component)
  JsonLd.tsx              ← Reusable schema component
```

---

## Complete page.tsx Template

```tsx
// app/markup-calculator/page.tsx
import type { Metadata } from 'next'
import Image from 'next/image'
import { JsonLd } from '@/components/JsonLd'
import { MarkupCalculatorTool } from '@/components/tools/MarkupCalculatorTool'

// ── Static generation (fast TTFB, better LCP) ────────────────────────────────
export const dynamic = 'force-static'

// ── SEO Metadata ─────────────────────────────────────────────────────────────
export const metadata: Metadata = {
  title: 'Markup Calculator: Selling Price from Cost + Margin (2026) | EcomStudio',
  description: 'Calculate your exact selling price from cost and markup percentage instantly. Free markup calculator — no signup required, works on mobile.',
  alternates: {
    canonical: 'https://ecomstudio.ai/markup-calculator/',
  },
  openGraph: {
    title: 'Markup Calculator — EcomStudio',
    description: 'Calculate selling price from cost and markup percentage instantly. Free, no signup.',
    url: 'https://ecomstudio.ai/markup-calculator/',
    siteName: 'EcomStudio',
    type: 'website',
  },
  twitter: {
    card: 'summary_large_image',
    title: 'Markup Calculator — EcomStudio',
    description: 'Calculate selling price from cost and markup percentage instantly. Free, no signup.',
  },
  robots: {
    index: true,
    follow: true,
    googleBot: { index: true, follow: true, 'max-image-preview': 'large' },
  },
}

// ── Schema Data ───────────────────────────────────────────────────────────────
const toolSchema = {
  "@context": "https://schema.org",
  "@type": "SoftwareApplication",
  "name": "Markup Calculator",
  "applicationCategory": "BusinessApplication",
  "operatingSystem": "Web Browser",
  "offers": { "@type": "Offer", "price": "0", "priceCurrency": "USD" },
  "description": "Free markup calculator. Enter cost price and markup percentage to calculate selling price instantly.",
  "url": "https://ecomstudio.ai/markup-calculator/",
}

const faqSchema = {
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What is the markup formula?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "The markup formula is: Selling Price = Cost Price × (1 + Markup%). For example, a $10 cost with 50% markup gives a $15 selling price. Markup is always calculated on the cost price, not the selling price."
      }
    },
    {
      "@type": "Question",
      "name": "What is the difference between markup and margin?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Markup is a percentage of the cost price. Margin is a percentage of the selling price. A 50% markup on a $10 item gives a $15 selling price. A 50% margin on a $10 item gives a $20 selling price. They produce different numbers."
      }
    },
    {
      "@type": "Question",
      "name": "How do I calculate markup percentage?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Markup percentage = ((Selling Price - Cost Price) ÷ Cost Price) × 100. If you bought something for $10 and sell it for $15, your markup is ((15-10)÷10)×100 = 50%."
      }
    },
    {
      "@type": "Question",
      "name": "What markup percentage should I use for retail?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Most retail businesses use 50–100% markup (known as keystone pricing). Wholesale businesses typically use 15–30%. Service businesses often use 200–500%. The right markup depends on your industry, overhead costs, and competition."
      }
    },
    {
      "@type": "Question",
      "name": "Is this markup calculator free?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Yes. This markup calculator is completely free with no signup, no account, and no hidden fees. Enter your cost price and markup percentage and your selling price calculates instantly."
      }
    },
  ]
}

const breadcrumbSchema = {
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://ecomstudio.ai/" },
    { "@type": "ListItem", "position": 2, "name": "Calculators", "item": "https://ecomstudio.ai/calculators/" },
    { "@type": "ListItem", "position": 3, "name": "Markup Calculator", "item": "https://ecomstudio.ai/markup-calculator/" },
  ]
}

// ── Page Component ─────────────────────────────────────────────────────────────
export default function MarkupCalculatorPage() {
  return (
    <>
      <JsonLd data={toolSchema} />
      <JsonLd data={faqSchema} />
      <JsonLd data={breadcrumbSchema} />

      <main>
        {/* BREADCRUMB — server-rendered, counted as internal links by Google */}
        <nav aria-label="Breadcrumb">
          <ol>
            <li><a href="/">Home</a></li>
            <li><a href="/calculators/">Calculators</a></li>
            <li>Markup Calculator</li>
          </ol>
        </nav>

        {/* H1 — matches primary keyword exactly */}
        <h1>Markup Calculator</h1>

        {/* ANSWER FIRST — one sentence, directly answers the search intent */}
        <p>
          Enter your cost price and markup percentage to instantly calculate your
          selling price, profit amount, and profit margin percentage.
        </p>

        {/* THE TOOL — must be the first interactive element, works with zero friction */}
        <MarkupCalculatorTool />

        {/* TOOL SCREENSHOT — shows example output, prevents CLS with explicit dimensions */}
        <Image
          src="/images/markup-calculator-example.png"
          alt="Markup calculator showing 50% markup on a $10 cost price resulting in $15 selling price and $5 profit"
          width={800}
          height={450}
          loading="lazy"
        />

        {/* SUPPORTING CONTENT — minimum 800 words total across all sections */}

        <section>
          <h2>How to Use the Markup Calculator</h2>
          <ol>
            <li>Enter your <strong>cost price</strong> — what you paid for the product or its production cost.</li>
            <li>Enter your <strong>markup percentage</strong> — the profit percentage you want to add over cost.</li>
            <li>The calculator instantly shows your <strong>selling price</strong>, <strong>profit amount</strong>, and <strong>margin percentage</strong>.</li>
            <li>Adjust either value to see results update in real time.</li>
          </ol>
        </section>

        <section>
          <h2>What is Markup?</h2>
          <p>
            Markup is the percentage added to a product's cost price to arrive at the selling price.
            It represents the profit as a percentage of the cost. A 50% markup means the profit is
            50% of the original cost.
          </p>

          <h3>The Markup Formula</h3>
          <p><strong>Selling Price = Cost Price × (1 + Markup%)</strong></p>
          <p>Example: Cost $10, Markup 50% → Selling Price = $10 × 1.5 = $15</p>

          <h3>Markup vs Margin — What's the Difference?</h3>
          <p>
            Markup and margin are often confused but they're different calculations.
            Markup is calculated on the <em>cost price</em>. Margin is calculated on the <em>selling price</em>.
            A 50% markup on a $10 item gives a $15 selling price (50% of $10 = $5 profit).
            A 50% margin on a $10 item gives a $20 selling price (50% of $20 = $10 profit).
            The same percentage produces very different results.
          </p>
        </section>

        <section>
          <h2>Frequently Asked Questions</h2>
          {/* Render FAQs visibly — schema alone is not enough, content must appear on page */}
          {faqSchema.mainEntity.map((faq, i) => (
            <div key={i}>
              <h3>{faq.name}</h3>
              <p>{faq.acceptedAnswer.text}</p>
            </div>
          ))}
        </section>

        {/* RELATED TOOLS — server-rendered internal links with descriptive anchor text */}
        <section>
          <h2>Related Calculators</h2>
          <ul>
            <li><a href="/gross-margin-calculator/">Gross Margin Calculator</a></li>
            <li><a href="/break-even-calculator/">Break-Even Point Calculator</a></li>
            <li><a href="/cogs-calculator/">COGS Calculator</a></li>
            <li><a href="/etsy-fee-calculator/">Etsy Fee Calculator</a></li>
          </ul>
        </section>
      </main>
    </>
  )
}
```

---

## opengraph-image.tsx Template

```tsx
// app/markup-calculator/opengraph-image.tsx
import { ImageResponse } from 'next/og'

export const runtime = 'edge'
export const alt = 'Markup Calculator — EcomStudio'
export const size = { width: 1200, height: 630 }
export const contentType = 'image/png'

export default async function Image() {
  return new ImageResponse(
    (
      <div style={{
        background: '#0F172A',
        width: '100%', height: '100%',
        display: 'flex', flexDirection: 'column',
        alignItems: 'center', justifyContent: 'center',
        fontFamily: 'sans-serif', padding: '80px',
      }}>
        <div style={{ fontSize: 22, color: '#60A5FA', marginBottom: 16,
          textTransform: 'uppercase', letterSpacing: '0.12em' }}>
          EcomStudio · Free Tool
        </div>
        <div style={{ fontSize: 76, fontWeight: 800, color: 'white',
          textAlign: 'center', lineHeight: 1.1 }}>
          Markup Calculator
        </div>
        <div style={{ fontSize: 30, color: '#94A3B8', marginTop: 24 }}>
          Cost + Margin → Selling Price · Instant · Free
        </div>
      </div>
    ),
    { ...size }
  )
}
```

---

## JsonLd Component (create once per project)

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

---

## Tool Widget Rules (ToolName.tsx)

The interactive widget is a `"use client"` component. Rules:
- Calculates purely client-side — zero API calls for math
- Shows example values pre-filled on load (helps user understand what to enter)
- Updates results on every keystroke — no submit button needed
- Works on mobile — touch-friendly inputs, readable font sizes
- Never requires signup, email, or any user data
- Handles edge cases: negative numbers, zero, very large numbers

```tsx
// components/tools/MarkupCalculatorTool.tsx
'use client'
import { useState } from 'react'

export function MarkupCalculatorTool() {
  const [cost, setCost] = useState('')
  const [markup, setMarkup] = useState('')

  const costNum = parseFloat(cost) || 0
  const markupNum = parseFloat(markup) || 0
  const sellingPrice = costNum * (1 + markupNum / 100)
  const profit = sellingPrice - costNum
  const margin = sellingPrice > 0 ? (profit / sellingPrice) * 100 : 0

  return (
    <div>
      <label>
        Cost Price ($)
        <input
          type="number"
          value={cost}
          onChange={(e) => setCost(e.target.value)}
          placeholder="10.00"
          min="0"
        />
      </label>
      <label>
        Markup (%)
        <input
          type="number"
          value={markup}
          onChange={(e) => setMarkup(e.target.value)}
          placeholder="50"
          min="0"
        />
      </label>
      {costNum > 0 && markupNum > 0 && (
        <div>
          <p>Selling Price: ${sellingPrice.toFixed(2)}</p>
          <p>Profit: ${profit.toFixed(2)}</p>
          <p>Margin: {margin.toFixed(1)}%</p>
        </div>
      )}
    </div>
  )
}
```

---

## Pre-Publish Checklist for Every Tool Page

**SEO:**
- [ ] URL slug = primary keyword (e.g., /markup-calculator/)
- [ ] H1 matches primary keyword
- [ ] Title tag: under 65 chars, includes year, includes keyword
- [ ] Meta description: 140–155 chars, keyword + CTA
- [ ] Canonical tag set to own URL
- [ ] `export const dynamic = 'force-static'` present
- [ ] robots: index, follow

**Content:**
- [ ] Answer in first sentence (no fluff intro)
- [ ] Tool is first visible interactive element
- [ ] 800+ words supporting content
- [ ] H2: How to Use
- [ ] H2: What is [Concept]
- [ ] H2: FAQ with 5+ visible Q&As
- [ ] H2: Related Tools with 3+ server-rendered internal links

**Technical:**
- [ ] OG image via opengraph-image.tsx
- [ ] Tool screenshot with explicit width + height
- [ ] All images have alt text including primary keyword
- [ ] FAQPage schema with 5+ Q&As
- [ ] SoftwareApplication schema
- [ ] BreadcrumbList schema
- [ ] Breadcrumb navigation rendered as HTML
- [ ] Validated with Rich Results Test

**Internal Linking:**
- [ ] Page in footer
- [ ] Page in category hub (if exists)
- [ ] 2+ existing pages link to this page
- [ ] Page visible in curl output of homepage
