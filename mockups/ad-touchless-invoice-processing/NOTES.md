# Notes — `/ad-touchless-invoice-processing`

## Design plan

Same brand composition as the sibling page: Primary layout, long-form reading
treatment, single ~740px column, sticky desktop TOC / `<details>` on mobile. Reuses
the exact same layout system and `tokens.css` import so the two archetype-13 pages
feel like the same publication, per 00-FOUNDATION.md §6 ("the design system is shared
across all 13 archetypes... let the first screen vary; keep the tokens, components and
footer identical" — here the first screen is intentionally *not* varied, since both
pages are the same archetype).

**ASCII wireframe, first screen (desktop):**

```
┌─────────────────────────────────────────────────────────┐
│ Yooz [wordmark]              Product  Resources  Pricing │
├─────────────────────────────────────────────────────────┤
│                                                           │
│   Accounts payable, explained                            │
│   What Is Touchless Invoice Processing?                  │
│                                                           │
│   Touchless invoice processing is when an invoice moves  │
│   from arrival to payment without anyone keying its data │
│   in by hand... [full answer before any framing]         │
│                                                           │
└─────────────────────────────────────────────────────────┘
```

**Section order:** Answer → Detail (how an invoice goes touchless, using the same
six-stage diagram with Capture/Review highlighted as the stages that decide
touchless-or-not, plus a section on what breaks touchless) → Related concepts →
Gated deeper asset → Newsletter.

## Why the process diagram highlights Capture and Review

The parent page (`/ad-ap-automation-guide`) uses the plain six-stage diagram to teach
the whole process. This page reuses the identical diagram — same brand vocabulary,
same component — but adds a two-item legend and highlights the two stages where
"touchless" is actually decided, so the diagram does new explanatory work instead of
being a duplicate graphic with a different caption.

## QS checklist (00-FOUNDATION.md §3)

1. **Query echo in H1** — ✅ "What Is Touchless Invoice Processing?" — see the open
   question below on where this term itself came from.
2. **Title/meta** — ✅ Title 44 chars, description 137 chars, both contain "touchless
   invoice processing."
3. **Ad-to-page continuity** — ✅ comment block present; flagged as blocked on the
   open question below.
4. **Transparency/navigability** — ✅ identical header/footer pattern to the sibling
   page.
5. **Mobile parity** — ✅ same treatment: full answer is the entire first mobile
   screen, TOC collapses to `<details>`, process diagram stacks vertically under
   600px with the legend still visible.
6. **Speed posture** — ✅ single file, shared cached `tokens.css`, no JS, no raster
   images. Page weight: **16.8 KB** HTML + the same shared **10.8 KB** `tokens.css`
   (already cached if a visitor arrives via the sibling page).
7. **Accessibility floor** — ✅ same pattern as the sibling page: one `<h1>`, semantic
   landmarks, global focus ring, `prefers-reduced-motion` respected, labelled inputs,
   `role="img"` + `aria-label` on the diagram (this time describing which stages are
   highlighted and why).

## Deliberate departures from the brief, and why

Same three as `/ad-ap-automation-guide`'s NOTES.md (single-tone query-echo H1,
Regular-weight list items in the "what breaks touchless" list, no Material Symbols
load) — not repeated here in full; see that file.

One additional departure specific to this page: **no "touchless rate" statistic
anywhere**, including in the gated-asset pitch. It's the single number most likely to
get invented for this exact topic ("achieve 90% touchless processing" is the kind of
line that shows up on competitor pages), and 00-FOUNDATION.md §2 is explicit that a
plausible fabricated number here is worse than useless. See PLACEHOLDERS.md.

## Open questions for the copy/paid-media team

- **The head keyword for this page is inferred, not sourced.** 13-guide.md lists
  `/ad-touchless-invoice-processing` as one of the two pages this archetype covers,
  but its keyword list (`what is accounts payable automation`, `...software`, `what is
  ap software`, `agentic ai accounts payable`, `autonomous accounts payable`) doesn't
  include a touchless-specific term or its search volume. "What is touchless invoice
  processing" was assumed as the natural head term from the page slug itself. **Before
  this ships, confirm the actual Campaign 11 ad group and head keyword this page is
  meant to rank/serve for** — if it turns out to be a different term (e.g. "touchless
  AP processing," "invoice automation touchless"), the H1 and title need to echo that
  term instead, per QS requirement 1.
- Same two inert Related Concepts cards as the sibling page (`3-way matching`,
  `invoice capture methods`) — no pages exist to link to yet.
- Not measured on demo requests, same as the sibling page — success here is checklist
  downloads + newsletter opt-ins.

## System note

Imports the same `/mockups/_system/tokens.css` authored for this build — see that
file's header comment and the sibling page's NOTES.md for the full explanation of why
it was created now instead of by archetype 01.
