# Notes — `/ad-yooz` (Archetype 01, Brand)

## Design plan (written before code, per Foundation §5)

**Composition:** Primary layout — Pattern BG page ground, Grey 10 content
box, Rich Blue type, Pink CTA. This archetype is the canonical brand
expression, so the shared system (`/mockups/_system/`) was derived here
rather than borrowed from elsewhere.

**Wireframe, first screen (desktop):**
```
┌─────────────────────────────────────────────────────┐
│ Yooz                          The Lean Advantage  Pricing │  ← sticky header
├─────────────────────────────────────────────────────┤
│  ░░░░░░░░░░░░░░░░ Pattern BG ░░░░░░░░░░░░░░░░░░░░░░  │
│  ┌───────────────────────┐                            │
│  │ Trusted by finance...  │        ▁▁▁              │
│  │ Yooz AP Automation      │       ▕ Z ▏  (hero      │
│  │ Software                │        ▔▔▔   placeholder,│
│  │ Purchase-to-pay ...      │              bottom-left)│
│  │ [Book a demo] See pricing│                          │
│  └───────────────────────┘                            │
└─────────────────────────────────────────────────────┘
```
Section order: 1. Hero + CTA → 2. Proof strip → 3. Booking calendar →
4. FAQ, exactly per the brief. No section between hero and the booking
calendar, so the calendar stays one scroll away from the fold on desktop.

**Checked against the brief:**
- "Get out of the way": no problem-agitation, no "what is AP automation"
  section — confirmed, not present.
- Price signal above the fold: the quiet "See pricing" tertiary link sits
  next to the primary CTA, satisfying this without competing with it.
- Booking widget not buried: it's section 3 of 4, directly below a single
  proof strip — one scroll on desktop, reachable in two mobile screens
  (see Quality Score checklist below).

## Quality Score checklist (Foundation §3)

1. **Query echo in H1** — ✅ "Yooz AP Automation Software" contains "Yooz"
   verbatim and "Yooz AP Automation" verbatim (covers "yooz",
   "yooz ap automation" inflectionally, "yooz software"). "getyooz" appears
   in the wordmark link target and footer, not the H1 — flagging as an
   open question below.
2. **Title/meta description contain head keyword, length caps** — ✅
   Title "Yooz AP Automation Software | Book a Demo" (41 chars). Meta
   description (106 chars) contains "Yooz AP automation software."
3. **Ad-to-page continuity** — ✅ comment block at top of `index.html`
   lists the ad headlines/descriptions to fill in; left as `{{TOKEN}}`s
   since no live RSA copy was available to this build.
4. **Transparency/navigability** — ✅ persistent header (wordmark →
   getyooz.com) and footer (Privacy Policy, Terms, Contact, address
   token). No interstitials, no scroll-jacking, no autoplay.
5. **Mobile parity** — ✅ verified in-browser at 390px: H1, subhead,
   price-signal link and the primary CTA all render inside the first
   mobile screen; "Book a demo" (the booking section) is reachable by the
   second screen. See "Departures" below for the layout change this
   required.
6. **Speed posture** — ✅ single self-contained file, no JS, no framework.
   `index.html` is 12.6KB raw (~4KB gzipped); shared `tokens.css` is 16KB
   raw, cached once across every archetype page. Fonts load via Google
   Fonts `<link>` with `font-display: swap` — no `@import`, no
   render-blocking beyond that one request.
7. **Accessibility floor** — ✅ one `<h1>`, semantic `<header>/<main>/
   <footer>`, `:focus-visible` Pink 2px outline/2px offset (global, in
   `tokens.css`), `prefers-reduced-motion` respected (the one motion
   moment — FAQ chevron rotation — is disabled under reduced motion via
   `--transition-fast: 0ms`), all inputs labelled, all placeholder
   imagery uses `role="img"` + `aria-label` plus a visible caption.

## Page weight

`index.html` 12.6KB, shared `tokens.css` 16KB (one-time cost, reused by
every later archetype). No images — all imagery is CSS/gradient
placeholders per the imagery policy, so there is no photography weight to
budget for yet; real graded photography will add real bytes once shot.

