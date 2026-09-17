# Notes — `/ad-ap-automation-healthcare` (Archetype 09, Fit: Industry)

Campaign 08 FIT – Industry, ad group Healthcare. Build priority 9. Built
first per the brief ("new vertical — build first"). This page's structure
is shared verbatim with `/ad-ap-automation-manufacturing`; only the
vertical vocabulary differs. `/ad-ap-automation-construction` diverges
structurally — see its own NOTES.md.

## Design plan (written before code, per Foundation §5)

**Layout concept.** This is a small-volume, coverage-tier campaign (~160
searches/month across all three industry pages, $400 budget) with one
job: prove in the first screen that Yooz knows how healthcare AP actually
runs, not that Yooz is a good AP tool in general. The brief's single
question is "do you understand how my industry actually works?" — so the
H1 itself carries the vertical vocabulary (GPO invoices, contract
pricing) rather than saving it for a subhead, and a dedicated workflow
section (distinct from the generic Product section) exists purely to
show the document types and approval-chain language in more than one
line.

**Brand composition.** Primary layout (Pattern BG ground, Grey 10 content
box, Rich Blue type, Pink CTA) for the hero, matching the archetype 01/02
reference builds. Pattern Pink single-strip callout for the proof
section. No Inframe layout needed here — that's reserved for
`/ad-ap-automation-construction`'s four-option comparison.

**ASCII wireframe — first screen (desktop):**

```
┌──────────────────────────────────────────────────────────┐
│ Yooz [wordmark]                 The Lean Advantage  Pricing│  ← header
├──────────────────────────────────────────────────────────┤
│ (Pattern BG)                                                │
│  ┌────────────────────────────────┐                        │
│  │ Built for healthcare AP teams   │        ▁▁▁            │
│  │ H1: AP automation for           │       ▕ Z ▏  (hero    │
│  │ healthcare                      │        ▔▔▔   placeholder│
│  │ H4: Built around GPO invoices   │              bottom-left)│
│  │ and contract pricing — routed   │                        │
│  │ through your existing chain     │                        │
│  │ [Book a demo]  See the workflow ↓│                       │
│  └────────────────────────────────┘                        │
└──────────────────────────────────────────────────────────┘
```

**Section order** (matches the brief exactly): 1 Industry-named hero →
2 Their specific workflow → 3 Industry proof → 4 Product → 5 Form.

Checked against the brief's "First screen must do" and "Do not" lines
before writing code: the H1 names the actual document types (GPO
invoices, contract pricing) rather than a stock photo or a generic "AP
automation" headline with the word "healthcare" swapped in; the workflow
section is a distinct block from Product, so the vertical vocabulary
doesn't get diluted into the generic six-stage grid every fit page shares.

## Query-echo / keyword strategy

Head keywords: "ap automation for healthcare," "healthcare accounts
payable automation," "accounts payable software for healthcare." The H1
— "AP automation for healthcare built around GPO invoices and contract
pricing" — carries "ap automation for healthcare" verbatim. The other two
variants ("healthcare accounts payable automation," "accounts payable
software for healthcare") are the same three concepts in different word
order; Google's exact/phrase-match head-term matching for QS purposes
treats inflectional and reordered variants generously, and title/meta
description reinforce "accounts payable software for healthcare"-style
phrasing directly (see below). Flagging as an open question below in case
the account structure actually splits these into separate ad groups with
their own landing pages rather than sharing this one.

## Quality Score checklist (Foundation §3)

1. **Query echo in H1** — ✅ "AP automation for healthcare" verbatim.
2. **Title/meta description contain head keyword, length caps** — ✅
   Title "AP Automation for Healthcare | Yooz" (36 chars). Meta
   description (118 chars) contains "AP automation for healthcare."
3. **Ad-to-page continuity** — ✅ comment block at top of `index.html`
   lists campaign/ad-group and the head keywords the H1 must echo, with
   `{{AD_HEADLINE}}`/`{{AD_DESCRIPTION}}` slots for the copy team.
4. **Transparency/navigability** — ✅ persistent header (wordmark →
   getyooz.com) and footer (Privacy Policy, Terms, Contact, address
   token). No interstitials, no scroll-jacking, no autoplay.
5. **Mobile parity** — ✅ verified at 390px: H1, subhead, and both CTAs
   render inside the first mobile screen; the workflow section (with the
   named document types) is reachable by the second screen scroll, same
   pattern as the archetype 01 reference build's hero/booking split.
6. **Speed posture** — ✅ single self-contained file, no JS, no
   framework. `index.html` is ~17KB raw; shared `tokens.css` (16KB) is
   cached once across every archetype page. Fonts load via Google Fonts
   `<link>` with `font-display: swap`.
7. **Accessibility floor** — ✅ one `<h1>`, semantic `<header>/<main>/
   <footer>`, `:focus-visible` Pink 2px outline/2px offset (inherited
   globally from `tokens.css`), `prefers-reduced-motion` respected (no
   page-specific motion added beyond the global button hover
   transitions, which are governed by the same reduced-motion media
   query in `tokens.css`), all form inputs labelled, all placeholder
   imagery uses `role="img"` + `aria-label` plus a visible caption.

## Page weight

`index.html` ~17KB raw. Shared `tokens.css` (16KB) and
`components.html` are a one-time cost already paid by whichever
archetype ships first; not re-derived here. No real photography — all
imagery is CSS/gradient placeholders per the imagery policy.

## In-browser QA findings (Playwright/Chromium, all four breakpoints)

This page was actually rendered and checked in a headless Chromium at
1440/1024/768/390px, not just visually inspected as a static file. Three
real layout bugs surfaced and were fixed; noting them because they'd
otherwise recur silently on any future archetype page copying this
structure:

1. **Grid tracks collapsing to `1fr` at a mobile breakpoint** (e.g.
   `.workflow__grid { grid-template-columns: 1fr; }`) inherit an implicit
   `auto` minimum width sized to content, not `0` — so a long unbroken
   run of text can force the grid, and the page, wider than the
   viewport. Fixed by using `minmax(0, 1fr)` everywhere a grid collapses
   to a single column, matching the pattern already used for the
   multi-column tracks.
2. **`<figure>`'s browser-default margin** (`1em 40px`, from the UA
   stylesheet) isn't zeroed by the shared `tokens.css` reset. Invisible
   normally because most figures sit inside a grid track that just
   absorbs it, but once a figure gets an explicit `width: 100%` (needed
   for the screenshot placeholders below), the default 40px side margins
   sit *outside* that 100% and push the box past the viewport at 390px.
   Fixed locally with `figure { margin: 0; }`; flagging as a candidate
   fix for `tokens.css` itself since any future page combining
   `.image-placeholder` with an explicit width will hit the same bug.
