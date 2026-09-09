# Placeholders — `/ad-ap-comparison` (Archetype 11, Proof / list)

Every `{{TOKEN}}` used in `index.html`. Per Foundation §2, no statistic,
customer name, logo, award, analyst position, rating, price or capability
is invented. This page carries an unusually large token count for one
reason: it's a competitor-naming comparison table, and every claim about
a named competitor is the highest-liability kind of guess this system can
make — so every competitor cell is a token, with nothing approximated.

## Competitor data (comparison table, section 1)

| Token | What it needs | Owner |
|---|---|---|
| `{{BILLCOM_G2_RATING}}` | Bill.com's current G2 star rating, sourced and dated at fill time. | Competitive intelligence |
| `{{RAMP_G2_RATING}}` | Ramp's current G2 star rating. | Competitive intelligence |
| `{{TIPALTI_G2_RATING}}` | Tipalti's current G2 star rating. | Competitive intelligence |
| `{{BILLCOM_CAPTERRA_RATING}}` | Bill.com's current Capterra rating. | Competitive intelligence |
| `{{RAMP_CAPTERRA_RATING}}` | Ramp's current Capterra rating. | Competitive intelligence |
| `{{TIPALTI_CAPTERRA_RATING}}` | Tipalti's current Capterra rating. | Competitive intelligence |
| `{{BILLCOM_ERP_INTEGRATION_COUNT}}` | Bill.com's publicly stated ERP/accounting integration count. | Competitive intelligence |
| `{{RAMP_ERP_INTEGRATION_COUNT}}` | Ramp's publicly stated ERP/accounting integration count. | Competitive intelligence |
| `{{TIPALTI_ERP_INTEGRATION_COUNT}}` | Tipalti's publicly stated ERP/accounting integration count. | Competitive intelligence |
| `{{BILLCOM_CAPTURE_CHANNELS}}` | Bill.com's publicly documented invoice-capture channels. | Competitive intelligence |
| `{{RAMP_CAPTURE_CHANNELS}}` | Ramp's publicly documented invoice-capture channels. | Competitive intelligence |
| `{{TIPALTI_CAPTURE_CHANNELS}}` | Tipalti's publicly documented invoice-capture channels. | Competitive intelligence |
| `{{BILLCOM_CATEGORY_FOCUS}}` | A neutral, defensible one-line category description for Bill.com (e.g. "spend & AP management" vs. Yooz's narrower "AP automation") — needs sign-off, not a guess at positioning. | Competitive intelligence / product marketing |
| `{{RAMP_CATEGORY_FOCUS}}` | Same, for Ramp. | Competitive intelligence / product marketing |
| `{{TIPALTI_CATEGORY_FOCUS}}` | Same, for Tipalti. | Competitive intelligence / product marketing |
| `{{BILLCOM_STARTING_PRICE}}` | Bill.com's current published starting price or pricing model. | Competitive intelligence |
| `{{RAMP_STARTING_PRICE}}` | Ramp's current published starting price or pricing model. | Competitive intelligence |
| `{{TIPALTI_STARTING_PRICE}}` | Tipalti's current published starting price or pricing model. | Competitive intelligence |
| `{{BILLCOM_ANALYST_RECOGNITION}}` | Any real, current, citable analyst or review-site recognition Bill.com holds. | Competitive intelligence |
| `{{RAMP_ANALYST_RECOGNITION}}` | Same, for Ramp. | Competitive intelligence |
| `{{TIPALTI_ANALYST_RECOGNITION}}` | Same, for Tipalti. | Competitive intelligence |

## Yooz data (comparison table + validation section)

| Token | What it needs | Owner |
|---|---|---|
| `{{G2_RATING}}` | Yooz's current G2 star rating. Same token/value as `/ad-yooz`'s proof strip — one source of truth. | Product marketing |
| `{{G2_REVIEW_COUNT}}` | Yooz's current G2 review count. | Product marketing |
| `{{CAPTERRA_RATING}}` | Yooz's current Capterra rating. | Product marketing |
| `{{REVIEW_COUNTS}}` | Yooz's current Capterra review count. | Product marketing |
| `{{PRICE_PER_INVOICE_BENCHMARK}}` | Yooz's starting price or pricing-model description for the "Starting price" row — brand doc doesn't currently publish a number; needs pricing/finance sign-off on what's safe to show a comparison shopper. | Pricing / finance |

## Analyst position (section 4)

| Token | What it needs | Owner |
|---|---|---|
| `{{GARTNER_POSITION_STATEMENT}}` | A real, honest sentence from the team on Yooz's position relative to the Gartner Magic Quadrant for AP automation (e.g. whether Yooz has been evaluated, is tracked in a related Gartner category, or isn't currently part of that research) — needs to come from whoever owns the analyst-relations function, not be inferred. | Analyst relations / product marketing |

