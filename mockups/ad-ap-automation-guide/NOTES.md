# Notes — `/ad-ap-automation-guide`

## Design plan

**Brand composition:** Primary layout, long-form reading treatment (00-FOUNDATION.md
§Layout patterns + 13-guide.md §Brand composition) — Grey 10 page on Grey 10, single
reading column capped at ~740px (under 80 characters at 17px body), H2/H3 structure,
sticky in-page contents at desktop. This is the one archetype that should read as a
document, not a landing page, so there's no hero image, no stat row, no award band —
just the answer, then the detail.

**ASCII wireframe, first screen (desktop):**

```
┌─────────────────────────────────────────────────────────┐
│ Yooz [wordmark]              Product  Resources  Pricing │  <- header
├─────────────────────────────────────────────────────────┤
│                                                           │
│   Accounts payable, explained                            │  <- eyebrow
│   What Is Accounts Payable Automation?                   │  <- H1, single-tone
│   (query echo, not two-tone — see "departures" below)     │     Rich Blue
│                                                           │
│   Accounts payable automation is software that replaces  │  <- answer paragraph,
│   the manual steps of paying a business's bills...       │     100 words, no
│   [continues — full definition before any framing]       │     framing above it
│                                                           │
└─────────────────────────────────────────────────────────┘
```

No image, no CTA, no brand statement above the answer — the brief's "answer the
question in the first 100 words" is read literally: the H1 states the question, the
very next paragraph is the answer.

**Section order:** Answer → Detail (how it works, six-stage diagram, the "AP
software" and "agentic AI / autonomous AP" query-variant subsections) → Related
concepts → Gated deeper asset → Newsletter. Matches 13-guide.md §Section order
exactly.

## Why two sub-questions live inside "Detail" instead of getting their own H2s

The ad group's other head terms — "what is accounts payable automation software,"
"what is ap software," "agentic ai accounts payable," "autonomous accounts payable" —
are all variants of the same core concept, not different concepts. Splitting them
into full sibling sections would repeat the six-stage explanation four times. Instead
they're H3 subsections inside Detail, each directly answering its own query variant
in its opening sentence, so the page still earns relevance for all five terms without
turning into five separate glossary entries.

## QS checklist (00-FOUNDATION.md §3)

1. **Query echo in H1** — ✅ "What Is Accounts Payable Automation?" is the head
   keyword (260/mo) verbatim, inflectional change only (added "?").
2. **Title/meta** — ✅ Title 43 chars, both contain "Accounts Payable Automation."
   Description 135 chars, contains "AP automation software." Both under the caps.
3. **Ad-to-page continuity** — ✅ HTML comment block at the top of `index.html`
   lists the fields for the copy team to fill; see `{{AD_HEADLINE_1..3}}` in
   PLACEHOLDERS.md.
4. **Transparency/navigability** — ✅ Persistent header, Yooz wordmark → getyooz.com,
   footer with Privacy/Terms/Contact + address placeholder. No interstitials, no
   scroll-jacking, no autoplay.
5. **Mobile parity** — ✅ Everything above the fold on desktop (eyebrow, H1, full
   answer paragraph) is the entire first mobile screen too — there's no hero content
   that gets pushed below the fold on mobile, because there never was any. The desktop
   sticky TOC becomes a native `<details>` disclosure on mobile (no JS). The process
   diagram switches from a horizontal row to a vertical stack under 600px instead of
   squashing six columns.
6. **Speed posture** — ✅ Single self-contained file, one shared `tokens.css` import
   (cached across every archetype-13 page), Noto Sans via `font-display: swap`, zero
   JS, zero raster images — the two "screenshot"/imagery slots are CSS gradient
   placeholders per the imagery policy. Page weight: **17.9 KB** HTML + **10.8 KB**
   shared `tokens.css` (loaded once, cached on the second page) = **~28.7 KB**
   combined on first load, ~18 KB on any subsequent archetype-13 page view. Fonts are
   the only external request.
7. **Accessibility floor** — ✅ One `<h1>`, semantic `<header>/<nav>/<main>/<footer>`,
   `:focus-visible` set to the brand's Pink 2px outline / 2px offset globally in
   `tokens.css`, `prefers-reduced-motion` respected (kills `scroll-behavior: smooth`
   and any transition), both form inputs labelled (the newsletter field uses a
   visually-hidden label), the process diagram carries `role="img"` with a text
   `aria-label` describing the sequence, both image placeholders have descriptive
   `alt`-equivalent captions.

## Deliberate departures from the brief, and why

- **Single-tone H1, not two-tone.** 00-FOUNDATION.md §2b explicitly allows this:
  "the right choice when the headline is a query echo that shouldn't be visually
  broken." The head keyword itself doesn't have a natural clause split, and QS
  requirement 1 needs it verbatim — a Pink/Blue split would have to break mid-phrase,
  which §5's design guardrails rule out.
- **List items at Regular (400), not Light (300).** 00-FOUNDATION.md §Typography
  already names this as an accepted departure for "any dense data block." This page
  is closer to that than a typical marketing bullet list — a skeptical reader working
  through a six-item process breakdown shouldn't be squinting either.
- **No Material Symbols font load.** The brand's icon system is Material Symbols, but
  this page only needs two small glyphs (a mobile TOC chevron, tertiary-style arrows),
  both drawn as unicode characters/CSS instead of loading an icon font — consistent
  with how the brand's own tertiary-link examples use a plain arrow character. Flagged
  in `tokens.css` for any future archetype-13 page that needs a real icon set.
- **Dot pattern pitch is a placeholder value.** "40%/600% spacing" etc. isn't a pixel
  spec anywhere in 00-FOUNDATION.md — the pitch values in `tokens.css` are a
  reasonable visual read, not sourced from a brand asset. Reconcile against the real
  Yooz pattern spec when archetype 01 (Brand) is built.

## Open questions for the copy/paid-media team

- The `/accounts-payable-fraud` link in Related Concepts assumes that page's nav/URL
  structure is a sibling path (`/accounts-payable-fraud`), matching how 13-guide.md
  names it. Confirm against the live site.
- Two Related Concepts cards (`3-way matching`, `ERP integration for AP`) don't have
  pages to link to yet — they're inert cards with `{{PAGE_LINK_...}}` tokens rather
  than dead `<a>` hrefs, so nothing 404s if this ships before those pages exist.
- This archetype is explicitly not measured on demo requests (13-guide.md §Do not) —
  confirming that here so it doesn't get judged against the wrong metric: success is
  guide downloads + newsletter opt-ins feeding remarketing, not form-fills.

## System note

`/mockups/_system/tokens.css` did not exist before this build — see the authoring
note at the top of that file. `/mockups/_system/components.html` (the visual specimen
sheet 00-FOUNDATION.md §6 assigns to archetype 01) is still outstanding; nothing on
this page depends on it, but building 01 next would let it properly seed the shared
system instead of this page having done it as a side effect.
