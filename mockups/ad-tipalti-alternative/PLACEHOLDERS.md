# Placeholders — `/ad-tipalti-alternative`

Every `{{TOKEN}}` used in `index.html`, what it needs, and who should own filling
it in. Per `00-FOUNDATION.md` §2, none of these were guessed — no comparative
claim, statistic, price, customer name, or capability description about either
Tipalti or Yooz ships in this mockup without a substantiated source behind it.

## Ad continuity (top-of-file comment block)

| Token | Needs | Owner |
|---|---|---|
| `{{AD_HEADLINE_1..4}}` | Live RSA headline text from campaign 09, ad group "tipalti alternative[s]" | Paid media / copy team |
| `{{AD_DESCRIPTION_1..2}}` | Live RSA description text, same ad group | Paid media / copy team |

## Header / footer

| Token | Needs | Owner |
|---|---|---|
| `{{PHONE_NUMBER}}` / `{{PHONE_NUMBER_DISPLAY}}` | Sales line to show in header (tel: href + display format) | Demand gen |
| `{{BUSINESS_ADDRESS}}` | Physical business address for footer, required for QS transparency/navigability | Legal / marketing ops |
| `{{CURRENT_YEAR}}` | Build-time year for the copyright line | Dev (mechanical, not a claim — safe to template) |

## Comparison table

Every cell describing a **Tipalti** capability is tokenized — Yooz has no
authoritative, dated source for a competitor's current feature set, and
competitor feature sets change (see NOTES.md legal section). Every cell
describing a **Yooz** capability beyond the two facts Foundation clears for
direct use (250+ ERPs; the 8-channel capture list) is also tokenized, because
it's framed as a *comparative* claim next to Tipalti and inherits the same
substantiation bar.

| Token | Needs | Owner |
|---|---|---|
| `{{COMPETITOR_FEATURE_TIPALTI_CAPTURE_CHANNELS}}` | Tipalti's actual supported capture channels, dated | Competitive intel |
| `{{COMPETITOR_FEATURE_TIPALTI_ERP_COUNT}}` | Tipalti's actual current integration/ERP count, dated | Competitive intel |
| `{{COMPETITOR_FEATURE_TIPALTI_GLOBAL_PAYOUTS}}` | Tipalti's actual global mass-payout capability (currencies/countries), dated | Competitive intel |
| `{{YOOZ_FEATURE_GLOBAL_PAYOUTS_FIT}}` | Honest, one-line statement of Yooz's payment-rail scope vs. Tipalti's — this is the concession row, must not be spun | Product marketing |
| `{{COMPETITOR_WINS_ROW}}` | Anchor/label used in the concede-row note; confirm wording once product marketing signs off on `{{YOOZ_FEATURE_GLOBAL_PAYOUTS_FIT}}` | Product marketing |
| `{{COMPETITOR_FEATURE_TIPALTI_P2P_COVERAGE}}` | Tipalti's actual purchase-to-pay/PO-matching coverage, dated | Competitive intel |
| `{{YOOZ_FEATURE_P2P_COVERAGE}}` | Yooz's P2P coverage claim, phrased comparatively | Product marketing |
| `{{COMPETITOR_TIPALTI_IMPLEMENTATION_WEEKS}}` | Tipalti's typical implementation timeline, dated, sourced | Competitive intel |
| `{{YOOZ_IMPLEMENTATION_WEEKS}}` | Yooz's typical implementation timeline | Customer success |
| `{{COMPETITOR_TIPALTI_PRICING_MODEL}}` | Tipalti's public pricing model description (not exact pricing unless public) | Competitive intel |
| `{{PRICE_PER_INVOICE_BENCHMARK}}` | Yooz's pricing model / per-invoice benchmark | Sales ops / finance |
| `{{COMPETITOR_TIPALTI_APPROVAL_CONFIG}}` | Tipalti's approval workflow configurability, dated | Competitive intel |
| `{{YOOZ_FEATURE_APPROVAL_CONFIG}}` | Yooz's approval workflow configurability | Product marketing |
| `{{YOOZ_MIGRATION_SUPPORT_DETAIL}}` | What migration support Yooz actually commits to for Tipalti switchers (named program, SLA, or generic onboarding — say which) | Customer success |
| `{{DATE}}` | Last-verified date for the whole table — structural element, not decoration | Table owner (below) |
| `{{TABLE_OWNER}}` | Named person/team accountable for keeping this table current | Competitive intel lead |
| `{{TABLE_REVIEW_CADENCE}}` | How often the table gets re-checked (e.g. "quarterly") | Competitive intel lead |
| `{{SOURCE_TIPALTI_CAPTURE_CHANNELS}}` | Footnote [1] source citation | Competitive intel |
| `{{SOURCE_TIPALTI_ERP_COUNT}}` | Footnote [3] source citation | Competitive intel |
| `{{SOURCE_TIPALTI_GLOBAL_PAYOUTS}}` | Footnote [5] source citation | Competitive intel |
| `{{SOURCE_TIPALTI_P2P_COVERAGE}}` | Footnote [7] source citation | Competitive intel |
| `{{SOURCE_TIPALTI_IMPLEMENTATION_WEEKS}}` | Footnote [9] source citation | Competitive intel |
| `{{SOURCE_TIPALTI_PRICING_MODEL}}` | Footnote [11] source citation | Competitive intel |
| `{{SOURCE_TIPALTI_APPROVAL_CONFIG}}` | Footnote [13] source citation | Competitive intel |

Yooz-column footnotes [2], [4], [6], [8], [10], [12], [14], [15] cite internal
product/legal sources rather than external ones; list them alongside the
Tipalti sources once assigned so every cell in the table — not just the
competitor's — carries a traceable citation.

## Migration timeline

| Token | Needs | Owner |
|---|---|---|
| `{{MIGRATION_PHASE_1..4}}` | Real phase names (e.g. discovery, parallel run, cutover, post-migration support) — do not invent generic names without CS sign-off | Customer success / implementation |
| `{{MIGRATION_PHASE_1..4}}_DESCRIPTION` | One or two sentences of what happens in that phase | Customer success / implementation |
| `{{MIGRATION_PHASE_1..4}}_WEEKS` | Real duration per phase | Customer success / implementation |
| `{{MIGRATION_DURATION_WEEKS}}` | Real end-to-end typical duration (appears in hero stat card and total-duration banner — must match the sum of the four phases) | Customer success / implementation |

## Customer proof

| Token | Needs | Owner |
|---|---|---|
| `{{CUSTOMER_SWITCHED_FROM_TIPALTI}}` | A named customer who switched from Tipalti specifically, with their permission to be named. **If none exists, this section ships as the honest "not yet available" state already built — do not fill with a generic Yooz customer.** | Customer marketing |

## Legal / trust

The comparison table's underlying claims policy is documented in `NOTES.md`
under "Legal and policy gate" — this file only tracks the tokens themselves.
