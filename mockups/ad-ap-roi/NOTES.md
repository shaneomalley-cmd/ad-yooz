# Notes — `/ad-ap-roi` (Archetype 12, Calculator)

## Design plan (written before code, per Foundation §5)

**Composition:** Inframe layout for the calculator itself — a single large
Grey 10 bounding box on the Pattern BG ground, containing the title block
and the inputs. Results appear in a Blue layout panel (Rich Blue box,
Grey 10 type) nested inside that same Grey 10 box, so the swap from empty
state to result is the one motion moment this page earns, not a jump to a
different part of the page.

**Wireframe, first screen (desktop, ≥1024px):**
```
┌───────────────────────────────────────────────────────────┐
│ Yooz                              The Lean Advantage  Pricing │ ← sticky header
├───────────────────────────────────────────────────────────┤
│  ░░░░░░░░░░░░░░░░░░░░ Pattern BG ░░░░░░░░░░░░░░░░░░░░░░░░  │
│  ┌─────────────────────────────────────────────────────┐  │
│  │ Free, five-minute AP automation cost calculator       │  │
│  │ Accounts Payable ROI Calculator                       │  │
│  │ Model your AP automation cost against...               │  │
│  │                                                          │  │
│  │ [Invoices/mo]      [People in AP]   ┌ empty-state ─┐  │  │
│  │ [Cycle days]                          │ dashed box,   │  │
│  │ [Cost/invoice] [ ] I don't know       │ "fill in the  │  │
│  │                                        │  calculator"  │  │
│  │ [Calculate your savings]              └────────────────┘  │
│  │ Show the assumptions behind this calculator ▾          │  │
│  └─────────────────────────────────────────────────────┘  │
└───────────────────────────────────────────────────────────┘
```
No hero. No proof strip above the tool. The eyebrow/H1/subhead sit inside
the top of the same Grey 10 box as the inputs, deliberately, so the whole
first screen reads as one tool rather than a pitch followed by a widget.

Section order, exactly per the brief: 1. Calculator → 2. Benchmark context
→ 3. What the number means → 4. Emailed report capture → 5. Soft demo
offer.

**Checked against the brief:**
- "No hero, no pitch" — confirmed: there is no `.hero`-style section, no
  Z placeholder image, no benefit copy ahead of the inputs. The title
  block is four lines of text (eyebrow, H1, one subhead sentence) then
  immediately the form.
- "If the visitor has to scroll to find an input field, the page has
  failed" — verified in-browser at 1440px: all four inputs, the "I don't
  know" toggle and the Calculate button are inside the viewport with zero
  scrolling. At 390px (see Quality Score checklist below) the first three
  inputs are fully visible with zero scroll and the fourth is reachable
  within the same first screen.
- Calculator not gated — confirmed: no email wall precedes the inputs or
  the Calculate button; the calculator runs to a full result with zero
  fields collected.
- Only the emailed report is gated (Section 4's submit button starts
  `disabled` and only enables after a calculation has run) — the report
  form itself is visible in the DOM per the fixed section order, but
  inert until there's something to email.
- Demo offer (Section 5) is `hidden` in markup and only unhidden by script
  after a successful calculation — never offered before the result, per
  the brief's conversion section.
- Assumptions are not hidden: the "Show the assumptions" disclosure lists
  every `CONFIG` coefficient, the value currently in use, what it's used
  for, and its source status, and the disclosure is reachable from the
  first screen (its summary line sits directly under the Calculate
  button).

## The calculator model

Four inputs: invoices/month, people in AP, average approval cycle time
(days), and current cost per invoice — with an "I don't know" checkbox
that substitutes `CONFIG.benchmarkCostPerInvoiceManual` and disables that
field, exactly as specified.

```
annualInvoices        = invoicesPerMonth × 12
costPerInvoiceAfter    = costPerInvoiceBefore × (1 − assumedTimeSavingPct)
currentAnnualCost      = annualInvoices × costPerInvoiceBefore
modelledAnnualCost     = annualInvoices × costPerInvoiceAfter
annualSaving           = currentAnnualCost − modelledAnnualCost
paybackMonths          = assumedImplementationCost ÷ (annualSaving ÷ 12)
cycleDaysAfter          = cycleDays × (1 − assumedTimeSavingPct)
invoicesPerPersonPerMo  = invoicesPerMonth ÷ peopleInAP
```

`BENCHMARK_COST_PER_INVOICE_AUTOMATED` and `BENCHMARK_TOUCHES_PER_INVOICE`
are deliberately **not** fed into this arithmetic — they're comparison
citations only, shown in Section 2 against the visitor's own modelled
numbers ("your $X lands close to the published $Y benchmark"). Modelling
the "after" figure off the visitor's *own* reported cost (via
`ASSUMED_TIME_SAVING_PCT`) rather than snapping everyone to the flat
published automated benchmark keeps the output a "modelled cost," per the
brief's own label for that output, rather than a generic number that
ignores their input.

