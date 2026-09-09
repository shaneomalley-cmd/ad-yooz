# Placeholders — `/ad-invoice-approval`

Every `{{TOKEN}}` used in `index.html`, per 00-FOUNDATION.md section 2 (claims discipline).

| Token | Where | What's needed | Owner |
|---|---|---|---|
| `{{COMPANY_ADDRESS}}` | Footer | Physical business address for the US/NORAM entity, required for QS transparency/navigability (foundation §3.4) and general legal footer requirements. | Legal / Marketing ops |

## Not tokenized — verified facts used directly

Per 00-FOUNDATION.md section 2, these two facts are brand-doc-verified and stated directly rather than as placeholders:

- "connects to more than 250 financial systems" — Section 3 ("Where it sits in the suite").

## Deliberately not included on this page

No customer names, logos, G2 rating, review count, pricing, or statistics appear on
this page. 07-capability.md scopes proof for capability pages to *product screenshots,
demo loop, and configuration detail* — not testimonials or third-party ratings — so
none were added or tokenized. If a future revision adds a testimonial or rating badge,
add the corresponding `{{CUSTOMER_NAME_...}}` / `{{G2_RATING}}` tokens at that time
rather than inventing values now.

## Non-content placeholders (not double-brace tokens, tracked separately)

- Two labelled image placeholders per the brand's imagery policy (00-FOUNDATION.md
  §1, "Imagery — placeholder policy"), not claims tokens:
  - Hero: `SCREENSHOT — approval queue with parallel and line-level routing visible`
  - Proof section: `SCREENSHOT — delegation and threshold rules panel, approval limits by role visible`
- Ad headline continuity comment block at the top of `index.html` (`{{AD_HEADLINE_1..3}}`,
  `{{AD_DESCRIPTION_1}}`) is a build note for the copy team, not rendered page content —
  see NOTES.md.
