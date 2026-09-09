# Placeholders — `/ad-ap-automation-healthcare`

Every `{{TOKEN}}` used in `index.html`, per Foundation §2 claims discipline.

## Ad continuity (top-of-file comment)
- `{{AD_HEADLINE_1..3}}`, `{{AD_DESCRIPTION_1..2}}` — copy team: paste live
  RSA copy for Campaign 08 FIT – Industry, ad group Healthcare.

## Vertical vocabulary — needs vertical SME sign-off before publish
These terms come from `09-fit-industry.md` itself (not invented for this
build), but the brief is explicit that "vertical vocabulary used slightly
wrong is worse than generic copy" — so each is flagged for a healthcare
AP SME to confirm before this ships, even though the copy renders the
term directly rather than a blank token.
- `DOCTYPE_HEALTHCARE_1` — "GPO invoices" (workflow section, list item 1)
- `DOCTYPE_HEALTHCARE_2` — "contract pricing" (workflow section, list item 2)
- `APPROVAL_CHAIN_HEALTHCARE` — "multi-department approval chain" (hero
  subhead + workflow section). The brief asks to name the approval chain;
  no specific chain structure (e.g. which departments, in what order) was
  given, so this stays intentionally generic pending SME input rather than
  inventing a specific sign-off path.

## Proof section
- `{{CUSTOMER_QUOTE_HEALTHCARE}}` — customer quote, needs a real customer
  and real permission to publish.
- `{{CUSTOMER_HEALTHCARE_1}}`, `{{CUSTOMER_HEALTHCARE_2}}` — named
  healthcare customer/peer references.
- `{{CUSTOMER_LOGO_HEALTHCARE_1}}`, `{{CUSTOMER_LOGO_HEALTHCARE_2}}` —
  customer logo marks.
- `{{CASE_STUDY_HEALTHCARE}}` / `{{CASE_STUDY_HEALTHCARE_URL}}` — the
  secondary-conversion case study asset (title + link), referenced twice
  (proof section, form section).

## Footer
- `{{COMPANY_ADDRESS}}` — physical business address (QS transparency
  requirement, Foundation §3.4).

## Not tokenized — stated directly per Foundation §2
"Yooz exports to more than 250 financial systems" and the multi-channel
capture list (email, drag & drop, mobile, scan, sFTP, e-invoicing,
fetcher, API) are the two facts Foundation clears for direct use; both
appear in the Product section without a token.