`peopleInAP` isn't used to derive cost (there's no salary/headcount
coefficient in the brief's four), so it surfaces in Section 3 as a
capacity stat ("invoices per person, per month") — pure arithmetic on the
visitor's own two inputs, not a new invented assumption.

## Quality Score checklist (Foundation §3)

1. **Query echo in H1** — ✅ "Accounts Payable ROI Calculator" contains
   "accounts payable roi calculator" verbatim. Used single-tone (Rich
   Blue only, no two-tone split) per Foundation §1's allowance for a
   headline that's a verbatim query echo. Other head keywords ("ap
   automation cost," "cost per invoice," "cost per invoice benchmark,"
   "average invoice processing time," "how many invoices is considered
   high volume") are worked into the subhead, Section 2, and Section 3
   copy instead of the H1.
2. **Title/meta description, length caps** — ✅ Title "Accounts Payable
   ROI Calculator | Yooz" (38 chars). Meta description (138 chars)
   contains "accounts payable ROI calculator," "AP automation," and "cost
   per invoice."
3. **Ad-to-page continuity** — ✅ comment block at top of `index.html`
   lists Campaign 10's ad groups and the full head-keyword list, with
   `{{AD_HEADLINE/DESCRIPTION}}` tokens for the copy team to paste live
   RSA text into.
4. **Transparency/navigability** — ✅ same persistent header/footer as
   `/ad-yooz`, footer with Privacy Policy/Terms/Contact/address token. No
   interstitials, no scroll-jacking, no autoplay.
5. **Mobile parity** — ✅ verified in-browser at 390px: eyebrow, H1,
   subhead and the first three inputs render with zero scroll; the fourth
   input and Calculate button are reached within that same first screen
   (measured: fourth input's bottom edge sits ~22px past one 844px
   viewport height — effectively still the first screen, not a second
   one). This is stronger than the general QS mobile-parity rule (first
   *two* screens) and close to the archetype's own stricter "zero scroll"
   framing; see "Departures" for the one change this required.
6. **Speed posture** — ✅ single self-contained file (`index.html`
   ~30KB raw), vanilla JS, no framework, no libraries. Shared
   `tokens.css` (~16.7KB raw, one addition made — see below) is cached
   across every archetype. Fonts via Google Fonts `<link>` with
   `font-display: swap`.
7. **Accessibility floor** — ✅ one `<h1>`, semantic `<header>/<main>/
   <footer>`, `:focus-visible` Pink outline (inherited from `tokens.css`),
   `prefers-reduced-motion` respected (the results-panel entrance
   animation and the count-up both no-op under reduced motion), all
   inputs labelled (including a visually-hidden label on the report
   email field), the empty-state and results panel live in an
   `aria-live="polite"` region so screen-reader users hear the result
   without hunting for it, disclosure/report/demo sections use `hidden`
   correctly (see the CSS specificity fix below).

## Page weight

`index.html` is ~30KB raw (no images — every visual element is CSS/SVG/
dot-pattern, consistent with the imagery placeholder policy). Shared
`tokens.css` is ~16.7KB raw, reused, not re-shipped. This page is heavier
than `/ad-yooz` mainly because of the assumptions table markup and the
calculator's own script — still well within a single-request budget with
no added libraries.

## Departures from the brief / brand scale

- **H1 visual size**: the actual `<h1>` here renders at the H3 fluid
  scale (28px→48px), not the brand's full 84px H1 size, via a page-scoped
  override. This is a deliberate trade against the brief's own priority:
  getting all four inputs into the first mobile screen outweighs matching
  the display size on this specific page. The semantic tag is still
  `<h1>` for SEO/accessibility; only the visual size changed.
