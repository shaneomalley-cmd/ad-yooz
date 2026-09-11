# 00 — Foundation: Yooz paid-search landing page system

**Read this file before running any archetype prompt (01–13). Every archetype prompt assumes this file is in context.**

You are building HTML/CSS mockups of paid-search landing pages for Yooz, a NORAM AP (accounts payable) automation vendor. These pages are the destination for a 14-campaign Google Ads account. Their two jobs, in this order:

1. **Match the searcher's awareness stage** so Google's Landing Page Experience component of Quality Score improves. The account currently sits at QS 1–3 on head terms, which is gating eligibility to show at top of page at all, not just inflating CPC.
2. **Convert** the visitor on the action assigned to that archetype — which is *not* "book a demo" on every page.

Do not design a generic SaaS landing page 13 times. Each archetype exists because the visitor arrives with a different belief and a different competing alternative in mind.

---

## 1. Non-negotiable brand tokens

These come from the Yooz Branding Guidelines (Sept 2025). Do not substitute, "improve", or reinterpret the palette or typeface. The brand direction is already pinned; spend your design judgement on layout and hierarchy instead.

### Colour

```css
:root {
  /* Primary */
  --rich-blue: #14354E;   /* Pantone 534c — primary type, dark backgrounds */
  --pink:      #E0185E;   /* Pantone 205c — accent, CTA fills, dot patterns */

  /* Secondary — rare, primarily in gradients */
  --teal:      #00BFA5;
  --blue:      #006AFF;

  /* Neutrals — backgrounds and strokes only, never the primary focus */
  --grey-100:  #3C4857;
  --grey-90:   #46515E;
  --grey-80:   #616C7A;
  --grey-70:   #A0A7AF;
  --grey-60:   #CCCDD2;
  --grey-50:   #DEDEE0;
  --grey-40:   #E6E6E6;
  --grey-30:   #EAEAEA;
  --grey-20:   #F5F5F5;
  --grey-10:   #FEFEFE;
}
```

**Colour hierarchy — 60/30/10.** 60% background, 30% type, 10% accent. Within the 10%, lean on Pink; secondaries appear mainly inside gradients.

**Accessibility, as tested by the brand team:**
- Rich Blue on Grey 10 = 12.63:1 → AAA. This is the default text pairing for almost everything.
- Pink on Grey 10 = 4.67:1 → passes AA for normal text, AAA for large. **Never use Pink for body copy, small labels, or dense table text.** Pink is for CTA fills, large display type, icon fills, dot patterns and accent rules.
- Grey 10 text on a Pink fill inherits the same 4.67:1. Fine for a button label at 17px semibold; not fine for 12px legal text.

**Gradients** are accents that complement hero photography. A gradient must always include Pink, balanced with Rich Blue, then optionally one secondary (Teal or Blue). Never a gradient of the greys, never a gradient as a decorative wash behind body content.

### Typography

Noto Sans only — Light 300 (headings), Regular 400 (body), SemiBold 600 (links, highlights, CTA). Load from Google Fonts.

| Role | Size | Line-height | Letter-spacing | Weight |
|---|---|---|---|---|
| Display | 120px | 90% | -2% | Light |
| Heading 1 | 84px | 110% | -2% | Light |
| Heading 2 | 64px | 100% | -2% | Light |
| Heading 3 | 48px | 110% | -2% | Light |
| Heading 4 | 32px | 120% | -2% | Light |
| Heading 5 | 24px | 120% | -2% | Light |
| Paragraph Large | 22px | 150% | -2% | Light |
| Paragraph | 17px | 150% | -1% | Regular |
| List item | 16px | 150% | -2% | Light |
| Paragraph Small bold | 16px | 100% | -1% | SemiBold |
| Tagline | 14px | 150% | -2% | Light |
| Call to action | 17px | 150% | 0% | SemiBold |

Two deliberate departures you should make, and flag in your build notes:

- **Light weight below 24px is a legibility risk.** Where the brand scale specifies Light for a 16px list item, use Light only on Grey 10/20 backgrounds at Rich Blue. Inside comparison tables, spec grids, migration timelines and any dense data block, step up to Regular 400. A skeptical CFO scanning a 6-row comparison table should not be squinting.
- **Display at 120px and H1 at 84px do not fit a mobile viewport.** Build a fluid scale: `clamp()` from roughly 40px (390px viewport) to the brand size at 1440px+, holding the -2% tracking and the stated line-heights throughout.

### 2b. Type hierarchy and buttons — the brand's own composed patterns

The guidelines include a Type hierarchy page specifying how these styles assemble. Follow it; it overrides generic landing-page instinct.