## Departures from the brief / brand scale (flagged per Foundation §1, §5)

- **List item weight**: per Foundation's own flagged departure, `.text-list-item`
  defaults to Regular 400, not the brand scale's Light 300, since this
  page has no genuinely dense data block but the token is shared with
  pages that do (comparison tables, etc.) — kept consistent rather than
  special-cased per archetype.
- **Mobile hero image placement**: the brief's reference hero has the Z
  image right-aligned beside the copy. On mobile that column stacks below
  the copy by default — but the brand's Z anchoring math (`bottom-left`,
  extruding beyond frame) assumes a tall portrait frame, and a first pass
  put the full-height Z crop *above* the H1 on mobile (matching the
  desktop DOM order visually via `order: -1`). That pushed the primary
  CTA past the first mobile screen, directly against this archetype's own
  brief ("get out of the way," brevity as the whole strategy). Fixed by
  keeping the hero copy first in visual order at all sizes and shrinking
  the Z image to a short decorative strip (`aspect-ratio: 16/6`) below the
  CTA on mobile, rather than the full portrait crop. Flagging in case
  design wants the full portrait Z preserved on mobile at the cost of
  scroll depth — this build prioritizes the brief's brevity mandate.
- **Z device geometry**: the clip-path polygon in `tokens.css` is a
  reasonable placeholder approximation of a stacked-invoices "Z," not a
  traced brand asset (none was provided). Swap for the real vector once
  design delivers it — every archetype page inherits it from the same
  class, so it's a one-file fix.
- **Dot pattern spacing**: the brand doc's "400%"/"600%" spacing values
  are a design-tool convention (percentage of the dot's own cell), not a
  CSS unit. Translated to `background-size` tiles at a fixed 3px dot
  radius — see the comment above `.pattern-bg` in `tokens.css` for the
  exact ratio, so a port to production can re-derive the same visual
  density at a different dot size if needed.
- **Booking fallback trigger**: Foundation asks for the 5-field form to
  appear "if scheduler fails to load." This mockup has no scheduler
  vendor wired in, so the fallback is a manually-triggered `<details>`
  disclosure ("Calendar not loading? Book by form instead") rather than
  JS that detects a failed iframe load. Production should replace the
  manual toggle with real failure detection (e.g. an `onerror`/timeout on
  the scheduler iframe) while keeping the same 5 fields.
- **Icon-font fallback risk**: Material Symbols renders via font
  ligatures (e.g. `arrow_forward`). If that font fails to load — blocked
  request, ad-blocker, offline preview — the ligature name prints as
  literal text. `.btn` no longer forces `white-space: nowrap` (removed
  during mobile QA) specifically so that failure degrades to wrapped text
  instead of horizontal scroll, but the icon will still visibly read as a
  word rather than an arrow glyph until the font loads. Worth self-hosting
  Material Symbols in production rather than depending on the Google
  Fonts CDN, mirroring the font-hosting note already flagged in this
  repo's earlier `CHECKLIST.md` for Noto Sans.

## Open questions

- Should "getyooz" (the fourth head keyword) appear literally in the H1
  or subhead text, not just as a link target? The current H1 covers the
  other three keywords; adding "getyooz" as visible copy would mean
  either working it into the eyebrow or subhead, or accepting that the
  link target + footer wordmark is sufficient echo for that variant.
- `/ad-yooz-vs` is **not built in this pass**. The brief is explicit that
  it inherits archetype 10's (Displacement) body — the comparison table,
  difference statement, and migration path — and archetype 10 doesn't
  exist yet in this repo. Building it now would mean guessing at a
  comparison structure that's supposed to be defined elsewhere and then
  redoing it. Once archetype 10 ships, `/ad-yooz-vs` should reuse this
  page's hero section verbatim (same composition, single-tone H1 pattern)
  and graft on archetype 10's body.
- Canonical URL uses `https://getyooz.com/en-us/ad-yooz`, matching the
  live path this repo's earlier audit (`README.md` Step 0) found for the
  current production page, on the assumption this mockup replaces it
  in place. Confirm with dev/SEO before treating that as final — if the
  URL structure changes, canonical/OG URLs need to move with it.
