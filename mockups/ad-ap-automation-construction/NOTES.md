# Notes — `/ad-ap-automation-construction` (Archetype 09, Fit: Industry)

Campaign 08 FIT – Industry, ad group Construction. Build priority 9.

## Why this page looks structurally different from its siblings

This is deliberate, not an inconsistency — but it looks like one until
you know why, so per Foundation's own instruction this gets called out
explicitly rather than left for a reviewer to puzzle over.

Healthcare and manufacturing both compete against **horizontal AP
vendors with vertical pages** (Rillion, Bottomline, Stampli, Ottimate),
so their argument is "we know your workflow better than the other AP
vendors do" — a straight industry-named hero works because the visitor
has already accepted they want AP automation; the only question is fit.

Construction competes against **vertical ERPs** instead. FoundationSoft
ranks #1 and Jonas Construction ranks #2 for AP-related searches, plus
hh2 and Buildertrend; only AvidXchange holds a true vertical AP page. So
the construction visitor's default answer to "why would I buy this" is
their own ERP's native AP module — which is the same shape of objection
archetype 03 (Category-establishing) answers ("why not just use what I
already have"), not the same shape as healthcare/manufacturing's
argument. Pitching a product before answering that objection would lose
the visitor before the pitch starts.

So this page borrows **archetype 03's opening pattern** (a problem-framed
hero with no primary CTA, followed by an honest multi-option comparison
in Inframe layout, before any product pitch) for sections 1-2, then
picks up the **standard archetype 09 body** — their specific workflow,
industry proof, product, form — for sections 3-6. Reference build for the
borrowed pattern: `ad-category-establishing` branch,
`/ad-accounts-payable-software/index.html` (archetype 03).

## Design plan (written before code, per Foundation §5)

**Layout concept.** Section 1 restates the objection, not the pitch — no
"Book a demo" button until the visitor has seen the four options and the
workflow that follows. Section 2 lays out four options (ERP's native AP
module, manual/spreadsheet, a horizontal AP vendor, Yooz) as identical
Grey 10 boxes on Pattern BG — no box enlarged, colored differently, or
positioned to imply Yooz is already the answer, matching archetype 03's
own discipline on this point. Each card carries a "Good / Watch" pair
rather than a flat pitch, so the comparison reads as honest rather than
a strawman. Sections 3-6 then follow the exact archetype 09 template used
by healthcare and manufacturing.

**Brand composition.** Primary layout (Pattern BG, Grey 10 box, Rich
Blue type, Pink CTA) for the problem-framed hero. Inframe layout (four
equal Grey 10 boxes directly on Pattern BG) for the four-option
comparison. Primary layout again for workflow/proof/product/form,
matching the sibling pages.

**ASCII wireframe — first screen (desktop):**

```
┌──────────────────────────────────────────────────────────┐
│ Yooz [wordmark]                 The Lean Advantage  Pricing│  ← header
├──────────────────────────────────────────────────────────┤
│ (Pattern BG)                                                │
│  ┌────────────────────────────┐                             │
│  │ Before you add another module│        ▁▁▁                │
│  │ H1: Accounts payable software│       ▕ Z ▏  (hero        │
│  │ for construction already ships│       ▔▔▔   placeholder,│
│  │ with your ERP.                │              bottom-left)│
│  │ H4: FoundationSoft and Jonas   │                          │
│  │ both post job costs to the     │                          │
│  │ ledger. Here's what neither    │                          │
│  │ one automates.                 │                          │
│  │ → See the four ways construction│                         │
│  │   teams handle this            │                          │
│  └────────────────────────────┘                             │
└──────────────────────────────────────────────────────────┘
```

The H1 itself was trimmed after an initial draft ran the objection clause
("...already ships with your ERP. Here's what it's missing.") inside the
H1 at the brand's 84px display scale, which produced an oversized hero
that ran several screens tall before reaching the four-option section.
The "here's what it's missing" beat now lives in the H4 subhead instead,
and the hero gained a two-column grid with a Z-frame image (matching the
sibling pages and the archetype 03 reference build's own wireframe,
which also pairs the problem statement with hero imagery) rather than
the earlier text-only single-column box.

No pricing claim, no product pitch, no primary CTA above the fold — the
H1/subhead restate the objection, and the only action is a tertiary link
scrolling to the four-option comparison, exactly matching archetype 03's
own "the primary CTA doesn't appear until the visitor has been walked
through the reasoning."

