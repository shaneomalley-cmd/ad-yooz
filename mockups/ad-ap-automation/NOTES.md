# Build notes — `/ad-ap-automation` (Archetype 02 — Solution)

## Rebuild note (structural only — copy unchanged)

This page was originally built before archetype 01 existed, against a
draft `tokens.css` authored ad hoc for this page (see the superseded
"Shared system — provenance flag" section below). Archetype 01 has since
shipped the real `/mockups/_system/tokens.css` and `components.html`, and
this page's markup/CSS did not match it — it referenced classes
(`.wrap`, `.box`, `.t-h1`, `.tone-blue`/`.tone-pink`, `.section-kicker`,
`material-symbols-outlined`) and custom properties (`--fs-h3`, `--wt-*`,
`--lh-*`) that don't exist in the real system, and loaded Material Symbols
**Outlined** instead of the brand-specified **Rounded** set.

This pass rebuilds the markup and CSS to use `ad-yooz/index.html` (the
reference implementation) as the pattern to follow: `.container` instead
of `.wrap`, `.box-grey10`/`.box-grey10--sm|md|lg` instead of `.box`,
`.text-h1`–`.text-h5`/`.text-para`/`.text-para-lg` instead of `.t-*`, an
`<em>` inside the heading instead of `.tone-pink` spans, the canonical
`.section-eyebrow`/`.section-eyebrow__number`/`.section-eyebrow__label`
instead of the unstyled `.section-kicker`/`.num`/`.label`, `.icon` +
Material Symbols Rounded instead of `material-symbols-outlined`, and the
shared `.site-header`/`.site-footer` chrome instead of page-local
`.wordmark`/`.site-nav` classes. Two content bugs were fixed as part of
this pass (not a copy rewrite): "Yooz runs the **brand's** full AP cycle"
→ "Yooz runs the full AP cycle" in the "How it works" intro, and the
section eyebrows — previously two unstyled adjacent spans that rendered
concatenated as e.g. "02How it works" — are now the two-element
`.section-eyebrow` pattern with `var(--space-3)` between them. All other
headlines, section copy, capability descriptions and form fields are
unchanged from the previous build.

Layout rules that aren't part of the shared system (the hero grid, the
3-step/capability/proof grids, the demo form grid) remain page-specific
`<style>` rules, per Foundation §6 — same pattern `ad-yooz/index.html`
uses for its own hero/proof/booking sections — but now built on
`var(--space-N)` spacing tokens throughout instead of ad hoc rem values.