**Hero section, top to bottom:**
1. **Eyebrow** — Pink, SemiBold, small, **sentence case** (e.g. "Discover Financial Operations Automation for ambitious companies"). Not all caps, not tracked out.
2. **H1, two-tone.** The first clause in Rich Blue, the continuation in Pink. This is the signature Yooz headline treatment and it recurs across every applied asset — social, ebook covers, webinar cards, in-page section heads. The split must fall on a natural clause boundary, so the Pink carries the part of the sentence that matters. Some pages use a single-tone Rich Blue H1 (the getyooz.com homepage does); that is also correct, and is the right choice when the headline is a query echo that shouldn't be visually broken.
3. **H4** as the supporting subhead, Rich Blue Light.
4. **Paragraph** in Rich Blue Regular.
5. **Buttons.**

**In-page section pattern:** eyebrow as a number plus a label in a Grey 10 pill (e.g. `04` + "The breakthrough") → H2 → Paragraph → list items with Pink bullet markers → tertiary button.

**Button system — build all three into the specimen sheet:**

| Level | Treatment | Use |
|---|---|---|
| Primary | Pink fill, Grey 10 label, 17px SemiBold, rounded | The page's conversion action |
| Secondary | Grey 10 fill, Pink label, thin Pink border | The alternate action alongside a primary |
| Tertiary | Text link in Pink SemiBold with a trailing arrow glyph | Low-commitment in-page links ("Read our growth-focussed mini-eBook →") |

The trailing arrow is brand practice on secondary and tertiary buttons and appears throughout the applied assets. **Keep the primary CTA label arrow-free** — a demo-booking button should read as a commitment, not a nudge — but use the arrow on tertiary links as the brand does.

**Brand vocabulary you may use directly:** *Lean Financial Operations™* is a trademarked Yooz term and *The Lean Advantage* is a top-level nav item; both appear on published assets including the CFO ebook covers. `Pricing` is also a real top-level nav item, which matters for archetype 1's price signal and archetype 12.

### Layout system — container, grid and spacing

The brand book covers colour, type and composition but not measurements. These are specified here so every page uses the same ones. Put all of them in `tokens.css` as custom properties; never hard-code a pixel value in a page.

```css
:root {
  /* Container */
  --container-max: 1200px;   /* content never exceeds this */
  --gutter: 24px;            /* 390px viewport */
  --gutter-md: 40px;         /* 768px+ */
  --gutter-lg: 64px;         /* 1200px+ */

  /* Spacing scale — use these, not arbitrary values */
  --space-1: 4px;   --space-2: 8px;   --space-3: 16px;
  --space-4: 24px;  --space-5: 40px;  --space-6: 64px;
  --space-7: 96px;  --space-8: 128px;

  /* Vertical rhythm */
  --section-y: var(--space-7);      /* between major sections */
  --section-y-lg: var(--space-8);   /* around hero and final CTA */

  /* Geometry */
  --radius-box: 16px;    /* Grey 10 bounding boxes */
  --radius-button: 999px; /* buttons are fully rounded, per brand assets */
  --border-hairline: 1px solid var(--grey-50);
}
```

**Every section wraps its content in a container** — `max-width: var(--container-max)`, `margin-inline: auto`, `padding-inline: var(--gutter)`. Full-bleed backgrounds are fine and often correct (a Rich Blue panel should span the viewport); the *content inside them* must not. A headline starting at x=0 against the browser edge is the single most visible sign the layout is broken.

**Grid:** 12 columns at 1200px+, 8 at 768px, 4 at 390px, `gap: var(--space-4)`. Capability grids are 3-up at desktop, 2-up at tablet, 1-up at mobile.

**Eyebrow spacing:** where the in-page eyebrow is a number plus a label (`04` + "The breakthrough"), they are two separate elements with `var(--space-2)` between them. Rendering as `04The breakthrough` means they were concatenated in markup — don't.

**Form fields** need visible labels above the input in Paragraph Small bold, not placeholder-only fields. On a Rich Blue panel, labels are Grey 10. A form of blank white boxes with no labels is not a form.

### Layout patterns

The brand defines three page compositions. Each archetype prompt names which to use.

| | Primary layout | Inframe layout | Blue layout |
|---|---|---|---|
| Page background | Pattern BG | Pattern BG | Pattern BG |
| Content box | Grey 10 | Grey 10 (contained) | Rich Blue |
| Type | Rich Blue | Rich Blue | Grey 10 |
| CTA | Pink | Pink | Pink |