**Section order** (per this page's specific brief): 1 Problem-framed hero
→ 2 Four-option comparison → 3 Their specific workflow → 4 Industry proof
→ 5 Product → 6 Form. The first primary "Book a demo" CTA appears at the
end of section 3, once the visitor has been walked through both the
comparison and the construction-specific workflow — deliberately later
than the sibling vertical pages, which put it in the hero.

Checked against both briefs' "Do not" lines before writing code: this
page does **not** use the same first screen as
`/ad-ap-automation-manufacturing` (the explicit "do not" in
`09-fit-industry.md`); the four-option comparison does not enlarge or
otherwise crown the Yooz card ahead of the reader reaching it; no
statistic, price, or specific competitor feature claim is stated as fact
without a token — see the competitive-claim flag in `PLACEHOLDERS.md`.

## Query-echo / keyword strategy

Head keywords: "accounts payable software for construction,"
"construction accounts payable software," "ap automation for
construction." The H1 carries "accounts payable software for
construction" verbatim, split at the natural clause boundary between the
query term (Rich Blue) and the objection-framing continuation (Pink) —
consistent with the brand's two-tone rule that the Pink half carries the
part of the sentence that matters, which here is the objection the whole
page exists to answer.

This page's sections 3-6 (workflow/proof/product/form) share the exact
CSS structure used on `/ad-ap-automation-healthcare` and
`/ad-ap-automation-manufacturing`; see that page's NOTES.md for the
in-browser QA findings that apply here unchanged — a grid-collapse
overflow bug (fixed with `minmax(0, 1fr)` on every mobile single-column
track), `<figure>`'s unreset default margin (fixed with `figure {
margin: 0; }`), and an `aspect-ratio`+`min-height` interaction that
needed an explicit `width: 100%` on the screenshot placeholders. All
three were actually caught and fixed via headless-Chromium testing at
1440/1024/768/390px, not just visual inspection.

## Quality Score checklist (Foundation §3)

1. **Query echo in H1** — ✅ "Accounts payable software for construction"
   verbatim.
2. **Title/meta description contain head keyword, length caps** — ✅
   Title "Accounts Payable Software for Construction | Yooz" (49 chars).
   Meta description (128 chars) contains "Accounts payable software for
   construction."
3. **Ad-to-page continuity** — ✅ comment block at top of `index.html`
   also documents the structural departure so the copy team and any
   future maintainer isn't surprised by the missing hero CTA.
4. **Transparency/navigability** — ✅ persistent header/footer, same as
   every other archetype page. No interstitials, no scroll-jacking, no
   autoplay.
5. **Mobile parity** — ✅ verified at 390px: H1, subhead, and the single
   tertiary CTA render inside the first mobile screen; the four-option
   comparison (which stacks to one column below 600px) is reachable by
   the second/third mobile screen. This page is intentionally longer
   before the first primary CTA than its siblings — a direct consequence
   of borrowing archetype 03's "no pitch before the objection is
   answered" structure — so QS's "everything above the fold on desktop
   reachable in the first two mobile screens" is satisfied for the hero
   content itself, but the primary conversion action sits further down
   the scroll than on the sibling vertical pages. Flagging as an open
   question below.
6. **Speed posture** — ✅ single self-contained file, no JS, no
   framework. `index.html` is ~23KB raw (the largest of the three, from
   the extra comparison section) — shared `tokens.css` (16KB) is cached
   once across every archetype page.
7. **Accessibility floor** — ✅ one `<h1>`, semantic landmarks,
   `:focus-visible` (inherited from `tokens.css`), `prefers-reduced-motion`
   respected, all form inputs labelled, all placeholder imagery uses
   `role="img"` + `aria-label` plus a visible caption.

## Departures / flags

- **Shared system reconciliation** — same flag as
  `/ad-ap-automation-healthcare/NOTES.md`: this page uses the canonical
  `tokens.css` from the `ad-brand` branch, not the locally-reinvented
  variant several other archetype branches (including the
  `ad-category-establishing` branch this page's opening pattern is
  modeled on) built for themselves before the shared system existed or
  without importing it. The **structure** of the four-option comparison
  is borrowed from that branch's `/ad-accounts-payable-software/`
  build; the **markup and class names** are re-authored against the
  canonical system so this page doesn't inherit that drift.
- **Competitive claim needs verification** — see `PLACEHOLDERS.md`,
  `FOUNDATIONSOFT_JONAS_AP_GAP`. The comparison card for "Your
  construction ERP's AP module" states that lien waiver and retainage
  tracking typically live in spreadsheets alongside a native module.
  This is inferred from the brief's own competitive framing, not
  fabricated, but it names two real competitors and must be checked
  against their actual current product before publish.
- **No hero CTA** is intentional (see Design plan above), not an
  oversight — flagging explicitly since every other archetype 09 page,
  and most other archetypes in this repo, put a primary CTA in the hero.

## Open questions

- Is deferring the first primary CTA to the end of section 3 (rather
  than, say, adding a soft primary CTA under the Yooz card in section 2)
  too conservative for a page that still needs to convert on a genuine,
  if small, keyword? Archetype 03's own build makes the same choice, but
  that page has six sections before its form and a bigger keyword base;
  this page is shorter and lower-volume. Worth a stakeholder gut-check
  before publish.
- Same as the sibling pages: whether Construction gets its own Campaign
  08 ad group with distinct RSA copy matching this page's problem-framed
  hero (which reads differently from a typical FIT-industry ad promise
  and needs the RSA copy to set that expectation, not promise a straight
  demo).
