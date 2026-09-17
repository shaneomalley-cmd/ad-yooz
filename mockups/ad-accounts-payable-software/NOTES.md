# Build notes — `/ad-accounts-payable-software`

Archetype 03, Category-establishing. Campaign 03 CATEGORY – Function-Named, all four
ad groups.

## Design plan (written before code, per Foundation §5)

**Layout concept.** The visitor hasn't accepted that they need new software — they
think their ERP might already cover this. So the page has to win an argument before
it makes an offer. Section order follows the brief exactly: problem-framed hero → an
honest four-option comparison (the centerpiece) → the case for a dedicated layer →
product → proof → form. No hero-and-demo-form; the primary CTA doesn't appear until
the visitor has been walked through the reasoning.

**Brand composition.** Primary layout (Pattern BG ground, Grey 10 content box, Rich
Blue type, Pink CTA) for the hero. Inframe layout — four Grey 10 boxes of identical
size/padding/border sitting directly on the Pattern BG ground — for the four-option
block; no box is enlarged, colored differently, or ordered to imply Yooz's option is
already the answer. Pattern Pink as a single-strip callout for the cost-per-invoice
contrast in Proof, per the brief's suggestion.

**ASCII wireframe — first screen (desktop):**

```
┌────────────────────────────────────────────────────────────┐
│ Yooz [wordmark]                                    Pricing │  ← header
├────────────────────────────────────────────────────────────┤
│ (Pattern BG — sparse pink dots on grey ground)              │
│  ┌──────────────────────────────────┐  ┌─────────────────┐ │
│  │ Before you buy another…          │  │                 │ │
│  │ H1: Your ERP already sells you   │  │  [Z-shape photo │ │
│  │ accounts payable software.       │  │   placeholder,  │ │
│  │ Here's what it doesn't do.       │  │   bottom-left   │ │
│  │ H4: Every ERP ships an AP module.│  │   anchor]       │ │
│  │ Most finance teams still process │  │                 │ │
│  │ invoices by hand.                │  │                 │ │
│  │ [body copy]                      │  └─────────────────┘ │
│  │ → See the four options           │                      │
│  └──────────────────────────────────┘                      │
└────────────────────────────────────────────────────────────┘
```

No pricing claim, no product name, no demo form above the fold — the H1 and subhead
restate the problem, and the only action is a tertiary link scrolling to the
four-option section, not a commitment ask.

**Section order** (matches the brief): 1 Hero-as-problem · 2 Four options · 3 Why a
dedicated layer wins · 4 Product (six-stage strip) · 5 Proof (cost callout +
comparison table + customer quote) · 6 Form.

Checked against the brief's "First screen must do" and "Do not" lines before writing
code: the first screen answers "why not just use what I have" via the H1/subhead
framing and hands off to the four-option section rather than pitching a product; it
never assumes automation has been accepted; it doesn't mention Stampli or Tipalti
anywhere on the page.

## Query-echo / keyword strategy

The brief lists six head keyword variants across four ad groups sharing this one
page. The H1 carries **"accounts payable software"** verbatim — the broadest, most
central of the six — since no single H1 can literally contain all six phrasings.
The other variants are echoed across the page rather than only in the H1: "AP
module" / "AP automation" language recurs through the four-option and product
copy, "accounts payable system" appears in the eyebrow-pill labels' surrounding
copy, and the `<title>`/description both restate the primary term. This is a
deliberate reading of "Head keywords for the H1 echo" as a set to draw from, the
same approach the general/brand page in `content/ad-yooz.json` took for its two
head terms. Flagging as an open question below — if each ad group needs its own
literal H1 match, this page would need four H1 variants swapped by ad-group
UTM/query-param rather than one shared H1.

## QS checklist (Foundation §3)

1. **Query echo in H1** — "accounts payable software" appears verbatim. ✅ (see
   keyword-strategy note above for the multi-ad-group caveat)
2. **Title/meta** — title 55 chars, contains "Accounts Payable Software"; meta
   description 143 chars, contains "accounts payable software". Both under the
   60/155 caps. ✅
3. **Ad-to-page continuity** — comment block at top of `<head>` lists placeholder
   slots for the copy team to paste actual RSA headlines/descriptions. ✅ (content
   pending from paid media)
4. **Transparency/navigability** — persistent header with Yooz wordmark linking to
   getyooz.com; footer with Privacy Policy, Terms, Contact, and an address token. No
   interstitials, no scroll-jacking, no audio. ✅
5. **Mobile parity** — hero collapses to one column under 960px; option grid goes
   4→2→1 columns at 1100px/600px; comparison table becomes a horizontally-scrollable
   region with a sticky first column and a visible "← Swipe to compare →" hint under
   768px (not a squashed 6-column grid); all interactive elements ≥44×44px (buttons
   min-height 52px, form fields 50px). ✅
6. **Speed posture** — single self-contained file, ~36KB as written (see below), no
   JS at all (this archetype needed none — the calculator is a separate page,
   `/ad-ap-roi`), fonts loaded with `display=swap`, all geometry is CSS
   gradients/inline markup, no raster images. ✅
7. **Accessibility floor** — one `<h1>`; semantic `header`/`nav`/`main`/`section`/
   `footer`; skip link; `:focus-visible` with 2px Pink outline / 2px offset;
   `prefers-reduced-motion` respected (page has no decorative motion to begin with —
   see Design guardrails note below); all form inputs labelled; both media
   placeholders carry a descriptive `figcaption` (used instead of `alt`, since these
   are CSS/SVG placeholders, not `<img>` elements — the caption *is* the accessible
   description). ✅