**Dot patterns** (build as CSS `radial-gradient` or an inline SVG `<pattern>`, not a raster image):
- *Pattern BG* — Grey 20 background, Pink dots at 40% opacity, 600% spacing. General page backgrounds.
- *Pattern Pink* — Grey 10 background, Pink dots at 100%, 400% spacing. Single-strip content callouts.
- *Pattern Blue* — Rich Blue background, Grey 80 dots at 100%, 600% spacing. Rich Blue background elements.

**The Z shape** is Yooz's signature device — the mark represents stacked invoices. In hero imagery the Z is anchored bottom-left with the subject cut out and extruding beyond the frame, facing inward toward the copy. In secondary imagery the Z sits top-right with a darker Rich Blue wash over the image top so the pink gradient map reads more strongly. Keep the aspect ratios consistent; do not rotate or reflect it arbitrarily.

**Icons:** Material Symbols (Google Fonts). No mixed icon sets.

### Imagery — placeholder policy

Yooz hero photography is graded (desaturate → exposure/curves → pink-to-teal gradient map → subtle noise) and cut out against the Z. You cannot produce that in a mockup and should not try to approximate it with stock photos or CSS filters on random images.

Instead, render every image slot as a **labelled placeholder**: the correct Z geometry and gradient, filled with a flat Rich Blue→Pink gradient, plus a caption in Tagline style naming what belongs there — e.g. `HERO — graded cutout, subject facing inward, Z anchored bottom-left`. Same for product screenshots: a correctly-proportioned frame captioned `SCREENSHOT — invoice approval queue, parallel approval visible`. This makes the mockup honest about what still needs asset production, and reviewable without pretending the assets exist.

---

## 2. Claims discipline — read this twice

**Never invent a statistic, customer name, logo, award, analyst position, rating, price or capability.** Yooz operates in finance software where every comparative claim is legally substantiable or a liability. A mockup full of plausible fabricated numbers is worse than useless because it will get copied into production.

Use double-brace placeholder tokens with a descriptive name, and collect every one you use into a `PLACEHOLDERS.md` manifest alongside the page:

```
{{STAT_PROCESSING_TIME_REDUCTION}}   — brand doc references "up to 80%", needs re-substantiation
{{CUSTOMER_NAME_MANUFACTURING}}
{{CUSTOMER_LOGO_SAGE_1..5}}
{{G2_RATING}} {{G2_REVIEW_COUNT}}
{{PRICE_PER_INVOICE_BENCHMARK}}
{{ERP_CONNECTOR_SYNC_FIELDS}}
{{COMPETITOR_FEATURE_TIPALTI_ROW_3}}
```

Two verified facts you may state directly, both from the brand guidelines: Yooz exports to **more than 250 financial systems**, and multi-channel capture covers **email, drag & drop, mobile, scan, sFTP, e-invoicing, fetcher and API**. Everything else is a token.

The six-stage Yooz process vocabulary — **Purchase → Capture → Review → Approve → Pay → Export** — is brand-approved and should be reused wherever a "how it works" section appears, rather than inventing new step names.

---

## 3. Global Quality Score requirements

Landing Page Experience is one of three QS components, alongside Expected CTR and Ad Relevance. Every page must satisfy all of the following, and your build notes must confirm each:

1. **Query echo in the H1.** The H1 contains the ad group's head keyword verbatim or with only inflectional change. Each archetype prompt lists the exact terms. This is the single highest-leverage QS lever and it is also why some of these headlines will feel blunter than a brand headline would be.
2. **`<title>` and meta description** both contain the head keyword. Title ≤ 60 chars, description ≤ 155.
3. **Ad-to-page continuity.** The above-fold copy restates the promise the ad made. Leave a comment block at the top of the file listing the ad headlines this page must stay consistent with, for the copy team to fill.
4. **Transparency and navigability.** A persistent header with the Yooz wordmark linking to `getyooz.com`, and a footer carrying links to Privacy Policy, Terms, Contact, and a physical business address placeholder. Google penalises pages that look like orphaned funnels. No exit interstitials, no scroll-jacking, no auto-playing audio.
5. **Mobile parity.** Everything above the fold on desktop must be reachable in the first two mobile screens. Tap targets ≥ 44×44px. No horizontal scroll at 390px. Comparison tables become either a stacked card list or a horizontally-scrollable region with a visible affordance and a sticky first column — never a squashed 6-column grid.
6. **Speed posture.** Self-contained single file, system-safe font loading with `font-display: swap`, no libraries beyond what the page genuinely needs, all decorative geometry as inline SVG or CSS. Note the page's weight in the build notes.
7. **Accessibility floor.** Semantic landmarks, one `<h1>`, visible keyboard focus states (Pink 2px outline with 2px offset), `prefers-reduced-motion` respected, all form inputs labelled, all placeholder images with descriptive `alt`.