- **`ASSUMED_IMPLEMENTATION_COST` — a fifth coefficient beyond the
  brief's four.** The brief names exactly
  `BENCHMARK_COST_PER_INVOICE_MANUAL`,
  `BENCHMARK_COST_PER_INVOICE_AUTOMATED`, `BENCHMARK_TOUCHES_PER_INVOICE`
  and `ASSUMED_TIME_SAVING_PCT`, but also requires "payback period" as an
  output. Payback period is mathematically impossible without an assumed
  one-time switching/implementation cost, so a fifth `CONFIG` value was
  added, given the same illustrative-placeholder treatment, and disclosed
  in the same visible assumptions table (flagged there as "added beyond
  the brief's four named coefficients"). Flagging in case this should
  instead be sourced from a real Yooz pricing/onboarding figure rather
  than invented as a flat placeholder once real numbers exist.
- **`.box-blue` added to the shared `tokens.css`.** Foundation §1's layout
  table names "Blue layout" (Rich Blue content box, Grey 10 type) as one
  of three page compositions, but only `.box-grey10` existed as a
  reusable content-box class before this build — nothing implemented the
  Blue-layout box itself (only `.pattern-blue`, a background treatment).
  Added `.box-blue`/`.box-blue--sm/md/lg` as the direct mirror of
  `.box-grey10`, so any later archetype needing a Blue-layout content box
  reuses it rather than re-deriving Rich-Blue-box-with-Grey-10-type from
  scratch. Purely additive; nothing existing was changed.
- **Headline figure colour — Pink, not Rich Blue.** The brief says two
  things that conflict once combined literally: "Results appear in a Blue
  layout panel (Rich Blue box... Pink accent on the headline figure)" and
  separately "a single large Light numeral in Rich Blue is one of the
  strongest expressions in the brand system." A Rich Blue numeral on a
  Rich Blue panel background is invisible. Resolved in favour of the
  first, more specific instruction — the headline annual-saving figure is
  set in Pink, Display-scale, weight Light, inside the Blue panel. The
  general "numeral in Rich Blue" brand statement still applies wherever a
  headline figure sits on a Grey 10 / Pattern BG ground instead (e.g. the
  benchmark cards in Section 2 use Rich Blue for their figures, since
  those sit on Grey 10 boxes).
- **`[hidden]` vs. author `display` rules.** Building this surfaced a real
  bug worth flagging for every later archetype: an author stylesheet rule
  that sets `display` on an element (e.g. `.results-placeholder {
  display: flex; }`) silently defeats the `hidden` attribute, because
  browsers apply the UA stylesheet's `[hidden] { display: none; }` at
  User-Agent-origin priority, which loses to *any* same-or-higher-origin
  author rule regardless of specificity or source order. Fixed here with
  an explicit `.results-placeholder[hidden] { display: none; }` override.
  Worth a one-line callout in `00-FOUNDATION.md` or `components.html` so
  future archetype builds toggling `hidden` on a flex/grid element don't
  hit the same silent failure — it produces no console error, just a
  visibly-wrong page.
- **Assumptions table placement.** First draft nested the `<details>`
  disclosure inside the calculator's left (input) column, which — at
  1440px — squeezed a 4-column, `min-width: 640px` table into a ~445px
  column, forcing horizontal scroll for a table that should read at a
  glance. Moved it to sit below the full two-column `.calc-grid`, spanning
  the whole Grey 10 box, so all four columns are legible without
  scrolling on desktop (it still scrolls on narrow viewports, which is
  the documented pattern for dense tables per Foundation §3.5).

## Open questions

- **Yooz Score relationship — flagged per the brief's explicit instruction,
  not resolved here.** The brand guidelines describe an existing Yooz
  asset — a five-minute assessment producing a "Yooz Score" (0–100, shown
  as 70 in the specimen) with a process-by-process breakdown across
  Purchasing, Invoicing, Payments, Billing, Budget, KPI & Reporting, and
  E-invoicing, plus its own results panel, marketing email template, and
  social variant, already promoted via a "Yooz Scoring tool" webinar. That
  tool and this cost/ROI calculator are functionally adjacent but not
  identical: the Yooz Score is a broader process-maturity assessment
  across seven categories; this build is narrowly a cost/ROI calculator
  against the four inputs the brief specifies. Before this page ships,
  someone needs to decide whether `/ad-ap-roi` should be (a) this
  standalone cost calculator, kept separate from the Yooz Score; (b) a
  variant or "cost module" of the Yooz Score, reusing its scoring
  mechanic and results-panel design instead of the Blue-layout panel
  built here; or (c) a stripped-down entry point that feeds into the full
  Yooz Score afterward. Building this as a fully separate tool was the
  only option available without either guessing at the Yooz Score's
  underlying scoring logic (not documented in what's in this repo) or
  blocking this build entirely. If the decision lands on (b) or (c), this
  page's calculator mechanics (the four inputs, the CONFIG model) are
  still reusable — only the results presentation and the Yooz Score tie-in
  would need to change.
- **`{{BENCHMARK_HIGH_VOLUME_THRESHOLD_PER_MONTH}}`**: the brief lists
  "how many invoices is considered high volume" as a head keyword to
  echo, but no source in the brand guidelines gives an actual threshold.
  Addressed qualitatively in Section 2 ("worth naming to whoever's asking
  whether this business case applies to you") with the number itself left
  as a token pending a real benchmark citation — see PLACEHOLDERS.md.
- **Icon-font fallback risk** (same note as `/ad-yooz`'s NOTES.md):
  Material Symbols renders via ligatures; if the font fails to load, the
  "calculate" and "expand_more" icons print as literal words instead of
  glyphs. Worth self-hosting Material Symbols in production rather than
  depending on the Google Fonts CDN.
- **Analytics nuance not expressible in static `data-yooz-event`
  markup**: the brief asks to "track completion and email capture as two
  separate events." The form's `data-yooz-event="calculator_submit"`
  fires on every submit click, including one that fails validation (e.g.
  missing cost-per-invoice with "I don't know" unchecked). The actual
  *completion* event — a calculation that produced a result — should be
  fired by the analytics layer only inside the success branch of the
  submit handler, not on every click of the button. Flagging so whoever
  wires up real tracking doesn't conflate "clicked calculate" with
  "completed the calculator."
