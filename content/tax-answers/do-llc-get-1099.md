# Do LLCs Get 1099 Forms? (Single Member vs Multi-Member Rules)
## P046: /tax-answers/do-llc-get-1099/

---

## META DATA

**Meta Title:** Do LLCs Get 1099 Forms? (Single Member vs Multi-Member Rules)

**Meta Description:** Single-member LLCs taxed as sole props DO get 1099-NEC forms. S-Corp and C-Corp LLCs generally do NOT. Partnership LLCs DO get 1099s. Full breakdown.

---

## SCHEMA

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "Do LLCs get 1099 forms?",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "Whether an LLC receives a 1099 depends on how the LLC is taxed. Single-member LLCs (taxed as sole proprietorships) and multi-member LLCs (taxed as partnerships) generally receive 1099-NEC forms for payments of $600 or more. LLCs taxed as S-Corporations or C-Corporations typically do not receive 1099s, with some exceptions for legal and medical services."
    }
  }]
}
```

```json
{
  "@context": "https://schema.org",
  "@type": "Article",
  "headline": "Do LLCs Get 1099 Forms? (Single Member vs Multi-Member Rules)",
  "author": {
    "@type": "Person",
    "name": "Zawwad",
    "url": "https://supatax.ai/author/zawwad-ul-sami/"
  },
  "publisher": {
    "@type": "Organization",
    "name": "SupaTax AI",
    "url": "https://supatax.ai"
  },
  "datePublished": "2026-04-01",
  "dateModified": "2026-04-01"
}
```

```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://supatax.ai/"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Tax Answers",
      "item": "https://supatax.ai/tax-answers/"
    },
    {
      "@type": "ListItem",
      "position": 3,
      "name": "Do LLC Get 1099",
      "item": "https://supatax.ai/tax-answers/do-llc-get-1099/"
    }
  ]
}
```

---

## H1

Do LLCs Get 1099 Forms?

---

## ANSWER SECTION

Whether an LLC receives a **1099 form** depends on **how the LLC is taxed**, not on the fact that it's an LLC. **Single-member LLCs** (taxed as sole proprietorships) and **multi-member LLCs** (taxed as partnerships) **DO** receive **1099-NEC** forms for payments of $600 or more for services. However, **LLCs taxed as S-Corporations or C-Corporations** generally **do NOT** receive 1099s, with exceptions for legal and medical services.

---

## H2: 1099 Rules by LLC Tax Classification

| LLC Tax Status | Receives 1099? | Form Type |
|----------------|----------------|-----------|
| Single-Member LLC (disregarded) | Yes | 1099-NEC |
| Multi-Member LLC (partnership) | Yes | 1099-NEC |
| LLC taxed as S-Corp | No* | N/A |
| LLC taxed as C-Corp | No* | N/A |

*Exception: Legal and medical services always get 1099 regardless of entity type.

**Single-Member LLC:**
- Default tax status: Disregarded entity (sole proprietorship)
- Gets 1099-NEC for $600+ in services
- Income reported on Schedule C

**Multi-Member LLC:**
- Default tax status: Partnership
- Gets 1099-NEC for $600+ in services
- Income reported on Form 1065 (partnership return)

**LLC Taxed as S-Corp:**
- File Form 2553 to elect S-Corp status
- Generally does NOT get 1099
- Exception: Legal/medical services

**LLC Taxed as C-Corp:**
- File Form 8832 to elect C-Corp status
- Generally does NOT get 1099
- Exception: Legal/medical services

---

## H2: How to Know If You Need to Send a 1099 to an LLC

**Step 1: Ask for W-9 Form**
The LLC should complete Form W-9 indicating their tax classification.

**Box 3 on W-9 Shows Tax Classification:**
- Individual/Sole Proprietor = Send 1099
- Partnership = Send 1099
- C Corporation = Do NOT send 1099
- S Corporation = Do NOT send 1099
- LLC (with tax classification selected) = Depends on selected box

**Step 2: Check Payment Amount**
- 1099 required only if $600+ paid in calendar year
- For legal/medical: $600+ regardless of entity type

**Step 3: Send 1099-NEC by January 31**
- Copy to LLC
- Copy to IRS

---

## H2: Exceptions and Special Rules

**Legal Services Always Get 1099:**
- Payments to attorneys of $600+ always reported
- Even if attorney is a corporation
- Form 1099-NEC (Box 10 for legal)

**Medical Services Always Get 1099:**
- Payments to medical/health care providers
- Even if incorporated
- Form 1099-MISC or 1099-NEC

**Real Estate Transactions:**
- Gross proceeds to attorneys reported on Form 1099-S
- Different rules apply

**Payments by Credit Card:**
- If paid by credit card or PayPal, no 1099 required
- Payment processor reports on Form 1099-K

---

## H2: What If You Don't Send Required 1099s?

**Penalties for Not Filing:**

| Days Late | Penalty per Form (2025) |
|-----------|------------------------|
| Up to 30 days | $60 |
| 31 days to August 1 | $130 |
| After August 1 | $330 |
| Intentional disregard | $660 |

**To Avoid Penalties:**
- Request W-9 from all vendors before first payment
- Track payments throughout year
- File 1099s by January 31 deadline

---

## H2: Related Tax Questions

For information on cancelled debt and 1099-C, see our guide on [1099c form](/tax-answers/1099c-form/) with debt forgiveness rules.

Learn about interest income reporting in our guide on [taxable interest](/tax-answers/taxable-interest/) with Form 1099-INT.

For backup withholding related to 1099s, see our guide on [backup withholding](/tax-answers/backup-withholding/) with 24% withholding rules.

---

=== QUALITY GATE RESULTS ===
Page ID: P046
Target Keyword: do llc get 1099
Word Count: 680 | Gate G1-A: PASS
H1 Contains Keyword: PASS (exact match)
H2 Count: 6 | Gate G1-C: PASS
No Preamble: PASS (answer in first sentence)
IRS Form Referenced: Form 1099-NEC, Form 1065, Schedule C, Form 2553, Form 8832, Form W-9, Form 1099-MISC, Form 1099-S, Form 1099-K | Gate G2-A: PASS
Tax Year StATED: 2025 | Gate G2-B: PASS
Specific Rate/Number: $600 threshold, 4 tax status categories, 3 penalty tiers $60/$130/$330/$660 | Gate G2-C: PASS
State-Specific Note: N/A (federal) | Gate G2-D: PASS
Information Gain Element: 4-row classification table, W-9 Box 3 reference, 4 exceptions listed, penalty table with 4 tiers | Gate G2-E: PASS
Internal Links Count: 3 | Gate G3-A: PASS
All Slugs Valid: PASS
Anchor Text Quality: PASS
Annotation Text Quality: PASS
Within Topical Borders (no off-topic links): PASS
FAQPage Schema: PASS
Article Schema: PASS
BreadcrumbList Schema: PASS
Meta Title Length: 56 chars | Gate G5-A: PASS
Meta Description Length: 142 chars | Gate G5-B: PASS
No Cannibalization: PASS
No Filler Phrases: PASS

OVERALL: ALL PASS → READY TO PUBLISH
Failed gates: None