## Disqualifiers (section 3, "Choose someone else if…")

| Token | What it needs | Owner |
|---|---|---|
| `{{MIN_INVOICE_VOLUME_THRESHOLD}}` | The actual invoice-volume floor below which Yooz isn't the right fit (the brief's own example: "if you are under N invoices a month"). | Sales / product marketing |
| `{{MIN_INVOICE_VOLUME_RATIONALE}}` | A short, honest reason why (e.g. implementation cost vs. value at that volume) — needs to be a real reason, not a filler sentence. | Sales / product marketing |
| `{{SPECIFIC_CAPABILITY_GAP}}` | A genuinely specific capability Yooz doesn't cover that a real shortlisted competitor does (the brief's own example: "if you need X") — needs a real answer from product, not an invented gap. | Product marketing |

## Shared / structural

| Token | What it needs | Owner |
|---|---|---|
| `{{AD_HEADLINE_1..3}}` | Live RSA headline text from Campaign 09 (Ramp & Bill.com / Competitor research / Head-to-head ad groups) and Campaign 10 (Best-of & Reviews / Conversational evaluation / Comparison & Selection / AP Vendors & Providers / Analyst Validation), pasted into the ad-to-page continuity comment at the top of `index.html`. | Paid media / copy |
| `{{AD_DESCRIPTION_1..2}}` | Live RSA description text, same purpose as above. | Paid media / copy |
| `{{COMPANY_ADDRESS}}` | Physical business address for the footer. Same token/value as `/ad-yooz` and `/ad-ap-roi` — one source of truth. | Legal / ops |

## Verified facts used directly (not tokens)

- **250+ financial systems** and the eight-channel capture list (email,
  drag & drop, mobile, scan, sFTP, e-invoicing, fetcher, API) — both
  cleared for direct use in Foundation §2, used in the "ERP / accounting
  integrations" and "Invoice capture channels" rows for Yooz only.
- **SourceForge Leader (Summer 2024)** and **Capterra Shortlist (2024)** —
  named directly in the "Recent analyst / review recognition" row for
  Yooz, and again with full detail in the validation section — both are
  on Foundation §11's list of awards "real and can be named rather than
  tokenised," with the explicit caveat that every one needs a currency
  check before publishing since several are dated. The validation
  section shows the year on every badge for exactly that reason.
- **CFO Tech Outlook, SpendMatters ("50 to Watch" and SolutionMap
  Validated), SoftwareReviews Gold Medal, G2 "Easiest Admin — Enterprise"
  and G2 Top Performer**, plus the **CIMA/BDO partner marks** and
  **Great Place to Work, 4 years running** — all named directly in the
  validation section on the same basis as above; none of these appear in
  the comparison table itself (kept to the two most recent/relevant there
  — SourceForge and Capterra — to keep that one table cell scannable).
- **Purchase → Capture → Review → Approve → Pay → Export** — the
  brand-approved process vocabulary (Foundation §2), used in the
  "Primary category" row and in section 3's procurement disqualifier.

## Open question affecting this manifest

See NOTES.md "Open questions" — competitor data sourcing is the biggest
gap here specifically because this page names competitors directly (most
other archetypes don't). Whoever fills these tokens should treat rating
figures as needing a re-check close to publish date, not a one-time pull,
since G2/Capterra scores move.
