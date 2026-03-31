---
name: verification-script
description: Apply after every deployment to verify critical SEO rules were followed. Contains shell scripts to run. Triggers on: verify deployment, post-deploy check, pre-launch verification, curl check, SEO audit after build, did it work.
---

# Skill 19: Verification Scripts
## Run these after every deployment. No exceptions.

---

## Why Automated Verification Exists

The deployment checklist (skill 15) requires manual curl commands.
In practice: after the 3rd site, the manual checks stop happening.
These scripts make verification automatic and fast.

---

## The 60-Second Post-Deploy Verification

Create this file in every project: `scripts/verify-seo.sh`

```bash
#!/bin/bash
# SEO Verification Script
# Run after every deployment: bash scripts/verify-seo.sh https://yourdomain.com

DOMAIN="${1:-https://yourdomain.com}"
TOOL_SLUG="${2:-markup-calculator}"  # Pass your first tool slug as second arg
PASS=0
FAIL=0

echo ""
echo "=== SEO Verification: $DOMAIN ==="
echo ""

check() {
  local name="$1"
  local result="$2"
  local expected="$3"
  if [ "$result" -ge "$expected" ] 2>/dev/null || [ "$result" = "$expected" ] 2>/dev/null; then
    echo "  ✓ PASS — $name ($result)"
    PASS=$((PASS+1))
  else
    echo "  ✗ FAIL — $name (got: $result, expected: $expected)"
    FAIL=$((FAIL+1))
  fi
}

# 1. Homepage returns 200
STATUS=$(curl -s -o /dev/null -w "%{http_code}" "$DOMAIN/")
check "Homepage HTTP status" "$STATUS" "200"

# 2. robots.txt returns 200
ROBOTS=$(curl -s -o /dev/null -w "%{http_code}" "$DOMAIN/robots.txt")
check "robots.txt accessible" "$ROBOTS" "200"

# 3. robots.txt allows Googlebot
ROBOTS_ALLOW=$(curl -s "$DOMAIN/robots.txt" | grep -c "Allow")
check "robots.txt has Allow directive" "$ROBOTS_ALLOW" "1"

# 4. Sitemap returns 200
SITEMAP=$(curl -s -o /dev/null -w "%{http_code}" "$DOMAIN/sitemap.xml")
check "sitemap.xml accessible" "$SITEMAP" "200"

# 5. Sitemap has pages
SITEMAP_PAGES=$(curl -s "$DOMAIN/sitemap.xml" | grep -c "<loc>")
check "sitemap.xml has pages" "$SITEMAP_PAGES" "1"

# 6. Homepage has server-rendered internal links
INTERNAL_LINKS=$(curl -s "$DOMAIN/" | grep -c 'href="/')
check "Homepage has server-rendered internal links" "$INTERNAL_LINKS" "5"

# 7. Homepage has H1
HAS_H1=$(curl -s "$DOMAIN/" | grep -c '<h1')
check "Homepage has H1" "$HAS_H1" "1"

# 8. Tool page returns 200 (if slug provided)
if [ "$TOOL_SLUG" != "markup-calculator" ] || curl -s -o /dev/null -w "%{http_code}" "$DOMAIN/$TOOL_SLUG/" | grep -q "200"; then
  TOOL_STATUS=$(curl -s -o /dev/null -w "%{http_code}" "$DOMAIN/$TOOL_SLUG/")
  check "Tool page HTTP status" "$TOOL_STATUS" "200"

  # 9. Tool page has H1
  TOOL_H1=$(curl -s "$DOMAIN/$TOOL_SLUG/" | grep -c '<h1')
  check "Tool page has H1" "$TOOL_H1" "1"

  # 10. Tool page has FAQPage schema
  TOOL_SCHEMA=$(curl -s "$DOMAIN/$TOOL_SLUG/" | grep -c '"FAQPage"')
  check "Tool page has FAQPage schema" "$TOOL_SCHEMA" "1"

  # 11. Tool page has SoftwareApplication schema
  TOOL_APP_SCHEMA=$(curl -s "$DOMAIN/$TOOL_SLUG/" | grep -c '"SoftwareApplication"')
  check "Tool page has SoftwareApplication schema" "$TOOL_APP_SCHEMA" "1"

  # 12. Tool page has canonical tag
  TOOL_CANONICAL=$(curl -s "$DOMAIN/$TOOL_SLUG/" | grep -c 'rel="canonical"')
  check "Tool page has canonical tag" "$TOOL_CANONICAL" "1"

  # 13. OG image accessible
  OG_IMAGE=$(curl -s -o /dev/null -w "%{http_code}" "$DOMAIN/$TOOL_SLUG/opengraph-image")
  check "OG image accessible" "$OG_IMAGE" "200"

  # 14. Tool page links back to homepage
  TOOL_LINKS_HOME=$(curl -s "$DOMAIN/$TOOL_SLUG/" | grep -c 'href="/"')
  check "Tool page links to homepage" "$TOOL_LINKS_HOME" "1"
fi

# 15. No noindex on homepage
NOINDEX=$(curl -s "$DOMAIN/" | grep -c 'noindex')
if [ "$NOINDEX" -eq "0" ]; then
  echo "  ✓ PASS — Homepage not noindexed"
  PASS=$((PASS+1))
else
  echo "  ✗ FAIL — Homepage has noindex tag (CRITICAL)"
  FAIL=$((FAIL+1))
fi

echo ""
echo "=== RESULTS: $PASS passed, $FAIL failed ==="
echo ""

if [ "$FAIL" -gt "0" ]; then
  echo "  ACTION REQUIRED: Fix all failures before requesting GSC indexing."
  echo ""
  exit 1
else
  echo "  All checks passed. Safe to request indexing in GSC."
  echo ""
  exit 0
fi
```