## Page weight

`index.html` is **~37KB** (681 lines) as a single file: inline `<style>`, no external
JS, two Google Fonts requests (Noto Sans + Material Symbols Rounded, preconnected,
`display=swap`). No raster images — both media slots are CSS gradients / bordered
placeholder frames.

## Verified in a real browser (Playwright/Chromium)

Rendered and measured at all four required breakpoints (1440, 1024, 768, 390) —
`document.documentElement.scrollWidth` equals viewport width at every one, i.e. no
horizontal scroll anywhere on the page. Two real bugs were caught and fixed this way
before considering the build done:

- Unbroken `{{TOKEN}}` strings displayed at hero/display type sizes were forcing
  page-level horizontal overflow (they can't wrap at a space). Fixed by giving every
  placeholder token a dedicated `.token` treatment — small monospace, dashed pink
  border, `overflow-wrap:anywhere` — so unfilled data reads as an obvious "needs
  sourcing" chip instead of stretching into a giant, mid-word-broken number.
- Grid/flex items containing long unbroken text (the same token strings) were
  overriding their `1fr` track width because grid/flex items default to
  `min-width:auto`. Fixed with `min-width:0` on `.box`.
- The comparison table's horizontal-scroll-with-sticky-column behavior was verified
  directly (`table-wrap` scrollWidth 640 vs. clientWidth 348 at 390px, `swipe-hint`
  computed `display:block` below 768px) rather than assumed from the CSS.

**Known sandbox limitation, not a page defect:** this environment has no outbound
network access to Google Fonts, so Material Symbols Rounded icons render as their
literal names ("check", "arrow_forward", etc.) in the screenshots taken here. The
markup and font request are correct per Foundation §1 ("Icons: Material Symbols");
this will render as icons on any connection with real internet access. Re-verify
visually once this can be opened outside the sandbox.

## Brand-scale departures (flagged per Foundation §1)

- **Fluid type scale extended beyond H1.** The brand doc calls out Display (120px)
  and H1 (84px) by name as needing `clamp()` for mobile. H2 (64px) and H3 (48px)
  have the same overflow problem at a 390px viewport, so the same fluid-scale
  treatment was applied through H4, holding each level's stated -2% tracking and
  line-height. Noted as a departure, not a silent change.
- **Regular 400 instead of Light 300 in dense blocks.** Per the brief's own
  departure #1, the four-option "Good fit / Watch for" lines, the stage-strip body
  copy, and the comparison table are all set in Regular 400 rather than the
  brand-scale's Light 300 for 16–17px text — this page is almost entirely a dense
  comparison argument, so nearly every list-style block qualifies.
- **H4 used as a type style, not a heading level.** The hero's supporting subhead
  ("Every ERP ships an AP module…") uses the H4 *font-size/weight* class per the
  brand's hero composition pattern, but is marked up as a `<p>`, not an `<h4>` tag —
  going straight from `<h1>` to a real `<h4>` would skip two heading levels and
  break the accessibility tree for no benefit. Section headings use `<h2>`
  correctly; the type styling and the semantic heading level are treated as
  separate concerns throughout.

## Design guardrail notes

- **No numbered markers on the four options** — a choice set, not a sequence,
  per Foundation §5. Distinguished by icon only.
- **Numbered markers used for**: the page's own section eyebrows (02–06, a genuine
  narrative sequence: options → resolution → product → proof → form) and the
  six-stage Purchase→Export strip (a genuine process sequence). The hero's eyebrow
  is unnumbered, matching the brand's plain hero-eyebrow pattern.
- **Motion**: none added. The guardrail caps motion at one deliberate moment per
  page; this page didn't need one, so nothing was added rather than manufacturing a
  moment for its own sake.
- **Four-option boxes are deliberately identical** in size, border, padding, and
  structure (icon → heading → description → good-fit/watch-for pair) — including for
  the AP-automation-layer option, which gets the same "watch for" caveat as the
  other three, per the brief's explicit centerpiece instruction.

## Open questions

1. **Per-ad-group H1 variants.** See "Query-echo / keyword strategy" above — confirm
   with paid media whether one shared H1 covering the most central term is
   acceptable QS-wise across all four ad groups, or whether this page needs to
   branch its H1 by ad group (would require a templating layer this static mockup
   doesn't have).
2. **Comparison table scope.** The brief says the table should "include the native
   module" — built here as a two-column Native-vs-Yooz table rather than all four
   options, since the native module is the specific competing alternative named in
   "The competing alternative in their head." Confirm this reading is right rather
   than wanting all four options repeated in table form.
3. **`/ad-ap-roi` existence.** The secondary CTA links to `/ad-ap-roi` per the brief;
   that page is out of scope for this build and its own archetype prompt wasn't
   provided in this pass — confirm it exists or is being built in parallel so this
   link isn't dangling.
4. **Shared system dependency.** This page was built before archetype 01 (Brand),
   which is supposed to emit `/mockups/_system/tokens.css` and
   `components.html`. All tokens here are defined locally in `:root` so the page is
   fully self-contained today; once archetype 01 lands, this file should be
   refactored to import `tokens.css` and reuse its components rather than carrying
   its own copy, per Foundation §6 ("what is shared and what is not").
