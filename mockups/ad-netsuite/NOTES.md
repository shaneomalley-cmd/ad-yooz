# Build notes — /ad-netsuite

## Design plan

**Layout concept.** Primary composition (Pattern BG ground, Grey 10 boxes)
for the top five sections; switches to Blue composition for the form band
so the conversion ask reads as a distinct final beat rather than blending
into the capability section above it.

**ASCII wireframe, first screen (1440px):**

```
┌─────────────────────────────────────────────────────────┐
│ yooz                          The Lean Advantage  Pricing│
├─────────────────────────────────────────────────────────┤
│  Built for teams already running NetSuite                │
│  NetSuite AP automation │ that connects natively,         │      ┌─────────────┐
│                          not bolted on.                   │      │   Z-shape   │
│  See the exact fields that sync before you book a call.  │      │  hero image │
│  Yooz runs inside NetSuite... vendor master, GL codes...  │      │  placeholder│
│  [Book a demo]  [See the connector →]                     │      └─────────────┘
│  ⟳ Exports to 250+ financial systems  🏬 SuiteApp listed  │
└─────────────────────────────────────────────────────────┘
```

**Section order** matches the brief exactly: ERP hero → connector/
screenshots → two-way sync table → named customer → capability block →
form. No deviation.

## Checked against the archetype brief

- **First screen does what's required:** ERP named in the H1 (verbatim
  query echo, "NetSuite AP automation"), and the hero shows the connector
  claim ("connects natively") rather than opening with generic AP-automation
  product marketing. Integration proof is promised above the fold and
  delivered in section 2.
- **Do-not #1 (generic page, name swapped in):** this page's screenshots,
  sync-frequency column, capability block and customer slot are all
  NetSuite-specific content, not shared boilerplate. The capability block
  (multi-subsidiary, NetSuite role mapping, saved-search compatibility) is
  genuinely NetSuite-only and does not appear on the other four ERP pages.
- **Do-not #2 (ERP × capability content):** no "NetSuite – matching" or
  similar capability-specific section was built; the capability block stays
  at the level of "why NetSuite specifically," not a feature-by-feature
  page.
- **Per-page note — capability block:** included per the brief's NetSuite-
  specific instruction.
- **Per-page note — SuiteApp marketplace listing:** added as its own
  callout in section 2 with a placeholder URL, flagged in PLACEHOLDERS.md
  that the listing needs to be confirmed live before this page ships
  (competitor Medius currently ranks #5 on the head term per the brief).

## QS checklist

1. **Query echo in H1** — "NetSuite AP automation" appears verbatim in the H1.
2. **Title/meta** — title 29 chars, contains "NetSuite AP Automation";
   meta description ~127 chars, contains "NetSuite AP automation."
3. **Ad-to-page continuity** — comment block at top of `index.html` with
   placeholder slots for the live RSA headlines; copy team to fill.
4. **Transparency/navigability** — persistent header (wordmark → getyooz.com)
   and footer (Privacy/Terms/Contact/address) present on every screen.
5. **Mobile parity** — hero, both CTAs and the trust row all sit within the
   first two mobile screens at 390px; sync table becomes a horizontally
   scrollable region with a sticky first column rather than a squashed grid.
6. **Speed posture** — single file, Google Fonts loaded with `display=swap`,
   no JS, no image assets (placeholders are gradient/clip-path only).
   Estimated page weight: ~14KB HTML (uncompressed), plus two Google Fonts
   requests (Noto Sans + Material Symbols). No build step.
7. **Accessibility floor** — one `<h1>`, semantic `<header>/<main>/<footer>`,
   skip link, table has a `<caption>` and scoped headers, form inputs
   labelled, focus-visible outline inherited from tokens.css (Pink 2px,
   2px offset), `prefers-reduced-motion` respected globally via tokens.css
   (this page adds no motion of its own).

## Conversion mechanics

- Primary: demo request form, 6 fields (first, last, work email, company,
  monthly invoice volume, phone optional) — correct for high-intent
  awareness tier per 00-FOUNDATION.md §4.
- Secondary: integration one-pager download, tertiary link, placed above
  the form so it's available to a visitor not ready to book yet.
- `data-yooz-event` attributes set on both CTAs, the marketplace link, the
  one-pager link and the form itself.

## Open questions

- Whether the SuiteApp Marketplace listing is live yet — if not, section 2's
  marketplace callout should be cut rather than link to nothing.
- Sync frequency values (real-time vs. batch) need engineering confirmation
  per field; currently all five rows are tokenized rather than guessed.
- No NetSuite reference customer was supplied for this build; the customer
  block is fully tokenized and should be replaced with the explicit
  `{{MISSING — no reference customer on this ERP}}` marker if none exists
  by ship time, per the brief's instruction not to borrow a quote from
  another ERP's customer.
