# Notes — `/ad-ap-comparison` (Archetype 11, Proof / list)

## Design plan (written before code, per Foundation §5)

**Composition:** Primary layout (Pattern BG ground, Grey 10 content
surfaces, Rich Blue type, Pink CTA) for every section — but with **no
hero**. The comparison table itself is the Grey 10 content surface for
section 1; there's no separate copy-box-plus-image split. Section 3
("Choose someone else if…") sits on a Pattern Pink strip to mark it as
the one candid, must-not-skip callout on the page — everywhere else is
Pattern BG.

**Wireframe, first screen (desktop, ≥1024px):**
```
┌───────────────────────────────────────────────────────────────┐
│ Yooz                                The Lean Advantage Pricing │ ← sticky header
├───────────────────────────────────────────────────────────────┤
│ ░░░░░░░░░░░░░░░░░░░░░░ Pattern BG ░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │
│  An honest, side-by-side comparison                            │
│  Best accounts payable automation software                     │
│  Whatever you searched — "best AP automation software"...      │
│  Sorted alphabetically, not by score, and it includes vendors   │
│  Yooz doesn't always win against.                               │
│  ┌────────────────────────────────────────────────────────┐   │
│  │ Compare by │ Bill.com │ Ramp │ Tipalti │ ●Yooz          │   │ ← Rich Blue header
│  │ (sticky)   │──────────┼──────┼─────────┼────────────────│   │
│  │ G2 rating  │  {{}}    │ {{}} │  {{}}   │ {{G2_RATING}}  │   │ ← Grey 10/20 zebra
│  │ Capterra   │  {{}}    │ {{}} │  {{}}   │ {{CAPTERRA}}   │   │
│  │ ERP integr.│  {{}}    │ {{}} │  {{}}   │ 250+           │   │
│  │ Capture ch.│  {{}}    │ {{}} │  {{}}   │ email, scan... │   │
│  │ Category   │  {{}}    │ {{}} │  {{}}   │ AP automation  │   │
│  │ Start price│  {{}}    │ {{}} │  {{}}   │ {{}}           │   │
│  │ Recognition│  {{}}    │ {{}} │  {{}}   │ SourceForge... │   │
│  └────────────────────────────────────────────────────────┘   │
└───────────────────────────────────────────────────────────────┘
```
Section order, exactly per the brief: 1. Comparison table → 2. Third-party
validation → 3. Where Yooz fits and doesn't → 4. Analyst position →
5. Form.

**Checked against the brief:**
- "No hero. The table *is* the first screen" — confirmed: `.compare-hero`
  is eyebrow + H1 + two short paragraphs, then the table immediately
  follows in the same section, in normal document flow. No `.hero__grid`,
  no Z placeholder image anywhere on this page.
- "Including vendors Yooz loses to" — confirmed: Bill.com, Ramp, and
  Tipalti are named columns, not omitted or footnoted.
- "Sort by something neutral and disclose the sort" — confirmed: columns
  are alphabetical (Bill.com, Ramp, Tipalti, Yooz), which also happens to
  put Yooz last rather than first — a genuinely neutral sort, not a
  contrived one that coincidentally favours Yooz. Disclosed twice: in the
  intro paragraph ("Sorted alphabetically, not by score") and in the
  table's own header ("Sorted A–Z" under "Compare by") and `<caption>`
  (visually hidden, read by screen readers).
- "Omit a competitor the visitor expects to see" — confirmed present:
  Bill.com and Tipalti, the two the brief names explicitly, plus Ramp
  (named in the ad group "Ramp & Bill.com").
- "Do not rank Yooz #1 by default" — confirmed: no ranking, ordering, or
  score column exists at all; every row is a neutral attribute, not a
  win/loss verdict, and Yooz's column carries no crown/badge/"winner"
  treatment.
- "Do not present a single-vendor pitch" — confirmed: sections 2–4 stay
  in comparison/positioning register (recognition, disqualifiers,
  analyst-absence honesty) rather than benefit copy about Yooz alone;
  section 3 explicitly sends some visitors elsewhere.
- Yooz column marker uses a decorative Pink dot (`aria-hidden`) plus a
  3px Pink left border on the column, not coloured text — see
  "Departures" below for why.

## Vendor selection

Four columns: **Bill.com**, **Ramp**, **Tipalti**, **Yooz**. Bill.com and
Tipalti are named directly in the brief as vendors whose absence "reads
as rigged." Ramp is added because it's the other half of Campaign 09's
"Ramp & Bill.com" ad group — a visitor in that ad group is comparing
Yooz against both by name. A fifth or sixth vendor (AvidXchange, Stampli,
MineralTree, etc.) was considered and deliberately left out rather than
padding the table — the brief's exemplar (a Gartner-reviews-style table)
rewards a focused, scannable set over an exhaustive one, and every added
column is another row of `{{TOKEN}}` placeholders with no sourced data
behind them yet (see Placeholders below and Open questions).

## Table structure

