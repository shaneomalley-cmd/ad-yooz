# Placeholders — /ad-sap

| Token | What's needed | Owner |
|---|---|---|
| `{{AD_HEADLINE_SAP_1..3}}` | Live RSA headline text for the SAP ad group, Campaign 07 FIT – ERP | Paid search / copy |
| `{{AD_DESCRIPTION_SAP_1}}` | Live RSA description line for the same ad group | Paid search / copy |
| `{{SCREENSHOT_INSIDE_SAP}}` (×2) | Real screenshots inside a live SAP environment — posted FI document and MM three-way match. Must show SAP GUI/Fiori chrome, not a generic UI. | Product marketing / design |
| `{{SYNC_FIELDS_SAP — frequency}}` (×5 rows) | Actual sync cadence per field from engineering/product | Product / Engineering |
| `{{CUSTOMER_LOGO_SAP}}` | Logo of a named customer running SAP, cleared for marketing use | Customer marketing |
| `{{CUSTOMER_QUOTE_SAP}}` | Real quote, ideally addressing the "will it break on our next SAP upgrade" fear | Customer marketing |
| `{{CUSTOMER_NAME_SAP}}` / `{{CUSTOMER_TITLE_SAP}}` | Name and title of the quoted customer, with permission on file | Customer marketing |
| `{{INTEGRATION_ONE_PAGER_URL}}` | Link to (or to-be-produced) SAP-specific integration one-pager | Content / demand gen |
| `{{BUSINESS_ADDRESS}}` | Footer legal address (shared across all pages) | Legal / brand |

## Verified facts used directly (not tokens)
- "Exports to 250+ financial systems" — brand guidelines.
- Purchase → Capture → Review → Approve → Pay → Export — brand-approved process vocabulary.
- "SAP-certified integration" trust-row claim and "Certified for SAP FI and MM" module card — **flag for legal/product review before ship**: confirm Yooz holds an actual SAP certification (e.g. SAP-certified integration with SAP S/4HANA or similar) before this exact wording goes live. If no formal certification exists, replace with a claim the connector team can substantiate (e.g. "built on SAP's standard FI/MM interfaces," which is stated separately and is safer).

## Open risk
If SAP has no reference customer, replace the customer block with `{{MISSING — no reference customer on this ERP}}` rather than reusing another ERP's quote.