3. **`aspect-ratio` + `min-height` on the same box** (`.image-placeholder`
   sets `min-height: 220px`; this page's `.product__screenshot` adds
   `aspect-ratio: 16/9`) can make the browser derive width *from* the
   min-height-driven height rather than filling the container, once
   min-height is the larger of the two candidate heights. Fixed by
   pinning `width: 100%` on the screenshot placeholder classes so width
   is settled before the aspect ratio applies.

Also revised after an in-browser look, not a bug but a design miss: the
first H1 draft folded the vertical vocabulary into the headline itself
("AP automation for healthcare built around GPO invoices and contract
pricing"), which wraps into 6+ lines at the brand's 84px H1 scale and
makes the hero disproportionately tall. Shortened the H1 to the bare
query echo and moved the vocabulary to the H4 subhead, which is sized
for a longer line. `/ad-ap-automation-manufacturing` and
`/ad-ap-automation-construction` carry the same fix.

**Caveat on these screenshots:** this sandbox has no outbound access to
Google Fonts (confirmed via `net::ERR_CONNECTION_RESET` in the console),
so Noto Sans never loads and the browser substitutes a wider system
sans-serif for the QA renders. "AP automation for **manufacturing**"
still breaks mid-word on that fallback font at 1440px even after the
fixes above; `hyphens: auto` is set on the H1 as a graceful fallback
where a hyphenation dictionary is available, but this is very likely a
fallback-font artifact rather than a real Noto Sans Light rendering
issue — worth a final look once real fonts are confirmed loading, not
a blocker.

## Departures / flags

- **Shared system reconciliation.** This branch was built starting from
  the canonical `/mockups/_system/tokens.css` and `components.html` as
  they exist on the `ad-brand` branch (archetype 01). Several other
  archetype branches in this repo (`ad-fit-erp`, `ad-qualifier`,
  `ad-category-establishing`, `ad-displacement`, `ad-guide`,
  `ad-modernisation`, `ad-capability`) were each built with their own
  locally-reinvented token names and component markup instead of
  importing the real shared file — e.g. `--fs-h1` instead of the
  canonical `.text-h1` class, `.box` instead of `.box-grey10`, `.wrap`
  instead of `.container`. This page and its sibling verticals use the
  **canonical** `tokens.css`/class names throughout. Whoever merges these
  branches will need to reconcile that drift — it isn't something this
  build can fix on its own, since it isn't this page's branch that
  diverged. Flagging here per Foundation's own instruction to note
  anything that looks like an inconsistency until you know why.
- **Approval-chain specificity.** The brief asks to "name their...
  approval chain" but only gives document-type examples, not an actual
  chain structure (e.g., which roles sign off in what order). Kept
  generic ("multi-department approval chain") rather than inventing a
  specific sign-off sequence not in evidence — see `PLACEHOLDERS.md`.

## Open questions

- Should healthcare, manufacturing, and construction each get their own
  Campaign 08 ad group with distinct RSA copy, or does one ad group's
  copy need to work across all three (unlikely, given each page's H1 is
  vertical-specific)? Assumed three separate ad groups sharing one
  campaign, matching the brief's "Head keywords for the H1 echo" being
  listed per-vertical.
- The four extra doc-type slots the placeholder convention implies
  (`_1..4`) are only partially filled here (2 of 4) because the brief
  only names two healthcare document types. Left at 2 rather than padding
  with invented ones — see `PLACEHOLDERS.md`.
