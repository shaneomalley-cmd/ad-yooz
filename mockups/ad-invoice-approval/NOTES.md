# Notes — `/ad-invoice-approval` (Archetype 07, Capability)

## Status: shared tokens didn't exist yet

`/mockups/_system/tokens.css` did not exist in this repo before this build — no
archetype has been built yet, including archetype 01 (Brand), which per
00-FOUNDATION.md §6 is supposed to originate `tokens.css` *and*
`/mockups/_system/components.html` (the live specimen sheet). Since this page
can't function without the token file, `tokens.css` was created here, but
**scoped strictly to values 00-FOUNDATION.md section 1 already specifies
explicitly** (colour, fluid type scale, buttons, dot patterns, Z geometry,
layout compositions, focus state) — nothing was invented for this page.
`components.html` was **not** built in this pass; it's still owed, ideally when
archetype 01 gets built, and should consume the same custom properties rather
than re-deriving them. Flagging this as the one place this build stepped
outside its own archetype's scope, and why.

## Design plan (written before code, per foundation §5)

**Brand composition:** Primary layout (Pattern BG page background, Grey 10
content boxes, Rich Blue type, Pink CTA) — as specified for archetype 07.

**Layout concept:** The brief is explicit that the first screen must *show the
capability working*, not sell it — "the image slot outranks the headline in
visual hierarchy" is the one archetype where that's stated outright. So the
hero H1 is set at the H3 scale (48px→28px fluid) rather than the full 84px H1
scale: it stays a single semantic `<h1>` for QS/SEO, but is sized down so a
large, correctly-proportioned screenshot can sit in the same first screen as
the headline block, rather than pushing the screenshot below the fold. The
screenshot frame is the largest single Grey 10-adjacent element on the page.

**ASCII wireframe, first screen (desktop):**

```
┌──────────────────────────────────────────────────────────┐
│ yooz.                          Pricing  Lean Adv.  [Demo] │ header
├──────────────────────────────────────────────────────────┤
│ ░░░░░░░░░░░░░░░░░░ pattern-bg ░░░░░░░░░░░░░░░░░░░░░░░░░░░ │
│  ┌────────────────────────────────────────────────────┐  │
│  │ Grey10 box                                          │  │
│  │  For teams ready to see the approval queue…(eyebrow)│  │
│  │  Invoice approval software you can watch work. (H1) │  │
│  │  Parallel routing, line-level routing… (H4)         │  │
│  │  This is the actual approval queue… (p)              │  │
│  │  [Book a demo]   Read the approval workflow guide → │  │
│  │  ┌────────────────────────────────────────────────┐ │  │
│  │  │                                                  │ │  │
│  │  │        SCREENSHOT (largest element)  ▶           │ │  │
│  │  │                                                  │ │  │
│  │  └────────────────────────────────────────────────┘ │  │
│  │  caption: SCREENSHOT — approval queue with…          │  │
│  └────────────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────────────┘
```

