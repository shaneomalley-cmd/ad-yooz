# Placeholders — /ad-netsuite

Every `{{TOKEN}}` used in `index.html`, what it needs, and who owns filling it.

| Token | What's needed | Owner |
|---|---|---|
| `{{AD_HEADLINE_NETSUITE_1..3}}` | Live RSA headline text for the NetSuite ad group, Campaign 07 FIT – ERP, pasted in for continuity check | Paid search / copy |
| `{{AD_DESCRIPTION_NETSUITE_1}}` | Live RSA description line for the same ad group | Paid search / copy |
| `{{SCREENSHOT_INSIDE_NETSUITE}}` (×2) | Real product screenshots captured inside a live NetSuite instance — dashboard panel and approval queue with NetSuite fields visible. Must be NetSuite-specific, not a generic Yooz UI shot. | Product marketing / design |
| `{{MARKETPLACE_LISTING_URL}}` | URL of the Yooz listing on the NetSuite SuiteApp Marketplace. Per 08-fit-erp.md build note: Medius currently ranks #5 on the head term — confirm Yooz has a live listing before this page ships, or this section has nothing to link to. | Partnerships / paid search |
| `{{NETSUITE_MARKETPLACE_CLAIM}}` | Hero trust-row line asserting a marketplace presence — do not ship as "Listed on the NetSuite SuiteApp Marketplace" unless the listing is confirmed live; this is the same open item as the row above | Partnerships / paid search |
| `{{SYNC_FIELDS_NETSUITE — frequency}}` (×5 rows) | Actual sync cadence per field (real-time, hourly, nightly batch, etc.) from engineering/product, not estimated | Product / Engineering |
| `{{CUSTOMER_LOGO_NETSUITE}}` | Logo of a named customer running NetSuite, cleared for marketing use | Customer marketing |
| `{{CUSTOMER_QUOTE_NETSUITE}}` | Real quote, ideally addressing the integration-risk objection directly (this is what closes the "will it break" fear) | Customer marketing |
| `{{CUSTOMER_NAME_NETSUITE}}` / `{{CUSTOMER_TITLE_NETSUITE}}` | Name and title of the quoted customer, with permission on file | Customer marketing |
| `{{INTEGRATION_ONE_PAGER_URL}}` | Link to (or to-be-produced) NetSuite-specific integration one-pager, the secondary conversion asset | Content / demand gen |
| `{{BUSINESS_ADDRESS}}` | Footer legal address (shared across all pages, sourced once) | Legal / brand |

## Verified facts already used directly (not tokens)
- "Exports to 250+ financial systems" — from brand guidelines.
- Purchase → Capture → Review → Approve → Pay → Export stage names — brand-approved process vocabulary.

## Open risk
If NetSuite has no reference customer, `{{CUSTOMER_...}}` block should be replaced with `{{MISSING — no reference customer on this ERP}}` per 08-fit-erp.md rather than reusing a customer from another ERP page.
