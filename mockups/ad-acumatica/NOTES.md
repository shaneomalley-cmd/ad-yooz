# Build notes — /ad-acumatica

## Gated — read this first

Per 08-fit-erp.md: "**Acumatica:** held pending the price-list decision.
Build the mockup, flag it as gated." This page is built to the same
standard as the other four ERP pages so review and future un-gating is
mechanical, but it should not be treated as launch-ready:

- A dashed red banner sits at the very top of `index.html`, above the
  header, marked `MOCKUP REVIEW ONLY — GATED`. It is a reviewer-facing
  flag, not customer copy, and must be deleted before this page ever
  serves traffic.
- The named-customer section (section 4) is deliberately left as an
  explicit `{{MISSING — no reference customer on this ERP}}` marker rather
  than a normal tokenized quote, since no Acumatica reference customer
  currently exists — per the brief's instruction not to borrow one from
  another ERP.
- Ad headline placeholders assume the Acumatica ad group may not exist
  yet in the live account.

Un-gating checklist (for whoever picks this up once pricing is resolved):
1. Confirm the price-list decision and update pricing-adjacent copy if it
   depends on the outcome (this build made no pricing claims either way —
   worth a re-read once the decision lands, since the resolution could
   introduce a pricing angle this build didn't anticipate).
2. Remove the gated banner and its HTML comment block note.
3. Fill placeholders per PLACEHOLDERS.md, including securing an Acumatica
   reference customer.
4. Confirm the ad group and RSA headlines exist before pointing traffic
   here.

## Design plan

Identical composition and validated layout patterns to the other four ERP
pages (Primary → Blue form band; `minmax(0, …)` grid tracks; module-card
column-stack below 640px) — consistency across the set matters more here
than novelty, since this page will eventually need to look like a sibling
of ad-netsuite/ad-sap/ad-quickbooks/ad-microsoft-dynamics, not a rushed
afterthought.

## Checked against the archetype brief

- **Query echo:** H1 contains "Acumatica AP automation" verbatim.
- **Do-not #1:** screenshots, sync table and capability block use
  Acumatica-specific vocabulary (branches, subaccounts, cloud xRP API) —
  not a renamed NetSuite or SAP page.
- **Do-not #2:** no ERP × capability page section built.
- **"If a given ERP has no customer reference yet, mark the slot
  `{{MISSING — no reference customer on this ERP}}`"** — followed exactly
  in section 4.

## QS checklist

1. **Query echo in H1** — "Acumatica AP automation" verbatim.
2. **Title/meta** — title "Acumatica AP Automation | Yooz" (32 chars);
   meta description ~125 chars, contains "Acumatica AP automation."
3. **Ad-to-page continuity** — comment block with placeholder ad headline
   slots, plus the gated flag.
4. **Transparency/navigability** — standard header/footer, unaffected by
   the gated banner.
5. **Mobile parity** — verified at 390px, zero non-table overflow. The
   gated banner itself wraps cleanly at narrow widths (tagline-sized text,
   no fixed width).
6. **Speed posture** — single file, ~15KB, no JS, no raster images.
7. **Accessibility floor** — one `<h1>`, semantic landmarks, skip link,
   scoped table headers, labelled fields, focus-visible via tokens.css.
   The gated banner uses `role="note"` so assistive tech announces it as
   supplementary rather than the page's primary content.

## Open questions

- Whether the price-list decision, once made, changes anything about this
  page's messaging beyond the standard placeholders — flagged above.
- No Acumatica reference customer exists; this is a harder blocker than
  the other four pages' "supplied later" placeholders since it's a known
  gap, not just an unfilled token.
