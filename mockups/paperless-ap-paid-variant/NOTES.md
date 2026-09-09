# Build notes — `paperless-ap-paid-variant` (archetype 06, Modernisation)

## Plan (written before code)

**Layout concept:** primary composition — Pattern BG page background, a
single Grey 10 bounding box holding the hero. Two-column: copy left,
before/after visual right, doubling as the hero image slot instead of a
generic Z-cutout product photo, since the competing alternative here is
the status quo (filing cabinets), not a competitor — a literal
paper-to-digital visual is more relevant hero art than a graded lifestyle
cutout would be.

**ASCII wireframe (first/only screen):**

```
[wordmark]                 Product  Pricing  Lean Advantage  [Book a demo]
┌─────────────────────────────────────────────────────────────┐
│  Still running accounts payable on paper?        [BEFORE/    │
│  Accounts payable, off paper / and fully digital   AFTER     │
│  See what changes on day one...                    Z-visual] │
│  Purchase, capture, review, approve — same steps...           │
│  [Book a demo]   Download the paperless AP guide →            │
└─────────────────────────────────────────────────────────────┘
  ↓ page continues unchanged (existing live content, not mocked up)
```

**Section order used:** hero only. 06's actual section order (before/after
→ day-one changes → product → proof → form) belongs to the *existing*
live page and is explicitly out of scope to rebuild — this file mocks up
only the recommended change to the first screen.

## Checked against the brief

- "First screen must do": leads with the paper-to-digital transition in
  the visitor's own language ("still running... on paper" /
  "off paper and fully digital"). No automation vocabulary anywhere in
  the eyebrow, H1, or subhead — confirmed by re-reading the copy above.
- "Do not": did not rebuild the page. No product section, no proof
  section, no form was built — the continuation strip explicitly says the
  rest of the page is unchanged and not mocked up.

## Query-echo trade-off (flagged, not hidden)

Two of the seven head terms for this campaign pairing ("automated ap
processing," "accounts payable process automation") contain automation
vocabulary the brief instructs the headline to avoid. Resolved in favor
of the brief's explicit psychological instruction over literal-string QS
matching: H1 anchors on "accounts payable" + "digital"/"cloud," which
covers 5 of 7 terms inflectionally. This is a judgement call — flagging
per the brief's instruction to note departures — and should be revisited
against real QS data for the 04b ad group specifically after launch.

## QS checklist confirmation (for the elements this mockup touches)

1. Query echo in H1 — partial by design; see trade-off above.
2. `<title>`/meta description — both contain "digital accounts payable" /
   "accounts payable"; title 47 chars, description 132 chars, both under
   the stated limits.
3. Ad-to-page continuity — HTML comment block added at top of file;
   left as `{{TOKEN}}`s pending real ad copy (see PLACEHOLDERS.md).
4. Transparency/navigability — persistent header with wordmark linking to
   getyooz.com present. Footer not mocked up (out of scope — lives on the
   unchanged rest of the page).
5. Mobile parity — verified at 390px: header wraps, hero box collapses to
   single column, annotation tags become inline instead of absolutely
   positioned, primary CTA stacks full-width, no horizontal scroll.
6. Speed posture — single self-contained HTML file, one external
   stylesheet link (`tokens.css`, shared system file) plus Google Fonts
   with `display=swap`. No JS. Estimated page weight: ~9KB HTML + ~6KB
   tokens.css, negligible vs. font load.
7. Accessibility floor — one `<h1>`, semantic `<header>`/`<main>`,
   labelled nav, focus-visible ring from tokens.css, placeholder image
   has a descriptive `aria-label` and caption, `prefers-reduced-motion`
   respected in tokens.css (no motion used on this page regardless).

## Open questions

- Real live-page source for `/paperless-accounts-payable` wasn't
  available to this session, so the "annotation" callouts describe the
  recommended change directly rather than diffing against actual current
  copy. Before shipping, paste the current H1/eyebrow/CTA text next to
  this mockup for a literal side-by-side.
- Whether the existing page's demo form is 3–4 fields already (06's spec)
  or matches some other field count — not verified, since the live page
  wasn't inspected this session.

## Departures from `00-FOUNDATION.md` §6 output spec

Section 6 specifies `index.html` + full `PLACEHOLDERS.md` + `NOTES.md`
per archetype, assuming each archetype is a full page. 06's own brief
overrides that explicitly ("Produce two things only... if you find
yourself building a full page here, stop"), so the HTML file here is
named `above-fold-mockup.html` rather than `index.html` to signal it's a
partial screen, not a deployable page.
