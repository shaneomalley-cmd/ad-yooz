# Build notes — `/ad-ap-comparison` (archetype 11, Proof/list)

## Design plan (written before code, per 00-FOUNDATION §5)

**Layout concept:** no hero. The comparison table is the first screen,
built as a Grey 10 bounding box on Pattern BG — the brand's own
structural device, sized to its importance (the largest box on the
page). This is the page's single most counter-intuitive instruction and
the whole build is organized around not fighting it.

**Brand composition:** primarily the *Primary layout* (Pattern BG ground,
Grey 10 content boxes, Rich Blue type, Pink accent/CTA). One section
(the "choose someone else if" column) borrows the *Blue layout*
(Rich Blue box, Grey 10 type) to give the disqualifier visual weight
without coding it as alarming — it's a different path, not a warning.

**ASCII wireframe, first screen (desktop):**

```
┌─────────────────────────────────────────────────────────────┐
│ yooz                                        [Book a demo]   │ ← sticky header
├─────────────────────────────────────────────────────────────┤
│  ● AP automation vendor comparison (eyebrow)                 │
│  Best accounts payable automation software, compared (H1)    │
│  Six vendors, one table, sorted alphabetically... (subhead)  │
│ ┌───────────────────────────────────────────────────────┐   │
│ │ Compare AP automation software    Sorted alphabetically│   │
│ │ ┌───────────────────────────────────────────────────┐ │   │
│ │ │ Vendor │G2│Capterra│ERPs│Channels│Focus│Best for│$│ │   │ ← Rich Blue header
│ │ │ Airbase│..................................................│ │   │
│ │ │ Bill.com│.................................................│ │   │
│ │ │ Ramp   │..................................................│ │   │
│ │ │ Stampli│..................................................│ │   │
│ │ │ Tipalti│..................................................│ │   │
│ │ │▐Yooz  │.................................................│ │   │ ← pink marker
│ │ └───────────────────────────────────────────────────┘ │   │
│ │ Last checked [date]           Get the full guide →    │   │
│ └───────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

**Section order (matches brief exactly):**
1. Comparison table (first screen, no hero)
2. Third-party validation ("Recognition, not a ranking claim")
3. Where Yooz fits — and where it does not
4. Analyst position (Gartner MQ statement)
5. Form (gated guide, primary; demo, secondary)

**Check against "First screen must do" / "Do not":**
- ✅ Table above the fold, includes vendors Yooz loses to.
- ✅ No hero — table is the first screen.
- ✅ Not a single-vendor pitch — five competitors get full rows.
- ✅ Sort is alphabetical (neutral) and disclosed inline, both above the
  table and repeated as a footnote-style tag next to the table title.
- ✅ Bill.com and Tipalti both present (named explicitly in the ad-group
  brief as vendors visitors expect to see), plus Ramp (its own ad group),
  plus Airbase and Stampli for shortlist credibility — six rows total,
  none omitted.

## QS checklist confirmation (00-FOUNDATION §3)

1. **Query echo in H1** ✅ — H1 is "Best accounts payable automation
   software, compared," containing the head keyword verbatim.
2. **Title/meta contain head keyword** ✅ — `<title>` = "Best Accounts
   Payable Automation Software, Compared | Yooz" (58 chars). Meta
   description contains the same phrase (149 chars, under 155).
3. **Ad-to-page continuity** — comment block at top of `index.html`
   left for the copy team to fill with the actual live ad headlines per
   ad group; the on-page promise (neutral multi-vendor comparison) is
   written to match what that ad copy should be promising.
4. **Transparency/navigability** ✅ — persistent header with Yooz
   wordmark linking to getyooz.com; footer with Privacy Policy, Terms,
   Contact and a `{{BUSINESS_ADDRESS}}` placeholder. No interstitials,
   no scroll-jacking, no autoplay.
5. **Mobile parity** ✅ — table becomes a horizontally-scrollable region
   with a sticky first column and a visible (and, respecting
   `prefers-reduced-motion`, animated) scroll affordance below 768px,
   per the brief's explicit instruction for this page (not the
   stacked-card alternative, since the brief calls for horizontal
   scroll with sticky column specifically). Fit-grid collapses to one
   column under 1024px. All tap targets ≥44px.
6. **Speed posture** ✅ — single self-contained HTML file plus one
   shared `tokens.css` (meant to be cached across every archetype page,
   not re-downloaded weight). Fonts loaded via Google Fonts with
   `display=swap`. Material Symbols loaded with the `media="print"`
   swap trick to avoid render-blocking. No JS at all — the scroll
   affordance and focus states are pure CSS. Page weight: `index.html`
   ~24KB uncompressed, `tokens.css` ~7KB (shared across all pages, not
   a per-page cost).
7. **Accessibility floor** ✅ — one `<h1>`, semantic `<header>/<main>/
   <footer>`, table has `scope="col"` headers and a `role="group"`/
   `aria-label` on the scroll container, skip link, Pink 2px focus
   outline with 2px offset (defined once in `tokens.css`), all decorative
   icons `aria-hidden`, form input labelled, `prefers-reduced-motion`
   respected for the one motion moment on the page (the scroll-affordance
   nudge, mobile-only).

## Claims discipline

Every comparative number (competitor ratings, integration counts,
capture channels, dedicated-AP-focus determination, best-for line,
pricing model) is a `{{TOKEN}}` — see `PLACEHOLDERS.md`. The only
non-tokenised facts on the page are Yooz's own two brand-guideline-
verified claims (250+ financial systems; the eight-channel capture
list) and the awards/partner names, which the brief explicitly says
"are real and can be named rather than tokenised." Dated awards carry
their year as a visible badge rather than being presented as current.

## Departures / decisions flagged

- **`/mockups/_system/tokens.css` did not exist yet.** The foundation
  document assumes archetype 01 (Brand) is built first and emits this
  file plus `components.html`. This session was asked to build
  archetype 11 directly, so `tokens.css` was created from scratch,
  scoped to exactly what this page needed: colour tokens, the fluid
  type scale, the three dot patterns, buttons, form fields, the Grey 10
  bounding box, focus states, and the shared header/footer shell.
  **`components.html` (the full specimen sheet) was intentionally not
  built** — it's explicitly an archetype-01 deliverable and out of
  scope for a single-archetype request. When archetype 01 is actually
  built, reconcile its tokens.css against this one (they should be
  identical or additive) rather than overwriting it blindly.
- **Sort chosen: alphabetical**, not by review count or any other
  metric. The brief requires disclosing a neutral sort; alphabetical is
  the only sort that requires no data we don't already have verified,
  and it's immediately legible as non-manipulated (Yooz lands last,
  which is itself part of the honesty signal).
- **Table responsive pattern:** brief's own "Brand composition" section
  specifies horizontal scroll + sticky first column for this page
  specifically, so that pattern was used instead of 00-FOUNDATION §3's
  general fallback of "stacked card list" for comparison tables.
- **Two-tone H1 not used.** Per 00-FOUNDATION §2b, a single-tone Rich
  Blue H1 is correct "when the headline is a query echo that shouldn't
  be visually broken" — this H1 is exactly that case.
- **Header CTA is secondary-styled** ("Book a demo," Pink-outline, not
  filled), so it doesn't compete with the page's one primary action
  (the gated guide download) while still giving high-intent visitors an
  always-available faster path.
- **The Gartner statement (`{{GARTNER_POSITION_STATEMENT}}`) is left
  as an explicit token rather than drafted**, because 00-FOUNDATION
  and the archetype brief both frame this as needing "a real, honest
  sentence from the team" — this is the one sentence on the page where
  a plausible-sounding placeholder would be actively worse than an
  obvious blank, since it's the line most likely to get copied into
  production verbatim under deadline pressure.

## Open questions for the content/legal owner

1. What is the real `{{MIN_INVOICE_VOLUME_THRESHOLD}}`? This is a
   genuine disqualifier claim (per the brief: "genuinely specific: if
   you are under N invoices a month") and needs a defensible number
   from Sales, not a marketing-picked round figure.
2. Who owns pulling competitor G2/Capterra ratings on a recurring
   cadence so this table doesn't go stale the week after launch? The
   brief flags several Yooz awards as already dated; the competitor
   data is even more perishable.
3. Confirm the exact, correctly-named Gartner MQ category
   (`{{GARTNER_MQ_CATEGORY_NAME}}`) before this ships — naming the
   wrong category is its own credibility risk with this visitor.
4. Per the brief: the guide download must be tracked as a **real
   conversion action with its own value**, not a micro-conversion —
   flagging here again since campaigns 10–13 apparently have no other
   optimization signal without it. `data-yooz-event="guide_download_submit"`
   is the primary conversion hook; `data-yooz-event="header_book_demo"`
   and `data-yooz-event="form_book_demo_instead"` are the secondary
   (demo) conversion hooks.
