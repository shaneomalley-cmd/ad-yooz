# Placeholders — /ad-acumatica

**This page is gated pending a price-list decision — see NOTES.md before
treating any of the below as a pre-launch checklist. Nothing here should
be filled in until the gate is lifted.**

| Token | What's needed | Owner |
|---|---|---|
| `{{AD_HEADLINE_ACUMATICA_1..3}}` | Live RSA headline text for the Acumatica ad group, once it exists — the ad group itself is gated | Paid search / copy |
| `{{AD_DESCRIPTION_ACUMATICA_1}}` | Live RSA description line for the same ad group | Paid search / copy |
| `{{SCREENSHOT_INSIDE_ACUMATICA}}` (×2) | Real screenshots inside a live Acumatica instance — posted bill and approval queue. | Product marketing / design |
| `{{SYNC_FIELDS_ACUMATICA — frequency}}` (×5 rows) | Actual sync cadence per field from engineering/product | Product / Engineering |
| `{{CUSTOMER_LOGO_ACUMATICA}}` / customer quote block | No Acumatica reference customer exists yet. Per 08-fit-erp.md, this slot is marked `{{MISSING — no reference customer on this ERP}}` rather than borrowed from another ERP page — do not fill with a non-Acumatica quote. | Customer marketing |
| `{{INTEGRATION_ONE_PAGER_URL}}` | Link to (or to-be-produced) Acumatica-specific integration one-pager | Content / demand gen |
| `{{BUSINESS_ADDRESS}}` | Footer legal address (shared across all pages) | Legal / brand |

## Verified facts used directly (not tokens)
- "Exports to 250+ financial systems" — brand guidelines.
- Purchase → Capture → Review → Approve → Pay → Export — brand-approved process vocabulary.

## Gate
The on-page banner at the top of `index.html` is a build-time reviewer
flag, not shippable copy. It must be removed as part of un-gating this
page, at which point the token checklist above becomes a normal pre-launch
list.
