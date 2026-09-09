# Placeholders — `/ad-ap-comparison`

Every `{{TOKEN}}` used in `index.html`, what it needs, and who should own filling it in.

## Yooz's own metrics

| Token | Needed | Owner |
|---|---|---|
| `{{G2_RATING}}` | Current Yooz G2 star rating | Marketing / review-platform admin |
| `{{G2_REVIEW_COUNT}}` | Current Yooz G2 review count | Marketing / review-platform admin |
| `{{CAPTERRA_RATING}}` | Current Yooz Capterra star rating | Marketing / review-platform admin |
| `{{CAPTERRA_REVIEW_COUNT}}` | Current Yooz Capterra review count | Marketing / review-platform admin |
| `{{YOOZ_STARTING_PRICE_MODEL}}` | Real starting price or pricing model description (e.g. "per-invoice, custom quote") — never a specific number unless Sales confirms it's publishable | Sales / Pricing |
| `{{TABLE_LAST_UPDATED_DATE}}` | The actual date the table's data was last verified — must be kept current or the table becomes a liability | Content owner of this page |

## Competitor data (Airbase, Bill.com, Ramp, Stampli, Tipalti)

Every cell in the comparison table for these five vendors is tokenised —
none of these numbers may be estimated or carried over from memory
training data, since they are exactly the kind of comparative claim
Section 2 of `00-FOUNDATION.md` calls a legal liability if wrong.

| Token pattern | Needed | Owner |
|---|---|---|
| `{{VENDOR_<NAME>_G2_RATING}}` | Current G2 star rating, pulled the same week as Yooz's own | Competitive intelligence / product marketing |
| `{{VENDOR_<NAME>_CAPTERRA_RATING}}` | Current Capterra star rating | Competitive intelligence / product marketing |
| `{{VENDOR_<NAME>_ERP_INTEGRATIONS}}` | Verified integration count or list, sourced from the vendor's own site (not a guess) | Competitive intelligence |
| `{{VENDOR_<NAME>_CAPTURE_CHANNELS}}` | Verified list of invoice intake channels the vendor actually supports | Competitive intelligence |
| `{{VENDOR_<NAME>_DEDICATED_AP_FOCUS}}` | Short phrase: is AP the vendor's core product or one module of a broader suite? | Competitive intelligence |
| `{{VENDOR_<NAME>_BEST_FOR}}` | One neutral sentence — written so a competitor could read it and not call it a strawman | Product marketing, reviewed by legal/claims process |
| `{{VENDOR_<NAME>_STARTING_PRICE}}` | Vendor's own published pricing model language, not a converted or estimated number | Competitive intelligence |

`<NAME>` = `AIRBASE`, `BILLCOM`, `RAMP`, `STAMPLI`, `TIPALTI`.

**Note on the check-mark cells (`check-yes` / `check-partial`):** the
mockup's placement of "dedicated AP focus" checks vs. partial-marks for
Airbase, Bill.com and Ramp reflects public positioning (spend-management
suites vs. AP-first tools) at time of writing, not a sourced claim — treat
these as drafts to confirm, not settled facts, before publish.

## Analyst / positioning

| Token | Needed | Owner |
|---|---|---|
| `{{GARTNER_MQ_CATEGORY_NAME}}` | The exact, correctly-named Gartner MQ category Yooz is being compared against (do not invent a category name) | Product marketing / analyst relations |
| `{{GARTNER_POSITION_STATEMENT}}` | A real, honest sentence from the team on why Yooz doesn't hold an MQ placement and what it holds instead — this is the single most sensitive line on the page and needs sign-off, not a copywriter's guess | Leadership / analyst relations |

## Fit criteria

| Token | Needed | Owner |
|---|---|---|
| `{{MIN_INVOICE_VOLUME_THRESHOLD}}` | The actual invoice-volume floor below which Yooz isn't the most cost-effective fit — needs a real number from Sales/Product, not a round guess | Sales / Product |

## Footer / compliance

| Token | Needed | Owner |
|---|---|---|
| `{{BUSINESS_ADDRESS}}` | Real physical business address for the footer (Google penalizes orphaned-funnel pages that omit this) | Legal / Marketing Ops |
