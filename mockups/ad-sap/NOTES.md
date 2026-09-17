# Build notes — /ad-sap

## Design plan

Same composition strategy as `/ad-netsuite`: Primary layout for the top
five sections, Blue layout for the form band. Reused the validated grid/
flex fixes from that build (see below) rather than re-deriving them.

**ASCII wireframe, first screen (1440px):** structurally identical to
ad-netsuite's — hero copy left, Z-image right, two CTAs, trust row —
with SAP-specific copy substituted throughout.

**Section order** matches the brief: ERP hero → connector/screenshots →
two-way sync table → named customer → capability block → form.

## Checked against the archetype brief

- **Query echo:** H1 contains "SAP AP automation" verbatim.
- **Do-not #1:** screenshots, sync table and capability block are SAP-
  specific — SAP table/transaction vocabulary (LFA1/LFB1 vendor master,
  cost centers, MM purchase order/goods receipt, F110 payment run) rather
  than the NetSuite page's SuiteApp language. No shared boilerplate beyond
  the design system.
- **Do-not #2:** no ERP × capability page section built.
- **Exemplar note:** stampli.com/erp/sap-business-one/ leans heavily on
  integration mechanics over product marketing — this page follows that
  ratio (2 of 6 sections are pure connector/sync proof).

## Claims discipline correction made during build

Two lines were drafted as bare marketing claims and then caught and
tokenized before finalizing, per 00-FOUNDATION.md §2:
- "SAP-certified integration" → `{{SAP_CERTIFICATION_CLAIM}}`, since no
  certification status was supplied and this is a substantiable claim in
  finance software.
- "Certified for SAP FI and MM" → rewritten to "Built on standard SAP
  interfaces," a defensible statement about architecture rather than an
  unverified certification claim.

## QS checklist

1. **Query echo in H1** — "SAP AP automation" verbatim.
2. **Title/meta** — title "SAP AP Automation | Yooz" (27 chars); meta
   description ~130 chars, contains "SAP AP automation."
3. **Ad-to-page continuity** — comment block at top with placeholder slots
   for the live SAP ad group's RSA headlines.
4. **Transparency/navigability** — same persistent header/footer as every
   other page in the system.
5. **Mobile parity** — verified at 390px using the same layout patterns
   validated on ad-netsuite (grid tracks use `minmax(0, …)`, the module
   card stacks to a column below 640px, `.btn-tertiary` has an
   `overflow-wrap` safety net). No horizontal scroll outside the
   intentional sync-table region.
6. **Speed posture** — single file, ~14KB, no JS, no raster images.
7. **Accessibility floor** — one `<h1>`, semantic landmarks, skip link,
   scoped table headers with caption, labelled form fields, focus-visible
   inherited from tokens.css.

## Conversion mechanics

Same as ad-netsuite: primary demo-request form (6 fields), secondary
integration one-pager tertiary link, `data-yooz-event` on both CTAs and
the form.

## Open questions

- Whether Yooz's SAP certification status supports any claim stronger than
  "built on standard SAP interfaces" — needs product/legal confirmation.
- Sync frequency values are tokenized pending engineering confirmation.
- No SAP reference customer was supplied for this build; per the brief,
  replace the customer block with the explicit missing-reference marker
  if none exists by ship time rather than borrowing NetSuite's quote.
