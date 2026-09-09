# Placeholders — `/ad-ap-automation-construction`

Every `{{TOKEN}}` used in `index.html`, per Foundation §2 claims discipline.

## Ad continuity (top-of-file comment)
- `{{AD_HEADLINE_1..3}}`, `{{AD_DESCRIPTION_1..2}}` — copy team: paste live
  RSA copy for Campaign 08 FIT – Industry, ad group Construction.

## Competitive claim — needs legal/SME substantiation before publish
- `FOUNDATIONSOFT_JONAS_AP_GAP` (four-option comparison, "Your
  construction ERP's AP module" card) — the copy states that lien waiver
  and retainage tracking "typically still run in spreadsheets alongside"
  a construction ERP's native AP module. This is a reasonable inference
  from `09-fit-industry.md`'s own framing (construction's default
  alternative is the ERP's AP module, and only AvidXchange is named as
  holding "a true vertical AP page" — implying the others don't natively
  solve this), but it is a claim about a named competitor's product and
  must be verified against FoundationSoft's and Jonas Construction's
  actual current feature set before this page ships. Do not publish
  without that check — an inaccurate claim about a named competitor is a
  legal liability, not just a copy risk.

## Vertical vocabulary — needs vertical SME sign-off before publish
These four terms are named explicitly in `09-fit-industry.md` (not
invented for this build): "job costs, lien waivers, retainage and
progress billing." Flagged for a construction AP SME to confirm the
copy describes each correctly before publish.
- `DOCTYPE_CONSTRUCTION_1` — "job costs"
- `DOCTYPE_CONSTRUCTION_2` — "lien waivers"
- `DOCTYPE_CONSTRUCTION_3` — "retainage"
- `DOCTYPE_CONSTRUCTION_4` — "progress billing"
- `APPROVAL_CHAIN_CONSTRUCTION` — "project and finance approval chain,
  PM sign-off included." No specific chain structure was given in the
  brief, so this stays generic pending SME input.

## Proof section
- `{{CUSTOMER_QUOTE_CONSTRUCTION}}` — customer quote, needs a real
  customer and real permission to publish.
- `{{CUSTOMER_CONSTRUCTION_1}}`, `{{CUSTOMER_CONSTRUCTION_2}}` — named
  construction customer/peer references.
- `{{CUSTOMER_LOGO_CONSTRUCTION_1}}`, `{{CUSTOMER_LOGO_CONSTRUCTION_2}}`
  — customer logo marks.
- `{{CASE_STUDY_CONSTRUCTION}}` / `{{CASE_STUDY_CONSTRUCTION_URL}}` — the
  secondary-conversion case study asset (title + link), referenced twice
  (workflow section, form section).

## Footer
- `{{COMPANY_ADDRESS}}` — physical business address (QS transparency
  requirement, Foundation §3.4).

## Not tokenized — stated directly per Foundation §2
"Yooz exports to more than 250 financial systems" and the multi-channel
capture list (email, drag & drop, mobile, scan, sFTP, e-invoicing,
fetcher, API) are the two facts Foundation clears for direct use; both
appear in the Product section and the four-option comparison without a
token.
