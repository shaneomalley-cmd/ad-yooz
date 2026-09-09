# Notes — `/ad-ap-automation-hub` (Archetype 04, Forking hub)

Campaign build priority 5. Per the brief, this is "the one untested bet in
the plan" — read this file's "How to diagnose the fork" section before
treating this page as done; the build isn't finished until that
instrumentation question is answered, not just the layout.

## Design plan (written before code, per Foundation §5)

**Composition:** Inframe layout — Pattern BG ground throughout, Grey 10
content boxes, Rich Blue type, Pink CTA. Two Grey 10 boxes of identical
size (`box-grey10--lg`, same padding, same grid track) side by side at
desktop; stacked at mobile with the stacking order randomised on load
(see "Departures" below for why randomised rather than A/B'd). Neither box
gets a Pink fill — Pink is reserved for the button inside each box, so
both paths read as visually identical peers. This is also the one page in
the set with two co-primary CTAs (`.btn-primary` on both chooser buttons),
per the brief's explicit exception to the global "one primary CTA per
screen" rule.

**Wireframe, first screen (desktop, ≥1024px):**
```
┌───────────────────────────────────────────────────────────────┐
│ Yooz                                The Lean Advantage Pricing │ ← sticky header
├───────────────────────────────────────────────────────────────┤
│ ░░░░░░░░░░░░░░░░░░░░░░ Pattern BG ░░░░░░░░░░░░░░░░░░░░░░░░░░░░ │
│  Two ways to use this page                                     │
│  AP automation solutions                                        │
│  Whether you searched "AP automation," "accounts payable       │
│  automation"... that query alone doesn't say which visitor      │
│  you are. So this page asks instead of guessing.                │
│  ┌───────────────────────┐   ┌───────────────────────┐         │
│  │ New to AP automation    │   │ Comparing vendors        │     │
│  │ What is AP automation,  │   │ See Yooz next to who      │     │
│  │ and what does it cost?  │   │ you're already looking at │     │
│  │ [Show me the explainer] │   │ [Compare vendors]          │     │
│  └───────────────────────┘   └───────────────────────┘         │
└───────────────────────────────────────────────────────────────┘
```
Nothing sits above the chooser except the persistent header, per the
brief. Both boxes are equal in size, position, and CTA treatment; no
`aria-current`/outline styling applies until a visitor actually picks one.

Section order, exactly per the brief: 1. Two-path chooser → 2. Path A
(explainer → calculator) → 3. Path B (comparison table) → 4. a single
form at the end of each path. Path A and Path B are both present in the
DOM from load (so a browser's in-page search or a screen reader in
"browse" mode can still reach either), but both carry the `hidden`
attribute until their chooser button is clicked — true in-page
progressive disclosure on one URL, not a route change, per the brief's
explicit instruction to keep a single destination for Quality Score.

**Checked against the brief:**
- "Ask, do not guess" / "two clearly equal paths" — confirmed: identical
  box size, identical CTA style, no default `aria-current`, no path
  pre-opened on load.
- "No default selection, no visual preference" — confirmed: neither
  `hidden` attribute is removed until a click happens; CSS gives both
  cards the same `box-grey10--lg` treatment with no order-based emphasis
  (see mobile-randomisation departure below for the one place a fixed
  order would have silently reintroduced a preference).
- "No demo form above the fold" — confirmed: Path B's demo form is the
  last thing on the page, reachable only after clicking "Compare
  vendors" and scrolling past the full table. It cannot suppress the
  explainer path because it isn't rendered (not just visually hidden —
  `hidden` sets `display:none`) until that specific choice is made.
- "The fork click must be tracked as a distinct event" — confirmed:
  `data-yooz-event="hub-path-explainer"` and `data-yooz-event="hub-path-
  compare"` sit directly on the two chooser buttons, matching the brief's
  exact event names.
- "One motion moment: the chosen path opening" — confirmed: `.path-panel`
  has exactly one CSS `@keyframes` entrance (fade + 14px slide-up, 450ms),
  disabled under `prefers-reduced-motion`, and it's the only animation on
  the page. Re-triggered (not just shown) when switching paths via the
  "actually, I'm comparing vendors" / "actually, I'm new to this category"
  links, so a path-switch still reads as something changing.

## How to diagnose the fork

Per the brief's success criteria ("design so the diagnosis is possible"),
these are the three events that, read together, tell Shane whether the
fork is working — not just whether the page gets traffic:

1. **`hub-path-explainer` vs. `hub-path-compare`** — the split ratio
   itself. The brief's own estimate is roughly 60% glossary-seekers / 40%
   buyers; if the observed click split lands far from that (e.g. 90/10 in
   either direction), it's a signal the two chooser cards aren't actually
   reading as equally weighted — worth a visual audit before concluding
   anything about visitor intent.
2. **`hub-patha-calculator-submit` vs. `hub-pathb-demo-submit`**, each as
   a completion rate *within* its own path (chosen → completed, not
   completed → total sessions). This is the number that tells you whether
   a chosen path actually delivers, independent of how many people chose
   it. A path that gets clicked often but rarely completes is a UX
   problem inside that path, not evidence the fork itself was wrong.
