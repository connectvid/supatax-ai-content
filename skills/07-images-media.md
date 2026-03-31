---
name: images
description: Apply when adding any image, screenshot, OG image, alt text, Next.js Image component, opengraph-image.tsx, or configuring image formats in next.config.js. Triggers on: image, alt text, OG image, opengraph-image, screenshot, WebP, AVIF, priority prop, width height.
---
# Skill 07: Images
## Source: Ahrefs "Image SEO: 12 Actionable Tips" + Alt Text Guide + Google Image Best Practices

---

## Why Images Matter for SEO (from Ahrefs)

"Google Images is the world's second-largest search engine. It's responsible for 20.45% of all online searches." — Ahrefs

"Images are often the largest contributor to overall page size, which can make pages slow and expensive to load." — Google (cited by Ahrefs)

"Images without dimensions" is the #1 cause of Cumulative Layout Shift (CLS) — a Core Web Vital that affects rankings.

Every tool page must have at least one image. Zero images = worse rankings and worse CLS performance.

---

## Rule 1: Always Use Next.js Image Component

Never use plain `<img>` tags. Next.js `<Image>` component:
- Automatically serves WebP/AVIF (faster loading)
- Prevents layout shift when width/height are set
- Handles lazy loading by default
- Responsive by default

```tsx
import Image from 'next/image'

// CORRECT
<Image
  src="/markup-calculator-example.png"
  alt="Markup calculator showing 50% markup on a $10 cost price resulting in $15 selling price"
  width={800}   // ALWAYS set
  height={450}  // ALWAYS set — prevents CLS
  loading="lazy"  // Default, but be explicit
/>

// Hero/above-fold images only:
<Image
  src="/tool-hero.png"
  alt="..."
  width={800}
  height={450}
  priority={true}  // Preloads the image — faster LCP
/>
```

Set `priority={true}` only on the FIRST image visible on page load. All other images use default lazy loading.

---

## Rule 2: Descriptive File Names (from Ahrefs)

"The filename can give Google clues about the subject matter of the image." — Google (cited in Ahrefs Image SEO guide)

Ahrefs example: `my-new-black-kitten.jpg` is better than `IMG00023.JPG`.

Google cannot perfectly identify all images — even with machine learning, Google identified butter as cheese with 91% confidence. Help Google understand with descriptive names.

**Format:** `{tool-name}-{description}.{ext}`

Good:
- `markup-calculator-example.png`
- `yes-or-no-wheel-result.png`
- `overtime-tax-calculator-result.png`

Bad:
- `image1.png`
- `screenshot.jpg`
- `IMG_0045.jpg`
- `tool.png`

---

## Rule 3: Alt Text Rules (from Ahrefs + Google)

"Google uses alt text along with computer vision algorithms and the contents of the page to understand the subject matter of the image." — Google

John Mueller: "Alt text is extremely helpful for Google Images — if you want your images to rank there."

**The Ahrefs shortcut formula:**
Finish this sentence: "This is a(n) image/screenshot/photograph of ___________."
Remove "This is a/an image/screenshot/photograph of" and use the rest as alt text.

Examples:
- "This is a screenshot of **a markup calculator showing 50% markup on a $10 product resulting in $15 selling price**"
→ alt: `Markup calculator showing 50% markup on a $10 product resulting in $15 selling price`

- "This is a screenshot of **the yes or no wheel spinner landing on YES**"
→ alt: `Yes or no wheel spinner landing on YES`

**Rules:**
- Include primary keyword naturally — not keyword stuffed
- Maximum 125 characters
- Do NOT use "image of" or "photo of" as prefixes
- Do NOT use empty alt on meaningful images
- Use empty `alt=""` ONLY for decorative images that add no information
- Do NOT stuff multiple keywords: `alt="markup calculator free markup tool percentage calculator"` — this is spam

---

## Rule 4: Image Formats (from Ahrefs)

Ahrefs guidance: Different formats for different image types.
- **JPEG**: Photographs and images with gradients — smallest file size for photos
- **PNG**: Screenshots, images with text, transparent backgrounds — lossless, stays crisp
- **GIF**: Animated images only
- **WebP/AVIF**: Modern formats, superior compression — let Next.js handle conversion

With Next.js and AVIF/WebP enabled in next.config.js, store source images as PNG or JPEG and Next.js converts them automatically.

```js
// next.config.js — enable this on every project
module.exports = {
  images: {
    formats: ['image/avif', 'image/webp']
  }
}
```

---

## Rule 5: Image Sizing — Prevent CLS

"Resize and upload images in the maximum width you need." — Ahrefs Image SEO Guide

For Next.js tool pages: content width is typically 680–720px. No need for images wider than 800px. Uploading 2000px images that display at 800px wastes bandwidth.

Process for tool screenshots:
1. Build the tool with realistic example inputs
2. Take screenshot at 1600px browser width
3. Crop to just the tool widget (no browser chrome)
4. Resize to 800px width (2x for retina: store at 1600px, display at 800px)
5. Save as PNG for screenshots with text, JPEG for photos
6. Store in `/public/images/` with descriptive filename

---

## Rule 6: OG Images (Required on Every Page)

Open Graph images make social shares look professional. Meta descriptions now influence AI citation selection — OG images influence click-through rates from AI summaries and social platforms.

Generate programmatically using Next.js ImageResponse:
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
        <div style={{ fontSize: 24, color: '#60A5FA', marginBottom: 16, textTransform: 'uppercase', letterSpacing: '0.1em' }}>
          EcomStudio · Free Tool
        </div>
        <div style={{ fontSize: 80, fontWeight: 800, color: 'white', textAlign: 'center', lineHeight: 1.1 }}>
          Markup Calculator
        </div>
        <div style={{ fontSize: 32, color: '#94A3B8', marginTop: 24 }}>
          Instant · Free · No Signup
        </div>
      </div>
    ),
    { ...size }
  )
}
```

Create one `opengraph-image.tsx` file per tool page. Next.js auto-uses it as og:image.

---

## Image Checklist Per Tool Page

- [ ] At least 1 tool screenshot showing realistic example inputs and outputs
- [ ] OG image created via opengraph-image.tsx (1200×630)
- [ ] All images use Next.js `<Image>` component (not plain `<img>`)
- [ ] All images have explicit `width` and `height` attributes
- [ ] All images have descriptive alt text including primary keyword
- [ ] Image filenames are descriptive (not image1.png)
- [ ] Hero/first image has `priority={true}` — all others lazy load
- [ ] AVIF/WebP enabled in next.config.js
- [ ] Screenshots are at appropriate width (800–1600px max)
- [ ] No decorative images with meaningful alt text (use `alt=""` for pure decoration)