Verified in-browser (Chromium via Playwright, proxied) at 1440px and
390px: no horizontal overflow, header nav collapses to the CTA only under
768px per `tokens.css`, and the untranslated `{{DIFFERENTIATOR}}`/quote
tokens — which have no natural break point — no longer push the layout
wide now that `main { overflow-wrap: anywhere; }` is set locally (real
copy won't need this once the tokens are resolved). One rendering
artifact is environment-only: this sandbox's headless Chromium does not
apply the Material Symbols ligature substitution even though the font
file itself fetches successfully (verified with an isolated test page),
so icons render as their literal name text instead of glyphs — the same
gap the original build's NOTES flagged for Google Fonts generally.
Expected to resolve in a normal browser with standard internet access.

## Design plan (written before code, per `00-FOUNDATION.md` §5)

**Layout concept.** Primary brand composition: Pattern BG page ground, Grey 10
bounding boxes carrying content, Rich Blue type, Pink CTAs. The visitor here
is solution-aware and comparison-shopping with several vendor tabs open, so
the entire job of the first screen is to state the product category (query
echo) and exactly one differentiator, fast, then get out of the way.

**ASCII wireframe, first screen (1440px):**

```
┌────────────────────────────────────────────────────────────────┐
│ [Z + Yooz]        Product  Lean Advantage  Pricing  Resources   [Book a demo] │
├────────────────────────────────────────────────────────────────┤
│ pattern-bg                                                       │
│  ┌──────────────────────────────┐   ┌─────────────────────┐     │
│  │ Grey10 box                     │   │  Z-frame hero        │     │
│  │ eyebrow (pink, sentence case)  │   │  placeholder,         │     │
│  │ H1: "AP automation software"   │   │  bottom-left Z,       │     │
│  │     (blue) + differentiator    │   │  facing inward        │     │
│  │     clause (pink)              │   │  toward the copy      │     │
│  │ H4 subhead                     │   │                       │     │
│  │ paragraph                      │   │                       │     │
│  │ [Book a demo] [Comparison →]   │   │                       │     │
│  └──────────────────────────────┘   └─────────────────────┘     │
└────────────────────────────────────────────────────────────────┘
```

**Section order** (matches the brief exactly): 1 Hero + differentiator,
2 How it works in 3 steps, 3 Capability grid, 4 ERP connector logos,
5 Customer proof, 6 Demo form.

**Checked against the archetype brief:**
- "State the product and one differentiator... above the fold" → H1 is a
  two-tone query echo + single differentiator clause, inside the first
  Grey 10 box, no scrolling required.
- "Do not open with a definition" → hero opens on the H1 declarative
  statement + a supporting subhead about how AP moves, not "AP automation
  is the process of...".
- "Differentiator is a strategy decision, not a design one" → left as
  `{{PRIMARY_DIFFERENTIATOR_HEADLINE}}` with three sourced candidates in an
  HTML comment, not decided in the mockup. See `PLACEHOLDERS.md`.
- Numbered markers used only in the 3-step section (a genuine sequence);
  the capability grid deliberately has no numbers, per the guardrail in
  `00-FOUNDATION.md` §5.

## Shared system — provenance flag

`00-FOUNDATION.md` states that `/mockups/_system/tokens.css` and
`components.html` are emitted by archetype 01 (Brand), and every later
archetype imports them. **Archetype 01 has not been built in this repo yet**
— `/mockups` did not exist before this build. To avoid blocking archetype 02
on an unbuilt dependency, this session authored `tokens.css` directly from
§1 of `00-FOUNDATION.md` (colour, type scale, layout patterns, dot patterns,
button system, Grey 10 box, header/footer, forms).

**Not built:** `/mockups/_system/components.html`, the live specimen sheet.
That is archetype 01's deliverable and out of scope for a Solution-page
build. **Open question / action item:** when archetype 01 is actually run,
reconcile its `tokens.css` output against this one — this file should be
treated as a draft of the shared system, not the final word, and archetype
01 should supersede it (or confirm it matches) rather than the two forking.

## QS checklist confirmation (`00-FOUNDATION.md` §3)

1. **Query echo in H1** — "AP automation software" appears verbatim as the
   Rich Blue clause of the H1. ✅
2. **`<title>` / meta description contain the head keyword** — title is
   "AP Automation Software | Yooz" (30 chars, well under 60); description
   opens "AP automation software that..." (≤155 chars, differentiator
   clause is tokenized). ✅ — re-verify exact char counts once the
   differentiator token is resolved to real copy.
3. **Ad-to-page continuity** — comment block at top of `index.html` lists
   the ad headline/description slots copy must stay consistent with. ⚠
   placeholders only; needs the live RSA copy from the Campaign 02 ad
   groups to actually verify against.
4. **Transparency/navigability** — persistent header with Yooz wordmark
   linking to `getyooz.com`; footer with Privacy Policy, Terms, Contact and
   an address placeholder. No interstitials, no scroll-jacking, no audio. ✅
5. **Mobile parity** — hero grid stacks to a single column under 960px with
   the image placeholder reordered above the copy (`order: -1`) so it
   doesn't push the H1 below the first two screens; steps/capability
   grids collapse to 1–2 columns; ERP logo grid collapses to 2 columns;
   demo form fields stack to one column under 540px. Tap targets on
   buttons and form fields are ≥44px via `min-height`. No fixed-width
   elements that would force horizontal scroll at 390px. ✅
6. **Speed posture** — single HTML file + one shared CSS file, Noto Sans
   loaded via Google Fonts with `display=swap`, Material Symbols for icons,
   no JS, no framework, all geometry (Z frame, dot patterns) is CSS-only
   (`clip-path` / `radial-gradient`), no raster images. Page weight:
   `index.html` ≈ 21KB, shared `tokens.css` ≈ 12KB (cached across every
   archetype once 01–13 all import it). ✅
7. **Accessibility floor** — one `<h1>`; semantic `<header>/<main>/<footer>`
   landmarks; skip link; visible focus via `:focus-visible` (Pink 2px
   outline, 2px offset) inherited from `tokens.css`; `prefers-reduced-motion`
   zeroes transition durations in `tokens.css`; all form inputs have
   associated `<label>`s; the hero and ERP-logo placeholders carry
   descriptive `role="img"`/text content rather than a bare `<img alt="">`
   since no raster asset exists yet. ✅

## Conversion / instrumentation

- Primary: `demo_form_submit_button` (the form itself), plus two earlier
  entry points to the same form/anchor: `header_cta_book_demo`,
  `hero_cta_book_demo`.
- Secondary: `hero_cta_comparison_guide` and `footer_comparison_guide`,
  both linking to `/ad-ap-comparison` — lower-commitment path per the brief.
- Every nav, footer and CTA element carries a `data-yooz-event` attribute
  per `00-FOUNDATION.md` §4 so tracking can be wired without re-editing
  markup.

## Departures from a literal reading of the brief

- The brief's "5–6 fields, including invoice volume and ERP" is built as
  6 required fields (first name, last name, work email, company, invoice
  volume, ERP) plus phone as a clearly-marked optional 7th — phone is
  explicitly allowed as optional in `00-FOUNDATION.md`'s form-length table
  and is not counted against the 5–6 required-field budget.
- Body-copy weight: list items in the demo-form pitch panel use Regular 400
  rather than the brand's specified Light 300 for 16px list items, per the
  foundation's own flagged departure (§Typography) — Light below 24px is a
  legibility risk, and this list sits on a Rich Blue background rather than
  Grey 10/20, which the departure note calls out as the exact case to avoid.

## Verified in-browser (Chromium, 1440px and 390px)

Rendered the file directly and screenshotted both breakpoints. Fixed one
real defect found this way: the `{{PRIMARY_DIFFERENTIATOR_HEADLINE}}` token
has no natural break point and was overflowing its Grey 10 box before
`overflow-wrap: anywhere` was added to the heading/paragraph utility
classes in `tokens.css` (now wraps correctly at both breakpoints — this
fix applies to every archetype that imports `tokens.css`, not just this
page). One rendering artifact is environment-only, not a code defect: this
sandbox has no outbound access to Google Fonts, so Noto Sans falls back to
a system sans-serif and the Material Symbols icons render as their literal
ligature text (e.g. "document_scanner") instead of glyphs in the local
screenshot — expected to resolve wherever the page has real internet
access to `fonts.googleapis.com`.

## Open questions

1. Which differentiator wins — deep-document-understanding AI, 250+ ERP
   exports, or multi-channel capture breadth? This gates the H1, meta
   description, and one capability-grid card's framing.
2. Real customer names/quotes at "similar scale" — marketing to confirm
   which reference customers are cleared for paid-media use.
3. ERP logo usage rights — several of the six (SAP, Sage, Microsoft
   Dynamics) are trademarked and may require partner-program logo
   agreements, not just placement.