3. **Downstream pipeline attribution on Path A's captured leads.** Path A
   is a single email-only capture (`hub-patha-calculator-submit`) — cheap
   to get, and by itself proves nothing about revenue. The real test of
   whether campaign 02b is worth ring-fencing is whether those emails
   later produce a `demo_request`/SQL event in the CRM within a defined
   window (30–60 days is a reasonable first cut). Without this third
   event, events 1 and 2 alone would make Path A look "successful" even
   if it's a content freebie that never turns into pipeline — which is
   exactly the failure mode a quarter-long ring-fenced experiment is
   supposed to catch before campaign 02 gets starved for nothing.

None of these three events exist as a working pipeline in this repo (no
analytics vendor is wired in) — this section describes what the `data-
yooz-event` attributes already on the page are for, so whoever wires up
GTM/GA4 knows which three numbers to put on one dashboard together rather
than reporting click counts in isolation.

## Quality Score checklist (Foundation §3)

1. **Query echo in H1** — ✅ "AP automation solutions" is verbatim (case
   only) against the highest-CPC bare category term. Single-tone Rich
   Blue H1 (no two-tone split), per Foundation §1's allowance for a
   headline that's a literal query echo — matching `/ad-ap-comparison`'s
   precedent. The other five head keywords ("ap automation", "accounts
   payable automation", "payables automation", "ap automation tools",
   "accounts payable solutions") are worked verbatim into the intro
   paragraph's direct list, since this page's whole premise is that the
   query can't distinguish the visitor — naming the actual queries
   out loud is itself part of the "ask, don't guess" framing, not just a
   keyword-stuffing exercise.
