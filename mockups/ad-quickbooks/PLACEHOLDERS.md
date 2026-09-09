# Placeholders — /ad-quickbooks

| Token | What's needed | Owner |
|---|---|---|
| `{{AD_HEADLINE_QUICKBOOKS_1..3}}` | Live RSA headline text for the QuickBooks ad group, Campaign 07 FIT – ERP | Paid search / copy |
| `{{AD_DESCRIPTION_QUICKBOOKS_1}}` | Live RSA description line for the same ad group | Paid search / copy |
| `{{SCREENSHOT_INSIDE_QUICKBOOKS}}` (×2) | Real screenshots inside a live QuickBooks Online (or Desktop) company file — posted bill and approval queue. | Product marketing / design |
| `{{SYNC_FIELDS_QUICKBOOKS — frequency}}` (×5 rows) | Actual sync cadence per field from engineering/product | Product / Engineering |
| `{{CUSTOMER_LOGO_QUICKBOOKS}}` | Logo of a named customer running QuickBooks, cleared for marketing use | Customer marketing |
| `{{CUSTOMER_QUOTE_QUICKBOOKS}}` | Real quote, ideally from a team that outgrew manual bill entry — reinforces the volume qualifier rather than undercutting it | Customer marketing |
| `{{CUSTOMER_NAME_QUICKBOOKS}}` / `{{CUSTOMER_TITLE_QUICKBOOKS}}` | Name and title of the quoted customer, with permission on file | Customer marketing |
| `{{INTEGRATION_ONE_PAGER_URL}}` | Link to (or to-be-produced) QuickBooks-specific integration one-pager | Content / demand gen |
| `{{BUSINESS_ADDRESS}}` | Footer legal address (shared across all pages) | Legal / brand |

## Verified facts used directly (not tokens)
- "Exports to 250+ financial systems" — brand guidelines.
- Purchase → Capture → Review → Approve → Pay → Export — brand-approved process vocabulary.

## Open risk
If QuickBooks has no reference customer, replace the customer block with
`{{MISSING — no reference customer on this ERP}}` rather than reusing
another ERP's quote. A QuickBooks reference is also the one most useful for
the volume-qualifier message — ideally a customer whose invoice volume
outgrew a smaller tool, not just any QuickBooks user.