---

## 4. Conversion mechanics

**Form length scales with awareness — do not use one form everywhere.**

| Awareness | Archetypes | Fields |
|---|---|---|
| Late / high intent | 1, 2, 7, 8, 9, 10 | 5–6 (work email, first, last, company, ERP or invoice volume, phone optional) |
| Mid | 3, 6, 11 | 3–4 |
| Low / exploratory | 4, 5, 12, 13 | Email only |

Every extra field on a low-awareness page costs more than the data is worth.

**One primary CTA per screen.** The only exception is archetype 4, where two competing paths are the entire point.

**CTA copy states what happens.** "Book a demo", "Calculate your cost per invoice", "Download the comparison". Never "Submit", never "Learn more". Arrow glyphs follow the button system in section 2b: none on the primary, allowed on secondary and tertiary.

**Instrumentation.** Give every CTA, form and path-choice a stable `data-yooz-event="..."` attribute so conversion tracking and the offline import can be wired without re-editing markup later. Note in the build notes which of these should be a primary conversion action versus a lower-value secondary one, per the archetype's brief.

---

## 5. Design guardrails

The brand pins the palette and typeface, which removes most of the axes where generated pages tend to converge on the same look. Spend the remaining freedom deliberately, and avoid these specific tells:

- Eyebrow labels are part of the brand system, so use them — but exactly as specified in section 2b, in sentence case. No tracked-out ALL-CAPS.
- The two-tone headline is brand-correct and should be used (see section 2b), but the split falls on a clause, never on one decorative word, and never mid-phrase for emphasis alone.
- Do not chop every section into identical rounded cards with the same radius and the same soft grey shadow. The brand's structural device is the Grey 10 bounding box on a patterned ground — use *that*, and vary its size and inset according to the content's importance.
- Numbered markers (01/02/03) only where the content is genuinely a sequence. Purchase→Capture→Review→Approve→Pay→Export is a sequence. A list of capabilities is not.
- Structural devices — rules, borders, insets, the Z — should encode information, not decorate. A hairline rule that separates two arguments is doing work; one under every heading is not.
- Motion: one deliberate moment per page at most, and only where it shows something changed (a path opening, a calculator result appearing, a table column highlighting). No fade-and-slide-up on every section, no hover transform on every card.
- Line length under 80 characters for body copy.

Work in two passes. First write a short plan — layout concept, which brand composition you're using, an ASCII wireframe of the first screen, and the section order. Check that plan against the archetype's "First screen must do" and "Do not" lines. Only then write code.

---

## 6. Output specification

For each archetype, produce:

```
/mockups/<page-slug>/
  index.html          # self-contained: inline <style>, inline SVG, no build step
  PLACEHOLDERS.md     # every {{TOKEN}} used, with a note on what's needed and who owns it
  NOTES.md            # design plan, QS checklist confirmation, page weight,
                      # open questions, and any place you departed from the brief
```

**Stack:** plain HTML + CSS in a single file. No framework, no Tailwind CDN, no build step. Reviewers need to open the file and see the page; developers need to read the CSS and port it into whatever the production CMS is. Use CSS custom properties for every token so a port is mechanical.

**Breakpoints:** design at 1440px, verify at 1024px, 768px and 390px.

**Concurrency — `_system` is read-only after archetype 01.** These pages are often built in parallel sessions. Once `/mockups/_system/tokens.css` and `components.html` exist, treat them as frozen: import them, never edit them. If you believe a token is wrong or a component is missing, record it in your page's `NOTES.md` as a proposed system change and work around it locally. Editing the shared files mid-run silently breaks every page already built, and the person running these cannot see your session to catch it.

**Shared assets:** the first page you build (archetype 01, Brand) also emits `/mockups/_system/tokens.css` and `/mockups/_system/components.html` — a live specimen sheet containing the type scale, the three dot patterns, the Z geometry, button states, form fields, the Grey 10 bounding box at three scales, and the header/footer. Every later page imports `tokens.css` and reuses those components rather than re-deriving them.

**What is shared and what is not:** the design system is shared across all 13 archetypes. The page skeleton is not. Archetypes 3, 4, 5, 11 and 12 have structurally different first screens — a four-option comparison, a two-path chooser, a disqualifier, a multi-vendor table and a calculator. None of those can inherit a hero-plus-demo-form layout without losing the thing that makes them convert. Let the first screen vary; keep the tokens, components and footer identical.