Criteria run as **rows**, vendors as **column headers** — the orientation
implied by "sticky first column" in the brief (the first column holds
the row labels, not a vendor). Seven criteria rows, in a CFO-skim order:
the two review-site ratings first (what a listicle reader already has a
mental model for), then the two verified Yooz capabilities where a
factual answer is possible (integrations, capture channels), then
category focus, price, and recognition last, since that's most likely to
need the most caveats.

Every competitor cell is a `{{TOKEN}}` — none of Bill.com's, Ramp's, or
Tipalti's specs, ratings, or pricing are sourced in this repo, and a
comparison table is exactly the highest-liability place to guess at a
named competitor's numbers (Foundation §2's claims-discipline rule).
Yooz's own cells use the two facts Foundation §2 clears for direct use
(250+ financial systems; the eight capture channels) and the real award
names Foundation §11 clears for direct use (SourceForge Leader, Capterra
Shortlist); every other Yooz cell (G2/Capterra rating figures, starting
price) is still a token, matching `/ad-yooz`'s existing token set so the
same `{{G2_RATING}}` etc. resolve identically everywhere they appear.

## Quality Score checklist (Foundation §3)

1. **Query echo in H1** — ✅ "Best accounts payable automation software"
   is the verbatim 320/mo head keyword (case difference only). The other
   five head keywords for this page ("ap automation vendors", "ap
   automation companies", "accounts payable automation software
   comparison", "top accounts payable automation software", "accounts
   payable solution providers") are worked into the intro paragraph,
   section 1's own copy, and the meta description rather than the H1.
   Single-tone Rich Blue H1 (no two-tone split), per Foundation §1's
   allowance for a headline that's a literal query echo. The highest-CPC
   conversational queries are echoed directly in the second intro
   sentence ("best AP automation software," "which accounts payable
   automation solution is the most reliable"), per the brief's own
   instruction that "the page must answer the question as literally
   asked."
2. **Title/meta description** — ✅ Title "Best Accounts Payable
   Automation Software | Yooz" (48 chars). Meta description (138 chars)
   contains "accounts payable automation software" plus all three named
   competitors.
3. **Ad-to-page continuity** — ✅ comment block at top of `index.html`
   lists both campaigns' ad groups and the full head-keyword/
   conversational-query list, with `{{AD_HEADLINE/DESCRIPTION}}` tokens
   for the copy team.
4. **Transparency/navigability** — ✅ same persistent header/footer as
   `/ad-yooz` and `/ad-ap-roi`, footer with Privacy Policy/Terms/Contact/
   address token. No interstitials, no scroll-jacking, no autoplay.
5. **Mobile parity** — ✅ the brief's own layout instruction for this
   archetype (horizontally-scrollable region, sticky first column,
   visible scroll affordance) is the general QS rule's named alternative
   to a stacked card list, so it's used as specified rather than the
   stacked-card pattern. `.compare-table-wrap` scrolls horizontally with
   `overflow-x: auto`, `role="region"` + `tabindex="0"` for keyboard
   scrolling, the first column (`th[scope="row"]`, plus the header's
   first `<th>`) stays `position: sticky; left: 0`, and
   `.compare-table__scroll-hint` (a text + icon affordance) becomes
   visible under 1024px. Everything in sections 1–2 above the fold on
   desktop is reachable within the first two mobile screens. Verified
   in-browser at 1440/1024/768/390px: at 390px, `document.documentElement
   .scrollWidth` matched `window.innerWidth` exactly (390 = 390) after a
   real bug fix — see below — with the table's own internal scroll region
   as the only horizontally-scrollable thing on the page.
6. **Speed posture** — ✅ single self-contained file, no framework, no
   JS at all (this page is fully static — no calculator, no client-side
   toggle logic). `index.html` is ~19KB raw. Shared `tokens.css`
   (~16.7KB raw) and `components.html` are unchanged by this build —
   nothing needed adding to the shared system; the comparison table is
   page-specific markup, per Foundation §6's "the page skeleton is not
   shared" note for this exact archetype.
7. **Accessibility floor** — ✅ one `<h1>`, semantic `<header>/<main>/
   <footer>`, `:focus-visible` Pink outline (inherited from
   `tokens.css`, plus an explicit rule on the scrollable table region),
   all form inputs labelled, `<table>` uses `<caption>` (visually
   hidden, discloses the sort order for screen-reader users), `scope`
   attributes on every header cell, and the Yooz-column marker is a
   decorative `aria-hidden` dot, not a colour-only signal (the column is
   still identified by its "Yooz" text label). No images/Z placeholders
   on this page, so the imagery `alt`-text requirement doesn't apply
   here.

## Page weight

`index.html` is ~20KB raw — heavier than `/ad-yooz` (~13KB), lighter than
`/ad-ap-roi` (~30KB, which carries a full calculator script); this page
has no image placeholders, no Z geometry, and no JavaScript. Shared
`tokens.css` (~16.7KB) is cached across all three pages already built in
this repo, not re-shipped.

## A real bug this build surfaced: flex items and unbroken {{TOKEN}} text

Browser-verified at 390px, this page initially failed the "no horizontal
scroll" QS rule: `document.documentElement.scrollWidth` came back 493px
against a 390px viewport. Root cause: `.fit-list li` is `display: flex`,
and two of its three list items contain a `{{LONG_TOKEN_LIKE_THIS}}`
placeholder with no internal space — a single unbreakable "word." Flex
items default to `min-width: auto`, meaning a flex child won't shrink
below its content's min-content width no matter how narrow the
viewport — so that one unbreakable token was setting the *whole page's*
minimum width, not just wrapping onto its own line the way it would in
normal block flow.

Fixed with `.fit-list li p { min-width: 0; overflow-wrap: anywhere; }`,
plus a page-wide defensive `main { overflow-wrap: anywhere; }` given how
many raw `{{TOKEN}}` strings this specific archetype's copy carries (see
Placeholders) — any of them could reintroduce the same failure mode once
real content replaces them if a future edit reintroduces a flex or grid
wrapper around body copy. Worth a one-line callout in `00-FOUNDATION.md`
or `components.html`, alongside the existing `[hidden]`-vs-`display` note
from the calculator build: **flex/grid children need an explicit
`min-width: 0` (or `min-height: 0` in a column direction) wherever the
content might be, or might later become, a long unbroken string** —
otherwise a real production value (a long SKU, an un-hyphenated German
compound noun, a raw URL) can silently reopen this exact bug after the
tokens are gone. This wasn't visible in either desktop breakpoint
screenshot taken during the build — it only showed up once a real
360–390px viewport check was run, which is why Foundation's own mobile
breakpoint requirement caught it and a quick desktop-only look wouldn't
have.

## Departures from the brief / brand scale

- **Yooz column marker uses a Pink dot + border accent, not Pink text.**
  The brief says "Pink reserved for the Yooz row marker," which read most
  naturally as a small coloured label ("This is us"). Foundation §1's own
  accessibility note is explicit that Pink must never be used for small
  labels or dense table text, and a 12–14px pill label is exactly that
  case. Resolved by marking the Yooz column with a small decorative Pink
  dot (`aria-hidden="true"`, redundant with the visible "Yooz" text so
  nothing depends on colour alone) plus a 3px Pink left border on the
  column body — both are accent-rule uses, which the brand palette
  explicitly allows, rather than Pink-coloured text at a size the
  brand's own contrast testing doesn't clear.
- **Awareness-tier form length: brief overrides Foundation's general
  table.** Foundation §4's table lists archetype 11 under "Mid" awareness
  (3–4 fields), but this archetype's own brief is explicit: "Email-only
  for the guide." Followed the archetype-specific instruction as the more
  precise one (it's naming this exact page, not a general bucket) — the
  primary form here is a single work-email field. The secondary path
  (request a demo) is a `.btn-secondary` link out to the standard
  demo-request flow rather than a second, longer form embedded on this
  page — keeping "one primary CTA per screen" true for section 5 while
  still surfacing the secondary action the brief asks for, the same
  primary+secondary pairing pattern `/ad-yooz`'s hero already uses
  (primary button + lower-commitment link, both visible together).
- **No JSON-LD.** Neither `/ad-yooz` nor `/ad-ap-roi` added structured
  data in this repo's mockups, and Foundation doesn't ask for it as a
  mockup-stage requirement (only the existing site's `BreadcrumbList` is
  mentioned, in the unrelated WordPress-template deliverable). Left out
  here for consistency with the other two built pages; flagging in case
  a `Product`/`FAQPage`/review-aggregate schema is wanted once real
  ratings exist.

## Open questions

- **`{{GARTNER_POSITION_STATEMENT}}` needs a real sentence from the
  team**, per the brief's explicit instruction — this can't be
  responsibly guessed. The current draft structure (state the absence
  plainly, then immediately list what validation Yooz *does* hold) is
  ready to receive that sentence as soon as it exists; see
  PLACEHOLDERS.md.
- **`{{MIN_INVOICE_VOLUME_THRESHOLD}}` and `{{SPECIFIC_CAPABILITY_GAP}}`**
  (section 3's second and third disqualifiers) are structurally real —
  the brief explicitly asks for "if you are under N invoices a month, if
  you need X" — but the actual threshold and the actual capability gap
  need product/sales input rather than an invented number or feature.
  The procurement disqualifier (first bullet) is filled in directly
  because it's a defensible statement about Yooz's own documented process
  vocabulary (Purchase → Capture → Review → Approve → Pay → Export is
  purchase-to-pay, not full source-to-pay), not a claim requiring
  external substantiation.
- **Competitor data sourcing.** Every Bill.com/Ramp/Tipalti cell is a
  token because this repo has no sourced data for any of them. Before
  this ships, whoever owns competitive intelligence needs to fill in
  real, current, citable figures (G2/Capterra ratings shift often enough
  that even "current at time of writing" figures should carry a
  last-verified date in the CMS, not just at token-fill time) — publishing
  stale or guessed competitor numbers is a bigger liability on this page
  than on any other archetype, since the whole page's credibility depends
  on the table reading as neutral and accurate.
- **Icon-font fallback risk** (same note as the other two pages in this
  repo): Material Symbols renders via ligatures; if the font fails to
  load, "swipe" and "priority_high" print as literal words instead of
  glyphs. Worth self-hosting Material Symbols in production.
