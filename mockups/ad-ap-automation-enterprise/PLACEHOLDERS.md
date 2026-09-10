# Placeholders — `/ad-ap-automation-enterprise`

Light variant of `/ad-ap-automation` — see that page's `PLACEHOLDERS.md` for
tokens shared between both (differentiator, ad headlines, ERP logos, footer
address). This file lists only the tokens unique to the enterprise proof
section and stat strip.

## Strategy decision (shared with the parent page)

| Token | Needs | Owner |
|---|---|---|
| `{{PRIMARY_DIFFERENTIATOR_HEADLINE}}` / `{{PRIMARY_DIFFERENTIATOR_META_CLAUSE}}` | Same open decision as `/ad-ap-automation`. Must resolve to the **same** differentiator on both pages for account-wide consistency. | Marketing / positioning lead |

## Enterprise proof stats — need sourcing, none may be invented

| Token | Needs |
|---|---|
| `{{STAT_ENTITY_COUNT_SUPPORTED}}` | A citable maximum (or "no hard limit") for entities supported on one platform. Used twice: capability grid and stat strip. |
| `{{STAT_INVOICE_VOLUME_THRESHOLD}}` | The actual invoice-volume ceiling/range Yooz is built for at enterprise scale. |
| `{{SECURITY_CERTIFICATION_BADGE}}` | The real, current certification (e.g. SOC 2 Type II) — do not render a badge or claim a certification without Legal/Security sign-off. Render as an explicit "unverified" state if the current status can't be confirmed before shipping (see the sibling `/ad-yooz` project's `README.md` for the precedent on this — that build hit the exact same gap). |
| `{{IMPLEMENTATION_TIMELINE_ENTERPRISE}}` | A real, typical enterprise rollout timeline. |

## Customers and quotes

| Token | Needs |
|---|---|
| `{{CUSTOMER_QUOTE_ENTERPRISE_1..2}}` / `{{CUSTOMER_NAME_ENTERPRISE_1..2}}` / `{{CUSTOMER_TITLE_1..2}}` / `{{CUSTOMER_COMPANY_1..2}}` | Real, permissioned enterprise/multi-entity customer quotes — should not reuse the exact same three quotes as the parent page verbatim if the same visitor could plausibly see both pages during comparison shopping. |

## Shared with `/ad-ap-automation` (not repeated here in full)

`{{ERP_LOGO_*}}`, `{{AD_HEADLINE_*}}`, `{{AD_DESCRIPTION_*}}`,
`{{COMPANY_ADDRESS}}` — same requirements as the parent page.
