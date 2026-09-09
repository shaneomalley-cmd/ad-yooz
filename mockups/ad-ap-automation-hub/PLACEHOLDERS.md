# Placeholders — `/ad-ap-automation-hub` (Archetype 04, Forking hub)

Every `{{TOKEN}}` used in `index.html`. No statistic, customer name, logo,
award, analyst position, rating, price or capability is invented — per
Foundation §2, everything not already verified is a token here.

| Token | What it needs | Owner |
|---|---|---|
| `{{AD_HEADLINE_1..3}}` | Live RSA headline text from Campaign 02b CATEGORY HEAD (both ad groups), pasted into the ad-to-page continuity comment at the top of `index.html`. | Paid media / copy |
| `{{AD_DESCRIPTION_1..2}}` | Live RSA description text, same purpose as above. | Paid media / copy |
| `{{EXPLAINER_VIDEO}}` | The real 90-second explainer video/asset for Path A. No script or storyboard exists yet in this repo. | Video / product marketing |
| `{{BENCHMARK_COST_PER_INVOICE_MANUAL}}` | Published manual cost-per-invoice figure, used both as the "I don't know" substitute value and as the calculator's baseline assumption. Currently a placeholder `15.00` in the page's own script, matching `/ad-ap-roi`'s CONFIG value so the two pages don't quietly disagree once a real figure lands — **must be replaced in both files together**. | Product marketing / benchmarking research |
| `{{ASSUMED_TIME_SAVING_PCT}}` | The modelled automation time/cost saving percentage. Currently a placeholder `60%`, matching `/ad-ap-roi`'s CONFIG value — same replace-in-both-files note as above. | Product marketing, needs sign-off against real customer outcomes |
| `{{BEGINNER_GUIDE_URL}}` | Destination for Path A's secondary "download the beginner's guide" link. The guide itself may not exist yet — confirm before linking. | Content / demand gen |
| `{{COMPARISON_GUIDE_URL}}` | Destination for Path B's secondary "download the comparison guide" link. Likely the same asset `/ad-ap-comparison` gates behind its own email form — confirm whether this should point to that same downloadable PDF or a dedicated landing step. | Content / demand gen |
| `{{G2_RATING}}` | Current Yooz G2 star rating, for the comparison table. | Marketing / G2 account owner |
| `{{G2_REVIEW_COUNT}}` | Current Yooz G2 review count, same table cell. | Marketing / G2 account owner |
| `{{PRICE_PER_INVOICE_BENCHMARK}}` | Yooz's own starting-price figure for the comparison table's price row. | Pricing / product marketing |
| `{{BILLCOM_G2_RATING}}`, `{{RAMP_G2_RATING}}`, `{{TIPALTI_G2_RATING}}` | Competitor G2 ratings. Not sourced in this repo — see Foundation §2's claims-discipline rule on named competitors. | Competitive intelligence |
| `{{BILLCOM_ERP_INTEGRATION_COUNT}}`, `{{RAMP_ERP_INTEGRATION_COUNT}}`, `{{TIPALTI_ERP_INTEGRATION_COUNT}}` | Competitor integration counts. | Competitive intelligence |
| `{{BILLCOM_CAPTURE_CHANNELS}}`, `{{RAMP_CAPTURE_CHANNELS}}`, `{{TIPALTI_CAPTURE_CHANNELS}}` | Competitor invoice-capture channel lists. | Competitive intelligence |
| `{{BILLCOM_CATEGORY_FOCUS}}`, `{{RAMP_CATEGORY_FOCUS}}`, `{{TIPALTI_CATEGORY_FOCUS}}` | Competitor primary-category descriptions. | Competitive intelligence |
| `{{BILLCOM_STARTING_PRICE}}`, `{{RAMP_STARTING_PRICE}}`, `{{TIPALTI_STARTING_PRICE}}` | Competitor starting prices. | Competitive intelligence / pricing |
| `{{COMPANY_ADDRESS}}` | Physical business address for the footer (required for Quality Score's transparency/navigability check). Same value as every other archetype's footer — one source of truth. | Legal / ops |

## Verified facts used directly (not tokens)

Per Foundation §2, these are brand-doc-verified and used as plain text, not
placeholders:
- "more than 250 financial systems" (explainer copy, comparison table)
- multi-channel capture list — email, drag & drop, mobile, scan, sFTP,
  e-invoicing, fetcher, API (explainer copy, comparison table)
- Purchase → Capture → Review → Approve → Pay → Export (the six-stage
  process vocabulary, explainer process strip)

## Shared-value note

`{{BENCHMARK_COST_PER_INVOICE_MANUAL}}` and `{{ASSUMED_TIME_SAVING_PCT}}`
are the two coefficients this page's own calculator script uses. They are
deliberately set to the same illustrative values as `/ad-ap-roi`'s CONFIG
object (`15.00`, `60%`) so a visitor who runs both calculators with the
same inputs doesn't see two different "modelled" numbers. If/when real
figures land, update both files in the same change.
