# Notes — `/ad-invoice-automation` (archetype 05, Qualifier)

## Read this before judging the mockup

**This page succeeds by bouncing people.** A high bounce rate on this page is a
sign it's working, not a problem to fix. The invoice root is shared with the
SMB billing (AR) market and roughly 44% of the search terms landing here are
hidden in Google's search terms report, so no negative-keyword list can filter
them — this page is the filter. Judge it on the conversion rate of visitors who
*stay* past the "not for you if" block, and on the click rate of the
`qualifier-redirect-ar` exit link (that click rate is the actual measurement of
how much wasted spend this page is catching). Do not "fix" this page by making
it friendlier to the traffic it's designed to turn away.

## Design plan (pass 1, checked against the brief before writing code)

**Layout concept:** Primary layout (Grey 10 content, Pattern BG ground, Pink
CTA), but the brief calls for "an unusually stark first screen" — so the hero
breaks from the standard eyebrow → H1 → H4 → paragraph → buttons stack. There
is one dominant statement and nothing else competing for attention.

**ASCII wireframe, first screen (desktop):**

```
┌──────────────────────────────────────────────────────────┐
│ Yooz                              Pricing  The Lean Adv.  │  ← site-header
├──────────────────────────────────────────────────────────┤
│                     (Pattern BG, mostly empty)             │
│              Before you request a demo   (eyebrow)         │
│                                                              │
│     Invoice automation software built for AP teams          │
│     processing 500+ supplier invoices a month.  (H1,        │
│                                     H2-scale, centered)      │
│                                                              │
│   Automates Purchase→Capture→Review→Approve→Pay→Export      │
│   for teams receiving supplier invoices — not for teams      │
│   sending invoices to customers.        (short sub, small)  │
│                                                              │
│        [ Book a demo ]      See who this isn't for ↓        │
└──────────────────────────────────────────────────────────┘
```

Section order matches the brief exactly: (1) qualifying statement,
(2) "not for you if" block, (3) product, (4) proof, (5) form.

**Checked against "First screen must do":** disqualify before any pitch — yes,
the H1 *is* the volume-and-role qualifier itself, there is no product pitch
above the fold at all.

**Checked against "Do not":**
- Softened the qualifier? No — "500+" (as `{{VOLUME_THRESHOLD}}`) and the AP/AR
  distinction are stated plainly in the H1 and reinforced in the disqualifier
  block, not hedged into a subhead.
- Reassurance copy that undoes the filter? No "...but we work with teams of
  all sizes" anywhere. The proof section reinforces the volume/team-size fit
  rather than softening it.

## Deliberate departures from default patterns (flagged per brief §5)

1. **H1 set at H2's type scale (64px Light), not H1's default 84px.** The
   archetype brief is explicit: "the qualifying statement set in H2 (64px
   Light, Rich Blue)." Rather than adding a second, separate H2 for the
   qualifying statement (which would leave the page with a smaller, less
   important-looking H1 sitting above the thing that actually matters), the
   query-echo requirement and the qualifying statement were merged into a
   single `<h1>` and that element was styled at the H2 size. This satisfies
   the QS "keyword in H1" requirement, the accessibility floor (exactly one
   `<h1>` per page), and the brief's explicit sizing instruction
   simultaneously, at the cost of the H1/H2 size relationship being inverted
   from the type scale's default assumption on this one page only.
2. **No eyebrow→H1→H4→paragraph→buttons hero stack.** Per §"What is shared and
   what is not" in `00-FOUNDATION.md`, archetype 05 is named as one of the
   pages with a structurally different first screen. The H4 supporting
   subhead is dropped; a single short paragraph does that job instead, kept
   deliberately brief so it doesn't compete with the H1.
3. **Standard-weight Regular applied to `.not-for-you li` at 22px**, not the
   dense-data-block departure from §Typography (that departure targets *below
   24px*; this list runs at Paragraph Large / 22px, which is above the
   Light-weight legibility threshold, so brand Light was kept here).

## Query echo / H1 choice

The ad group serves five head terms (invoice automation software, invoice
processing software, invoice management software, automated invoice
processing, ai invoice processing software) across three ad groups sharing
this one page. "Invoice automation software" was used verbatim in the H1 as
the umbrella term closest to all three ad group names; the other four terms
recur in the meta description, product section eyebrow, and body copy so ad
relevance holds across all three ad groups landing here, not just one.

## QS checklist (`00-FOUNDATION.md` §3)

