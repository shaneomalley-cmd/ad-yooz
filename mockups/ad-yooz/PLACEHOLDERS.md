# Placeholders — `/ad-yooz` (Archetype 01, Brand)

Every `{{TOKEN}}` used in `index.html`. No statistic, customer name, logo,
award, analyst position, rating, price or capability is invented — per
Foundation §2, everything not already verified is a token here.

| Token | What it needs | Owner |
|---|---|---|
| `{{AD_HEADLINE_1..3}}` | Live RSA headline text from Campaign 01 BRAND (ad groups Yooz core / Yooz evaluation / Yooz vs competitor), pasted into the ad-to-page continuity comment at the top of `index.html` so hero copy can be checked against it. | Paid media / copy |
| `{{AD_DESCRIPTION_1..2}}` | Live RSA description text, same purpose as above. | Paid media / copy |
| `{{CUSTOMER_LOGO_1..6}}` | Named customer logos for the proof strip. Brand guidelines don't name specific customers — needs real, reference-approved logos. | Customer marketing / legal |
| `{{G2_RATING}}` | Current G2 star rating. Do not reuse a screenshot-derived number — pull live from G2 or the G2 badge widget. | Marketing / G2 account owner |
| `{{G2_REVIEW_COUNT}}` | Current G2 review count, same sourcing constraint as above. | Marketing / G2 account owner |
| `{{IMPLEMENTATION_TIMELINE_BENCHMARK}}` | A real, substantiable implementation-time claim for the FAQ answer. Nothing in the brand doc gives this a number — needs a source (e.g. customer success benchmark) or the FAQ answer should stay qualitative. | Customer success / product marketing |
| `{{SOC2_CERTIFICATION_STATUS}}` | Current SOC 2 certification status/wording for the security FAQ answer. Per the prior template build in this repo (`CHECKLIST.md`), no SOC 2 badge/asset was found anywhere in the live site source — confirm current status before publishing this answer at all. | Security / compliance |
| `{{GDPR_COMPLIANCE_STATEMENT}}` | Current GDPR compliance wording, same FAQ answer as above. | Security / compliance / legal |
| `{{COMPANY_ADDRESS}}` | Physical business address for the footer (required for Quality Score's transparency/navigability check). Also present in `/mockups/_system/components.html`'s footer specimen — same value, one source of truth. | Legal / ops |

## Verified facts used directly (not tokens)

Per Foundation §2, these two are brand-doc-verified and used as plain text,
not placeholders:
- "more than 250 financial systems" (hero subhead, FAQ)
- multi-channel capture list — email, drag & drop, mobile, scan, sFTP,
  e-invoicing, fetcher, API (FAQ)
