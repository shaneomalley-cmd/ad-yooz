# Notes — `/ad-tipalti-alternative`

Archetype 10, Displacement. Campaign build priority 8. First of five
competitor pages (`tipalti`, then `avidxchange`, `stampli`, `ramp`,
`bill-com`) — built first per the brief.

## Design plan (written before code, per Foundation §5)

**Brand composition:** Primary layout (Pattern BG page background, Grey 10
content boxes, Rich Blue type, Pink CTAs) with the Rich Blue → Grey 10
comparison table treatment specified in `10-displacement.md`'s own brand
composition note.

**Section order** (fixed by the brief): named comparison hero → honest
feature table → migration path & timeline → customer who switched → form.

**ASCII wireframe, first screen at ~1440px:**

```
┌─────────────────────────────────────────────────────────────────┐
│ [yooz]                                    tel   [Book a demo]   │ ← sticky header
├─────────────────────────────────────────────────────────────────┤
│  (pattern-bg)                                                    │
│  For AP teams evaluating a move off Tipalti        ┌───────────┐│
│  A Tipalti alternative                              │           ││
│  built to migrate without the reset.                │  Z figure ││
│                                                       │ (hero    ││
│  ⇄ Tipalti = global mass payouts.                    │  cutout  ││
│    Yooz = full purchase-to-pay, one system.          │  placehldr)│
│                                                       └───────────┘│
│  Switching platforms is usually why teams stay...    ┌──────────┐│
│                                                       │ Migration ││
│  [Book a demo]   [Get the migration checklist →]     │ window:   ││
│  ⏱ See your timeline before you commit               │ N weeks   ││
└─────────────────────────────────────────────────────────────────┘
```

Everything above is reachable in the first two mobile screens too: eyebrow
→ H1 → one-line difference → CTAs stack full-width before the visual, which
drops below the copy at ≤1024px.

## First screen — checked against the brief

- ✅ **Names the competitor in the headline** — "Tipalti" appears verbatim in
  the H1, which also satisfies the QS query-echo requirement for "tipalti
  alternative[s]."
- ✅ **States the difference in one line** — the boxed `.hero-diff` line:
  "Tipalti is built around global mass payouts. Yooz is built around the
  full purchase-to-pay cycle." One sentence, no migration talk yet.
- ✅ **Then de-risks the migration** — the paragraph immediately after,
  before either CTA, plus the migration-window stat card in the hero visual.
  Order matches the brief exactly: name → difference → de-risk.

## Do-not checklist

- ✅ **Not a blog post** — ships at the top-level `/ad-tipalti-alternative`
  slug, no `/blog/` prefix, no article byline/date treatment.
- ✅ **Table does not let Yooz win every row** — row 3 (global mass payouts /
  multi-currency supplier pay) is explicitly tagged "Tipalti wins here" with
  a `.concede` styling treatment (pink border top/bottom, tag badge) so it
  reads as a genuine concession, not a hedge. The row also carries an
  explicit "may be the better fit" note rather than burying the concession
  in a neutral tone.
- ✅ **Not a shared template with the name swapped in** — this page's
  concession row (global payouts), migration-phase framing, and hero
  differentiator line are all Tipalti-specific. When `avidxchange`,
  `stampli`, `ramp`, and `bill-com` are built, each needs its **own**
  genuine-weakness row and migration shape — none of that content should be
  copy-pasted with only the competitor name changed. Flagging this now so
  whoever builds page 2 doesn't shortcut it.

## Legal and policy gate (flagged per brief)

This page names a live competitor in comparative content, which the brief
correctly identifies as something a mockup cannot fully clear on its own:

1. **Every factual claim about Tipalti is tokenized, not asserted.** All
   seven Tipalti-side table cells carry a `{{COMPETITOR_FEATURE_TIPALTI_*}}`
   token plus a numbered footnote (`[1]`–`[13]`, odd numbers) pointing to a
   `{{SOURCE_TIPALTI_*}}` citation slot. None of this ships until
   Competitive Intel supplies dated, sourced values — see
   `PLACEHOLDERS.md`.
2. **The table has an owner and a review cadence, on-page.** The
   `.verified-line` under the table (`Last verified: {{DATE}} · owner:
   {{TABLE_OWNER}} · review cadence: {{TABLE_REVIEW_CADENCE}}`) is built as
   a structural row, not a caption or afterthought, per the brief's explicit
   instruction. It needs real values before launch and then needs someone
   to actually own re-checking it.
3. **Ad-copy trademark compliance is a separate, ads-side check.** Using
   "Tipalti" in landing-page body copy (this file) is governed differently
   from using it in Google Ads RSA headlines/descriptions. This page does
   not attempt to clear the ads-side policy — that's the paid-media team's
   check — but the two need to land on the same claims once both are final,
   which is also why the ad-headline comment block at the top of
   `index.html` exists: so copy staying consistent is checkable in one
   place.
4. **Do not ship any Tipalti cell with a plausible-sounding guess.** Every
   Tipalti-side cell is a token. This was the one rule in the brief with no
   exception, and it's held here even where a real number was fairly
   guessable (e.g. implementation timelines) — guessable is not the same as
   sourced.

## QS checklist confirmation (Foundation §3)

1. **Query echo in H1** — "Tipalti alternative" appears verbatim (brief's
   plural "tipalti alternatives" is an inflectional match). ✅
2. **`<title>` / meta description contain the head keyword** — title is
   "Tipalti Alternative for AP Automation | Yooz" (44 chars, ≤60). Meta
   description is 122 chars (≤155) and contains "Tipalti." ✅