---

## How to Install the Script

In every project repo:

```bash
mkdir -p scripts
# Create the file (paste the script above)
chmod +x scripts/verify-seo.sh
```

Run it:
```bash
# Basic check (homepage only)
bash scripts/verify-seo.sh https://ecomstudio.ai

# Full check including a specific tool page
bash scripts/verify-seo.sh https://ecomstudio.ai markup-calculator
```

---

## Make It Automatic With a Git Hook

Create `.git/hooks/pre-push` in each repo:

```bash
#!/bin/bash
echo "Running SEO verification before push..."
# Only run on pushes to main branch
if git rev-parse --abbrev-ref HEAD | grep -q "main"; then
  if [ -f "scripts/verify-seo.sh" ]; then
    # Can't check live domain pre-push, so check local dev server if running
    echo "Remember to run: bash scripts/verify-seo.sh https://yourdomain.com"
  fi
fi
exit 0
```

```bash
chmod +x .git/hooks/pre-push
```

---

## The Weekly Health Check Script

Run every Monday. Add to each project as `scripts/weekly-check.sh`:

```bash
#!/bin/bash
# Weekly SEO Health Check
# Run: bash scripts/weekly-check.sh https://yourdomain.com

DOMAIN="${1:-https://yourdomain.com}"
echo ""
echo "=== Weekly Health Check: $DOMAIN ==="
echo "Run date: $(date)"
echo ""

# Check all pages in sitemap return 200
echo "Checking sitemap pages..."
URLS=$(curl -s "$DOMAIN/sitemap.xml" | grep -oP '(?<=<loc>)[^<]+')
FAIL_COUNT=0

while IFS= read -r url; do
  STATUS=$(curl -s -o /dev/null -w "%{http_code}" "$url")
  if [ "$STATUS" != "200" ]; then
    echo "  ✗ $STATUS — $url"
    FAIL_COUNT=$((FAIL_COUNT+1))
  fi
done <<< "$URLS"

if [ "$FAIL_COUNT" -eq "0" ]; then
  echo "  ✓ All sitemap pages return 200"
else
  echo "  $FAIL_COUNT pages have errors — fix before adding new content"
fi

echo ""
echo "=== Manual checks to do in GSC ==="
echo "  1. Coverage > Indexed count (should be growing)"
echo "  2. Coverage > Crawled not indexed (should not be growing)"
echo "  3. Core Web Vitals > any new issues?"
echo "  4. Manual Actions > any penalties? (should be zero)"
echo ""
echo "Log these numbers in your tracking spreadsheet."
echo ""
```

---

## The 5-Minute GSC Verification Protocol

After every new page deployment, within 48 hours:

1. Open GSC → URL Inspection
2. Enter the new page URL
3. Click "Request Indexing"
4. Note the crawl status — save screenshot to tracking sheet
5. Check back in 7 days — if still not indexed, run `verify-seo.sh` again

**Do not deploy more pages until this 5-step protocol is done for each page.**

---

## Kimi API Output Verification

When Kimi generates tool widget code, run these checks before Claude Code
integrates it:

```bash
# Test Kimi widget for common errors
# 1. Check for API calls (should be zero for math calculators)
grep -n "fetch\|axios\|XMLHttpRequest\|api\." kimi-output.js
# If any results: the widget makes network calls — this will hurt INP and may fail offline

# 2. Check for console.log statements (should be removed before production)
grep -n "console.log" kimi-output.js

# 3. Check for hardcoded values that should be dynamic
grep -n "hardcoded\|TODO\|FIXME\|placeholder" kimi-output.js
```

If the Kimi widget makes API calls for a calculator that should be pure math:
reject it and ask Kimi to rewrite with pure JavaScript calculation.

Test with edge cases manually:
- Input: 0 (zero cost price)
- Input: negative number
- Input: very large number (1,000,000)
- Input: decimal (0.99)
- Input: no input (empty field)

All five cases must produce reasonable output without errors or NaN.