1. ✅ Query echo in H1 — "invoice automation software" appears verbatim.
2. ✅ `<title>` (54 chars) and meta description (152 chars) both contain the
   head keyword; both under the stated limits.
3. ✅ Ad-to-page continuity — HTML comment block at top of `index.html` lists
   the ad headlines this page must stay consistent with (placeholder tokens,
   for the copy team to fill from the live RSAs).
4. ✅ Persistent header (Yooz wordmark → getyooz.com) and footer (Privacy
   Policy, Terms, Contact, address placeholder). No exit interstitials, no
   scroll-jacking, no auto-playing audio.
5. ✅ Mobile parity — hero, disqualifier block and primary CTA are all within
   the first two mobile screens; product grid collapses 3→2→1 columns; tap
   targets are 44px minimum (buttons, form input, footer links sized
   accordingly); no fixed-width elements that would force horizontal scroll
   at 390px. No comparison table on this page, so no stacking rule applies.
6. ✅ Speed posture — self-contained single file, `tokens.css` linked (not
   inlined per-page, but it's a single small shared stylesheet, not a build
   step), Noto Sans loaded with `font-display: swap`, no JS framework, all
   decorative elements (dot patterns, markers) are pure CSS. Page weight: see
   below.
7. ✅ Accessibility floor — one `<h1>`, semantic `<header>/<main>/<section>/
   <footer>` landmarks, all sections labelled via `aria-labelledby`, visible
   `:focus-visible` states (inherited from `tokens.css`), form input has an
   associated `<label>`, screenshot placeholder has descriptive `alt` via
   `role="img" aria-label`, `prefers-reduced-motion` respected globally in
   `tokens.css`. No motion was added on this page at all — nothing here
   needed the "one deliberate moment" budget.

## Page weight

`index.html`: ~13 KB uncompressed. `tokens.css` (shared, cached across every
archetype page once more are built): ~12 KB uncompressed. External requests:
Google Fonts (Noto Sans 300/400/600, `swap`) and Material Symbols icon font
for the two arrow glyphs. No images beyond CSS-gradient placeholders, no JS.

## Conversion instrumentation

- Primary: `data-yooz-event="cta-primary-book-demo"` (hero) and
  `data-yooz-event="form-submit-book-demo"` (form submit) — the demo request.
- Secondary: `data-yooz-event="qualifier-redirect-ar"` on the AR/billing exit
  link — per the brief, this is the page's actual success metric, not a
  vanity click.
- Supporting: `data-yooz-event="cta-tertiary-see-not-for-you"` on the in-page
  jump link, useful for seeing how many visitors self-navigate to the
  disqualifier before it would naturally scroll into view.
- Form is email-only per the brief's low-awareness field-count table — the
  visitors who reach the form have already survived the qualifier, so no
  additional friction was added.

## Open questions / handoffs

- **`{{VOLUME_THRESHOLD}}` is not yet a real number.** The brief flags this
  explicitly — "500+" is illustrative only. This is the single highest-risk
  token on the page: if it's wrong, the page either disqualifies profitable
  buyers or fails to disqualify the AR-seeking traffic it exists to catch.
  Needs sign-off before this leaves mockup stage.
- **`{{URL_AR_BILLING_REDIRECT}}` has no resolved destination.** See
  `PLACEHOLDERS.md` — this needs a product/legal decision on whether it's an
  internal explainer or an external resource.
- **Shared system files did not exist yet in this repo.** `00-FOUNDATION.md`
  specifies that archetype 01 (Brand) is responsible for emitting
  `/mockups/_system/tokens.css` and `/mockups/_system/components.html`, and
  that every later archetype imports them rather than re-deriving tokens.
  Neither file existed in this repository before this build. Since this page
  cannot be built without them, a `tokens.css` covering every token, pattern,
  and component this page uses (colour, type scale, dot patterns, buttons,
  the Grey 10 box, form fields, header/footer) was created now, transcribed
  directly from `00-FOUNDATION.md` §1–2b rather than invented. A minimal
  `components.html` specimen was also added. **When archetype 01 is actually
  built, treat these as a first draft to reconcile against, not a locked
  system** — archetype 01 is the canonical source per the brief, and may add
  components (the Z geometry treatment, additional box scales) this page
  didn't need and therefore didn't build out.
- **Z shape geometry was not built.** This archetype has no hero photography
  slot in the brief (the first screen is deliberately text-only), so no Z
  treatment was needed here. `tokens.css` does not yet include Z geometry
  helpers for the same reason — that should be added when an archetype that
  needs it (e.g. 01, Brand) is built.