3. **Ad-to-page continuity** — comment block at the top of `index.html`
   lists the ad groups this page must stay consistent with and states this
   page's current above-fold promise, for the copy team to reconcile against
   the live RSAs. ✅ (content itself still needs the copy team's fill-in)
4. **Transparency and navigability** — sticky header with Yooz wordmark
   linking to `getyooz.com`; footer with Privacy Policy, Terms, Contact,
   Pricing, and a `{{BUSINESS_ADDRESS}}` placeholder. No exit interstitials,
   no scroll-jacking, no autoplay audio. ✅
5. **Mobile parity** — hero content reflows to a single column at ≤1024px
   with the visual dropping below the copy; comparison table becomes
   per-row stacked cards with a sticky attribute label at ≤768px (the
   desktop scrollable table is hidden via `display:none` below that
   breakpoint, and vice versa, so only one version ships to the DOM's
   visible rendering per viewport — both exist in markup for
   crawlability/no-JS resilience). Tap targets: buttons min-height 44px,
   form inputs min-height 44px. No horizontal scroll at 390px — verified by
   design (single-column grids below 1024px, `.wrap` padding drops to
   `--space-4` at ≤390px). ✅
6. **Speed posture** — single self-contained HTML file (~44KB before
   fonts/icons), tokens inlined so it opens standalone. External requests:
   Google Fonts (Noto Sans 300/400/600, `display=swap`) and Material
   Symbols Rounded. No JS framework, no build step; all geometry (Z figure,
   button/table styling) is inline SVG or CSS. `scroll-behavior: smooth` is
   gated behind `prefers-reduced-motion`. ✅ — flagging that a production
   port should self-host Noto Sans with `fetchpriority="high"` preloads
   (this org's own prior template work on `/ad-yooz` already established
   that pattern; reuse it here rather than the Google Fonts CDN link this
   preview uses only because it's the one stylesheet host this sandboxed
   environment's CSP allows).
7. **Accessibility floor** — semantic `<header>/<main>/<section>/<footer>`,
   one `<h1>`, visible Pink 2px focus outline with 2px offset via
   `:focus-visible`, `prefers-reduced-motion` respected, every form input
   labelled, skip-link to `#main`, hero image and Z figure have descriptive
   `alt`/`aria-labelledby` captions naming what the real asset should show.
   ✅

## Conversion instrumentation

Primary: `form-book-demo-primary` (6 fields — first name, last name, work
email, company, monthly invoice volume, phone optional — matches the
"late/high intent" 5–6 field band Foundation assigns this archetype).
Secondary: `form-migration-checklist-secondary` (email-only, deliberately
lower-friction, placed in its own section rather than folded into the demo
form so it doesn't inflate the primary form's field count).
`cta-book-demo-header`, `cta-book-demo-hero-primary`,
`cta-migration-checklist-hero-secondary`, and `link-methodology-tertiary`
are all tagged for tracking; the tertiary link exists specifically to
exercise the brand's third button level on this page (secondary and primary
were already load-bearing in the hero).

## Deliberate departures from the brief/brand scale, flagged

- **Fluid type beyond Display/H1.** Foundation only calls out Display (120px)
  and H1 (84px) as needing a `clamp()` fluid scale for mobile. This build
  also fluids H2 (64px) and H3 (48px) between the same 390px/1440px anchors,
  because 64px and 48px Light-weight headings also overflow or crowd a
  390px viewport in this page's actual section heads. H4/H5 stay fixed per
  spec since they're used at sizes that already fit.
- **Dense data steps up to Regular 400.** Comparison-table body text uses
  `.t-list-dense` (Regular 400, 16px) rather than the brand's default Light
  300 list-item style, per Foundation's own explicit carve-out for
  comparison tables — not a new departure, just confirming it was applied.
- **`noindex, follow` on this page.** Not in the brief, added as a judgment
  call: this is a paid-only landing URL naming a live competitor, and
  Foundation's own "do not publish as a blog post" instruction is about
  competing for organic SEO rank with a dedicated page structure — it isn't
  a statement that this URL should rank organically at all. Flagging for
  marketing to confirm; flip to `index` if the intent is for this URL to
  also compete organically against `payhawk.com/tipalti-alternative` and
  similar.

## Page weight

`index.html` alone: ~44KB (includes inline CSS, inline SVG, all markup for
both desktop table and mobile card variants of the comparison table).
External requests: 2 Google Fonts stylesheets (Noto Sans, Material Symbols
Rounded) plus their font-file fetches. No images, no JS, no build step.

## Open questions for the copy/legal/product owners

1. Is "global mass payouts & multi-currency supplier pay" the right
   concession row, or does Competitive Intel have a different genuine
   Tipalti strength they'd rather concede instead? The row was chosen
   because it's Tipalti's well-known market position, but the specific
   framing in `{{COMPETITOR_FEATURE_TIPALTI_GLOBAL_PAYOUTS}}` needs their
   sign-off regardless.
2. Does Yooz have *any* named customer who switched from Tipalti
   specifically? If marketing knows of one but hasn't cleared them for
   public naming yet, that's worth flagging back — the empty state this
   page ships with is honest but a real logo/quote there would materially
   help conversion for exactly this high-intent audience.
3. Should the migration checklist secondary-CTA be a gated PDF (email-only,
   as built) or ungated? Built as gated since it doubles as a lead-capture
   moment for visitors not ready for a full demo — worth confirming that's
   the intended value of the secondary path versus a pure trust-builder.
