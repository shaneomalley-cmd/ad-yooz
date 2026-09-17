# Build notes — /ad-microsoft-dynamics

## Design plan

Same composition and validated layout patterns as ad-netsuite/ad-sap/
ad-quickbooks (Primary → Blue form band; `minmax(0, …)` grid tracks;
module-card column-stack below 640px). No new layout risk introduced —
this build focused on content correctness for a two-headword page.

**ASCII wireframe:** structurally identical to the other three pages —
hero copy left, Z-image right, two CTAs, trust row.

## Checked against the archetype brief

- **Query echo:** H1 contains "Dynamics 365 AP automation" verbatim,
  satisfying the primary head term.
- **Secondary term ("d365 invoice automation"):** this ad group and page
  serve both `dynamics 365 ap automation` (primary, in the H1) and `d365
  invoice automation` (secondary, lower volume). Rather than a separate
  section — which the brief's "do not build ERP × capability content"
  guidance argues against by extension — the secondary term is woven into
  section 2's H2 ("What D365 invoice automation actually looks like"),
  keeping continuity for that query without fragmenting the page.
- **Do-not #1:** screenshots, sync table and capability block are
  Dynamics-365-specific (financial dimensions, legal entity, F&O/Business
  Central parity) — not a renamed NetSuite or SAP page.
- **Do-not #2:** no ERP × capability page section built.

## QS checklist

1. **Query echo in H1** — "Dynamics 365 AP automation" verbatim.
2. **Title/meta** — title "Dynamics 365 AP Automation | Yooz" (34 chars);
   meta description ~130 chars, contains both "Dynamics 365 AP
   automation" and "D365 invoice automation."
3. **Ad-to-page continuity** — comment block at top with placeholder ad
   headline slots; also documents the secondary-term handling for the
   copy team.
4. **Transparency/navigability** — standard header/footer.
5. **Mobile parity** — verified at 390px, zero non-table overflow.
6. **Speed posture** — single file, ~15KB, no JS, no raster images.
7. **Accessibility floor** — one `<h1>`, semantic landmarks, skip link,
   scoped table headers, labelled fields, focus-visible via tokens.css.

## Conversion mechanics

Standard 6-field demo-request form, tertiary integration one-pager link,
`data-yooz-event` on both CTAs and the form — consistent with the rest of
the ERP set.

## Open questions

- Whether Yooz's Dynamics 365 connector has equivalent field coverage
  across F&O and Business Central — see PLACEHOLDERS.md. If coverage
  differs, "One connector, both editions" needs to be softened or split.
- No Dynamics 365 reference customer was supplied; customer block is
  fully tokenized pending one.
- Sync frequency values are tokenized pending engineering confirmation.
