# Notes — `/ad-ap-automation-manufacturing` (Archetype 09, Fit: Industry)

Campaign 08 FIT – Industry, ad group Manufacturing. Build priority 9.
Structurally identical to `/ad-ap-automation-healthcare` (built first);
this file documents only what differs. See that page's `NOTES.md` for the
full design plan, QS checklist reasoning, the shared-system drift flag,
and the in-browser QA findings (grid-collapse overflow, `<figure>`
default margin, `aspect-ratio`+`min-height` width bug) — all apply here
unchanged, since this page shares the same CSS structure verbatim.

## What differs from `/ad-ap-automation-healthcare`

- **Vertical vocabulary.** H1 is the bare query echo, "AP automation for
  manufacturing" (verbatim); the vocabulary lives in the H4 subhead
  instead — "Built around goods receipts and three-way match — exceptions
  routed through your existing approval chain, automatically." (Same
  H1-length fix as healthcare: an earlier draft folded the vocabulary
  into the H1 itself and produced an oversized hero — see healthcare's
  NOTES.md for the full reasoning.) Workflow section names the two
  document-type concepts the brief gives for this vertical: goods
  receipts and three-way match against production POs — both flagged for
  SME verification in `PLACEHOLDERS.md`, same discipline as healthcare.
- **Title/meta description** — "AP Automation for Manufacturing | Yooz"
  (39 chars); meta description (117 chars) contains "AP automation for
  manufacturing."
- **Product section stage copy** — tuned to reference production POs and
  three-way match exceptions instead of GPO contract pricing, but the
  six-stage Purchase→Capture→Review→Approve→Pay→Export sequence itself is
  unchanged, per Foundation's brand-approved process vocabulary.

## Quality Score checklist (Foundation §3)

Same posture as `/ad-ap-automation-healthcare` — one `<h1>` with verbatim
query echo, title/description within length caps, ad-continuity comment
block, persistent header/footer, mobile parity verified at 390px (H1,
subhead, both CTAs above the fold; workflow section within two mobile
screens), single self-contained file (~17KB raw) reusing the shared
16KB `tokens.css`, and the same accessibility floor (one `<h1>`,
`:focus-visible`, `prefers-reduced-motion`, labelled inputs, captioned
placeholders).

## Open questions

Same as `/ad-ap-automation-healthcare`: whether this vertical gets its
own Campaign 08 ad group, and the doc-type slot count (2 of the `_1..4`
convention filled, matching what the brief actually names for this
vertical rather than padding with invented terms).