**Section order (matches brief exactly):**
1. Capability in action (hero + screenshot)
2. How it works (4-step routing sequence — numbered, because it's a genuine
   sequence per foundation §5's "numbered markers only where genuinely a
   sequence" rule)
3. Where it sits in the wider suite (short: one paragraph, the six-stage
   strip with Approve highlighted, one tertiary link — deliberately the
   shortest section on the page)
4. Proof (2×2 config-depth grid + a second, differently-captioned screenshot)
5. Form (5–6 fields, demo request)

Checked against the brief's "Do not" list before writing code:
- *"Pitch the whole platform before proving the one capability"* — section 3
  is one paragraph + a link, placed after the mechanism and the proof, not
  before it.
- *"Same hero copy across the four capability pages with the noun swapped"* —
  hero copy here is approval-specific throughout (parallel/line-level
  routing, delegation, thresholds, audit trail — the actual approval
  mechanism), not a generic capability template with "invoice approval"
  dropped in.

## Copy sourcing

All mechanism claims (parallel routing, line-level routing, delegation,
thresholds, audit trail) come directly from 07-capability.md's own proof list
("parallel and line-level routing, delegation, thresholds, audit trail") —
none invented. The one verified stat used ("more than 250 financial systems")
is the fact 00-FOUNDATION.md §2 explicitly clears for direct use. No stat,
customer, or rating was fabricated; see PLACEHOLDERS.md.

## Quality Score checklist (00-FOUNDATION.md §3)

1. **Query echo in H1** — ✅ "Invoice approval software" appears verbatim as
   the opening clause of the H1.
2. **Title/meta description** — ✅ Title "Invoice Approval Software | Yooz"
   (34 chars). Meta description (142 chars) contains "invoice approval
   software" and stays under 155.
3. **Ad-to-page continuity** — ✅ HTML comment block at top of `index.html`
   lists placeholder ad headline slots for the copy team to fill once real ad
   copy exists.
4. **Transparency/navigability** — ✅ Persistent header with Yooz wordmark
   linking to getyooz.com; footer with Privacy Policy, Terms, Contact, and an
   address placeholder. No interstitials, no scroll-jacking, no audio.
5. **Mobile parity** — ✅ Hero stacks to one column; H1/subhead/CTA and the
   screenshot are both reachable within the first two mobile screens (copy
   block first screen, screenshot early in screen two). Step rail: 4→2→1
   columns at 900px/520px. Proof grid: 2→1 column at 720px. Tap targets: CTA
   buttons and inputs are ≥44px min-height.
6. **Speed posture** — ✅ Single self-contained HTML file + one shared CSS
   file (no per-page duplication of tokens); Google Fonts loaded with
   `display=swap`; no JS at all (mobile nav needs none — see below); all
   patterns/Z geometry/icons are CSS or the Material Symbols web font, no
   raster images. Estimated page weight: ~9KB HTML + ~6KB shared CSS
   (amortized across every future page that imports it) + Google Fonts
   (Noto Sans 3 weights + Material Symbols subset, network-cached across
   pages once a visitor has loaded one).
7. **Accessibility floor** — ✅ One `<h1>`; semantic `header`/`main`/`section`/
   `footer` landmarks with `aria-labelledby`; visible `:focus-visible` (Pink,
   2px, 2px offset) from tokens.css; `prefers-reduced-motion` respected in
   tokens.css; all form inputs labelled; both screenshot placeholders carry
   descriptive `role="img"` + `aria-label` text (not decorative `alt=""`,
   since they stand in for real content images).

## Deliberate departures flagged (per 00-FOUNDATION.md §1)

- **Light-weight-below-24px risk**: the proof grid and step-rail body copy
  use `.t-p` (17px, Regular 400), not `.t-list` (16px Light) — this counts as
  a "dense data block" of configuration detail per the departure note, so it
  steps up to Regular rather than using Light at that size.
- **Fluid H1/Display**: `tokens.css` implements the clamp-based fluid scale
  for Display, H1, H2, and H3 (H2/H3 included proactively, since this page's
  H1 is set at the H3 scale and needs the same mobile-fit treatment as a true
  H1 would). H4 and smaller are left static since they already fit a 390px
  viewport per the brief.

## No JS

The header has no hamburger/mobile-menu toggle. Instead the two secondary nav
links (Pricing, The Lean Advantage) are hidden below 720px via CSS, while the
wordmark and the primary "Book a demo" CTA stay visible at every width —
avoids a JS dependency for something that isn't this archetype's job (a
capability page's only job above the fold is the screenshot + one CTA).

## Instrumentation (`data-yooz-event`)

Primary conversion action (demo request): `cta-hero-demo-primary`,
`cta-form-demo-primary`, `nav-cta-demo-primary` — all point at the same goal
(the form at `#demo-form`).
Secondary/lower-value: `cta-hero-guide-secondary`, `cta-form-guide-secondary`
(feature-specific guide, per the brief's stated secondary conversion),
`cta-suite-platform-tertiary` (platform overview, lowest-commitment link on
the page).

## Open questions / dependencies for whoever schedules this campaign

1. **NEG-06-DIY-TOOLS dependency (blocking).** 07-capability.md states this
   page shouldn't take traffic until that negative-keyword list is live —
   Adobe Acrobat ranks #2 and Jotform ranks #7 on approval head terms, so a
   real slice of query volume is signing-PDF or form-builder intent, not
   AP-platform intent. This is a paid-media/account-structure task, not a
   page-content one — nothing on the page itself can filter that traffic;
   flagging here per the brief's instruction to note the dependency.
2. **`/ad-po-matching` and `/ad-ap-payments`** were *not* built as standalone
   pages, per the brief's own recommendation (5 keywords, a 12-result
   educational SERP with zero product pages for matching; payments SERP
   resolves to `/ad-ap-automation`). Not addressed in this pass since this
   task's scope was `/ad-invoice-approval` specifically — flagging so a PO
   matching section on this page, and the `/ad-ap-payments` → `/ad-ap-automation`
   redirect/pointer, are tracked as separate follow-ups rather than assumed
   done.
3. **`/ad-invoice-capture`** (the next page in this archetype's build order)
   is not started. This page's proof section deliberately does not encroach
   on capture-specific claims (OCR, multi-channel ingestion) to leave that
   page its own capability to prove.

## Breakpoints verified (visual inspection of the CSS, not a live browser)

1440px (design target), 1024px, 768px, 390px — grid columns for the step
rail (4/2/1) and proof grid (2/1) collapse at 900px/720px respectively, ahead
of the 768px checkpoint, so both land cleanly at every named breakpoint.