2. **Title/meta description** — ✅ Title "AP Automation Solutions | Learn
   or Compare | Yooz" (48 chars). Meta description (137 chars) contains
   "AP automation" and signals the fork itself ("Two ways to use this
   page"), which doubles as ad-relevance and as an honest expectation-set
   for Expected CTR — nobody clicks through to just a generic pitch.
3. **Ad-to-page continuity** — ✅ comment block at top of `index.html`
   names Campaign 02b, both ad groups, the full six-keyword list, and
   `{{AD_HEADLINE/DESCRIPTION}}` tokens for the copy team.
4. **Transparency/navigability** — ✅ same persistent header/footer as
   every other archetype in this repo, footer with Privacy Policy/Terms/
   Contact/address token. No interstitials, no scroll-jacking, no
   autoplay — the explainer is a static placeholder frame, not an
   autoplaying video.
5. **Mobile parity** — ✅ verified in-browser at 390px: eyebrow, H1,
   intro paragraph, and both chooser cards (stacked, each with its own
   visible CTA) all render within the first two mobile screens — the
   whole point of this archetype's brief is that the fork itself *is*
   the first screen, so "reachable in two screens" was the easiest of
   the seven checks to satisfy. The comparison table uses the same
   horizontally-scrollable-with-sticky-first-column pattern as
   `/ad-ap-comparison` (`.compare-table-wrap`, `overflow-x:auto`,
   `role="region"`, visible scroll hint under 1024px) rather than a
   stacked-card list, per the general QS rule's named alternative.
6. **Speed posture** — ✅ single self-contained file, ~34KB raw (heavier
   than `/ad-ap-comparison`'s ~20KB because this page carries both that
   table *and* a compact calculator script; lighter than `/ad-ap-roi`'s
   ~30KB script alone since this calculator only models two coefficients,
   not five). Shared `tokens.css` (~16.7KB) and `components.html` are
   unchanged — nothing needed adding to the shared system for this
   archetype. Fonts load via Google Fonts `<link>` with `font-display:
   swap`.
7. **Accessibility floor** — ✅ one `<h1>` ("AP automation solutions");
   each chooser card and each path panel then uses `<h2>`/`<h3>` in
   document order, not a second `<h1>`. `:focus-visible` Pink outline
   (inherited from `tokens.css`). `prefers-reduced-motion` respected —
   both the path-open animation and the calculator's results-reveal
   animation are disabled, and the `scrollIntoView` call falls back to
   `behavior:'auto'` under reduced motion. Both chooser buttons carry
   `aria-expanded` + `aria-controls` pointing at their panel's `id`, so
   assistive tech gets the same disclosure semantics as a native
   `<details>` even though the visual treatment needed two independent
   panels rather than one. All form inputs labelled (including the
   "I don't know" checkbox and both hidden-until-relevant panels' fields).
   The explainer video and the "I don't know" substitution logic use
   `role="img"`/`aria-label` and a visible caption per the imagery
   placeholder policy.

## Page weight

`index.html` is ~34KB raw. Shared `tokens.css` (~16.7KB) is cached across
every archetype already built in this repo, not re-shipped per page. No
new classes were added to `tokens.css` or `components.html` — the
comparison-table CSS is copied from `/ad-ap-comparison`'s page-specific
`<style>` block (same class names, condensed to five rows instead of
seven — G2 rating, integrations, capture channels, category, and price;
Capterra rating and analyst recognition were dropped here since the "See
the full comparison" tertiary link sends anyone who wants the complete
picture to `/ad-ap-comparison` itself, and duplicating all seven rows on
a page whose job is to fork traffic quickly would work against this
archetype's own brevity mandate).

## Departures from the brief / brand scale

- **Mobile stacking order: randomised via a one-line inline script, not
  A/B'd.** The brief allows either. This repo has no experimentation
  platform wired in (no client-side flagging, no server-side variant
  assignment), so a true A/B split isn't buildable at the mockup stage —
  `Math.random() < 0.5` on each page load is the honest equivalent of "not
  fixed" without pretending a testing framework exists. It runs
  synchronously before first paint (a small blocking script placed right
  after the two chooser cards' markup, not deferred), so there's no
  flash of one order changing to the other. Flagging for whoever wires up
  real A/B infrastructure: swap the `Math.random()` call for that
  platform's variant assignment and the rest of the CSS/JS needs no
  change, since it only reads/writes one class name
  (`.chooser-grid--flip`).
- **Path A's calculator is a condensed version of `/ad-ap-roi`'s, not the
  same tool embedded twice.** The full ROI calculator (archetype 12) asks
  for invoices/month, people in AP, approval cycle time, and cost per
  invoice, and models payback period against an assumed implementation
  cost. This page's brief only asks for "a cost benchmark," and Section
  order item 4 requires "a single form at the end of *each* path" — so
  embedding the full five-field/five-coefficient tool here would both
  contradict "a single form" (it already has its own gated report-email
  step as a second form) and duplicate a whole page's worth of
  interaction budget on what's supposed to be a fast, low-commitment
  first path. Kept to two inputs (invoices/month, cost/invoice) plus the
  same "I don't know" benchmark substitution, gated by the one email
  field already on the form rather than a second gate. The two
  coefficients this page's script uses (`benchmarkCostPerInvoiceManual`,
  `assumedTimeSavingPct`) are set to the exact same illustrative values as
  `/ad-ap-roi`'s `CONFIG` object so the two tools can't disagree with each
  other if a visitor tries both — see PLACEHOLDERS.md's "Shared-value
  note."
- **Comparison table condensed to five rows, with a link out to the full
  seven-row table.** See "Page weight" above for the reasoning; flagging
  here too since it's a content decision, not just a byte-count one — if
  research shows visitors on this specific path want the full table
  in-line rather than a click-through, the fix is to paste
  `/ad-ap-comparison`'s remaining two rows (Capterra rating, recent
  analyst/review recognition) back in, since the CSS classes are already
  shared verbatim.
- **"Switch paths" links are an addition beyond the brief.** The brief
  doesn't ask for a way to back out of a chosen path, but "no forced
  path" reads more honestly if a visitor who clicked the wrong box isn't
  stuck scrolling back to the top. Each path panel opens with a small
  tertiary "Actually, I'm comparing vendors" / "Actually, I'm new to this
  category" link that swaps panels in place. Flagging in case this is
  considered scope creep on an archetype whose entire brief is about
  restraint — it's cheap (one button, no extra network request, no extra
  form) and directly serves "ask, don't guess," but it wasn't explicitly
  asked for.
- **Icon-font fallback risk** (same note as every other page in this
  repo): Material Symbols renders via ligatures; if the font fails to
  load, "play_circle", "swap_horiz", "swipe" etc. print as literal words
  instead of glyphs. Worth self-hosting Material Symbols in production,
  as flagged in this repo's earlier `CHECKLIST.md` for Noto Sans.

## Open questions

- **Is email-only really the right gate for Path A's calculator result?**
  The brief is explicit ("Email-only capture on Path A"), and this build
  follows it, but the result panel currently reveals *after* the form
  submits — meaning the visitor commits their email before seeing any
  number. An alternative worth testing once real analytics exist: show
  the modelled benchmark immediately on input (no submit required), and
  only gate the *emailed report* behind the email field — closer to how
  `/ad-ap-roi`'s "Get this as a report" section works as a second,
  separate step. This build kept the calculator itself as the one form
  (matching "a single form at the end of each path" literally) rather
  than splitting it into an ungated calculation plus a gated report,
  which is `/ad-ap-roi`'s pattern but would mean two forms on this path.
  Worth deciding deliberately rather than by default.
- **`{{BEGINNER_GUIDE_URL}}` and `{{COMPARISON_GUIDE_URL}}`** — neither
  asset is confirmed to exist yet. If the beginner's guide doesn't exist,
  Path A's secondary CTA needs either a real asset before launch or
  removal (not a broken link at the one place this campaign's whole
  quarter-long test depends on looking credible).
- **Five-row vs. seven-row comparison table** — see "Departures" above;
  this is a real open decision, not just a build note.
- **Canonical URL** uses `https://getyooz.com/en-us/ad-ap-automation-hub`,
  matching this repo's existing `/en-us/ad-<slug>` convention (see
  `/ad-yooz`, `/ad-ap-comparison`, `/ad-ap-roi`). Confirm with dev/SEO
  before treating as final.
