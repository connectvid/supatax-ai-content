---
name: internal-linking
description: Apply when adding navigation links, footer links, breadcrumbs, contextual links in content, Related Tools sections, or verifying server-rendered links via curl. Triggers on: internal link, footer, breadcrumb, Related Tools, anchor text, server-rendered link, curl grep href.
---
# Skill 08: Internal Linking
## Source: Ahrefs "Internal Links for SEO: An Actionable Guide" (Aug 2023) + SEO Basics

---

## Why Internal Links Are Critical (from Ahrefs)

John Mueller, Google: "Internal linking is super critical for SEO. It's one of the biggest things you can do on a website to guide Google and visitors to the pages that you think are important."

Ahrefs data: "Pages with at least one exact match anchor text internal link had at least 5x more traffic than pages without."

Internal links do three things:
1. Help Google find new pages — if a page has no internal links pointing to it, Google may never find it
2. Pass PageRank — "Generally speaking, the more internal links a page has, the higher its PageRank." (Ahrefs)
3. Tell Google what a page is about — through anchor text context

"Google still uses PageRank as a signal after 18+ years." — Gary Illyes, Google (cited by Ahrefs)

---

## The Critical Rule: Server-Rendered Links Only

This is the lesson from wyomingllc.co. Repeat: NEVER again.

The wyomingllc.co homepage had ZERO crawlable internal links because they were rendered with JavaScript only. Googlebot could not follow them. Pages were published but never indexed.

**The rule:** Every internal link that Google needs to follow MUST appear in the initial server-rendered HTML.

Verify after every deployment:
```bash
curl -s https://yourdomain.com/ | grep 'href="/'
```

Every important page URL must appear in this output.
If a URL is missing — Google cannot crawl to it.

**In Next.js App Router:**
- Server components render links server-side ✓
- `"use client"` components render links client-side only ✗

Navigation, footer, and category hub links: always in server components.
Tool widget interactions: fine in client components — these don't need to be crawled.

---

## Types of Internal Links (from Ahrefs)

### 1. Navigational Links (Header/Menu)
"Most visitors find their way around using your site navigation. These are some of the most important internal links on your website." — Ahrefs

Always server-rendered. Links to homepage, main category pages, key tool pages.

### 2. Contextual Links (Body Content)
"Links in the main body of content. Used to expand on ideas, refer to resources, or direct readers to relevant content." — Ahrefs

3–5 contextual links per page is appropriate. More than 5 dilutes the signal.
Use when a related concept is mentioned: "To calculate your gross profit margin, use our [gross margin calculator]."

### 3. Breadcrumb Links
"Google treats them as normal links in PageRank computation." — Gary Illyes, Google (cited by Ahrefs)

Implement breadcrumbs on every tool page:
```tsx
// Breadcrumb on markup calculator page
<nav aria-label="Breadcrumb">
  <ol>
    <li><a href="/">Home</a></li>
    <li><a href="/calculators/">Calculators</a></li>
    <li>Markup Calculator</li>
  </ol>
</nav>
```

### 4. Footer Links
"Typical links: contact page, privacy policy, and other important pages." — Ahrefs

Footer is ALWAYS server-rendered. Use it for comprehensive link coverage:
- Links to all tool category hubs
- Links to About, Contact, Privacy Policy
- Site name/logo linked to homepage

---

## Anchor Text Rules (from Ahrefs)

Ahrefs data: "URLs with a larger number of anchor text variations are highly correlated with more Google search traffic."

Best practices:
- Use descriptive anchor text that matches the target page's primary keyword
- Vary anchor text naturally — don't always use exact-match
- Never use "click here", "learn more", "here" as anchor text
- The anchor text tells Google what the linked page is about

Examples:
Good: `<a href="/markup-calculator/">markup calculator</a>`
Good: `<a href="/markup-calculator/">calculate your markup percentage</a>`
Good: `<a href="/markup-calculator/">free markup tool</a>`
Bad: `<a href="/markup-calculator/">click here</a>`
Bad: `<a href="/markup-calculator/">this</a>`

---

## The Internal Linking Workflow

### When Publishing a New Tool Page:
1. Add the new tool to the site footer
2. Add the new tool to its category hub page (if exists)
3. Find 2 existing pages where this tool is mentioned or relevant
4. Add a contextual link from those pages to the new tool
5. Verify the new page appears in `curl -s https://yourdomain.com/ | grep href`

### When a Site Has 6+ Tools:
1. Create a category hub page (e.g., /calculators/)
2. Move tool links from homepage to hub (or link to hub from homepage)
3. Every tool page links back to its hub with descriptive anchor text
4. Hub page links to all tools in the cluster

### Finding Internal Link Opportunities:
Ahrefs recommends: Search your own site for mentions of a topic, then add links to the relevant page.

In Next.js projects: use VSCode "Find in Files" to search for mentions of a tool name across all .tsx/.md files, then add links where the concept is mentioned but not linked.

---

## Internal Linking Checklist

**Per new page published:**
- [ ] Page linked from footer (server-rendered)
- [ ] Page linked from category hub or homepage
- [ ] Page linked from 2 existing related pages with descriptive anchor text
- [ ] Breadcrumb navigation on the page
- [ ] Page has 2–4 outbound internal links to related tools
- [ ] Page appears in curl output of homepage

**Per site (verify monthly):**
- [ ] No orphan pages (pages with zero internal links pointing to them)
- [ ] Footer links to all major tools — server-rendered
- [ ] Homepage links to all category hubs or key tools
- [ ] All internal links use descriptive anchor text
- [ ] No "click here" or "learn more" anchor text
