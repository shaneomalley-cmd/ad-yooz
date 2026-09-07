# Technical checklist

Per the brief's requirement to separate what was actually changed from what still needs
a manual Core Web Vitals check against live field data (PageSpeed Insights / CrUX) —
this session had no way to run either against the live site (see README Step 0 access
note), so nothing below marked "manual check" has been verified live.

## Structural changes made in this delivery

- [x] **JSON-LD added**: `Organization` + `SoftwareApplication` (+ kept the existing
  `BreadcrumbList`). The live page had only the breadcrumb. No `aggregateRating` /
  review schema added — no confirmed numeric rating was found in the fetched source;
  adding one would need the exact current score from each review platform.
- [x] **Video stays a lazy facade**: static thumbnail + play button; the real `<iframe>`
  is only created on click. This matches the pattern already live (Perfmatters), not a
  new technique — kept, not rebuilt.
- [x] **CLS space reserved for the HubSpot form**: `.form-card` has a fixed
  `min-height:520px` before the form renders, sized for the actual field set (first/last
  name, email, company, phone, country, submit) — larger than the live theme's existing
  `min-height:400px` reservation on the equivalent element, which is tight for the full
  field set once it stacks on mobile.
- [x] **Single CTA action**: reduced from three "Request a Demo" touchpoints on the live
  page to two (hero form + one repeat at the final section), per requirement 3's "at
  most once more" cap. See README "Design decisions."
- [x] **Mobile-first responsive layout**: hero collapses from two columns to one at
  900px; H1, subhead, and the demo-form card are all in normal document flow above any
  `100vh`-style trap, so they're visible without scrolling on a standard mobile viewport
  once the actual page (with a real header/nav) is assembled — **verify this specific
  claim once assembled in Bricks with the real header height**, see manual checks below.
- [x] **Tap targets**: primary CTA button is 52px min-height; form fields sized to
  50px; footer/social icons sized to real touch-target minimums.
- [x] **Analytics untouched**: no new client-side tag added; `svsd.getyooz.com`
  first-party GTM path is the only analytics mechanism referenced in the template.
- [x] **Superlative language audited**: three unsupported superlatives found and
  rewritten (see README). Every stat retained is one already present on the live page;
  everything not already confirmed is marked `[VERIFY]` rather than invented.
- [x] **Security/compliance badge row added** (was missing entirely) — in an explicit
  unverified visual state pending real SOC 2 / GDPR confirmation, not a placeholder that
  could accidentally ship as a real claim.
- [x] **Brand system applied**: Noto Sans (Light headings / Regular body / Semibold
  UI), Material Symbols Rounded, Rich Blue / Pink / Grey10 / Grey20 60-30-10 palette,
  pink pill primary button (single style), pink-text-plus-arrow tertiary link for the
  whitepaper download, hero eyebrow + split-weight H1 pattern, and a zero-image-weight
  inline-CSS "Z" device anchored bottom-left of the hero (no photography asset needed,
  so it costs nothing toward LCP/byte-weight — this is the resolution to the brief's own
  flagged tension between the signature device and performance).
- [x] **Fonts loaded from Google Fonts** (`fonts.googleapis.com` → `fonts.gstatic.com`),
  not the live site's self-hosted woff2 files — **when implementing in Bricks, keep the
  live site's existing self-hosted/preloaded Noto Sans setup instead of switching to the
  Google Fonts CDN** — self-hosting with `fetchpriority="high"` preloads (as the live
  page already does) is strictly better for LCP than an external font host. This
  template uses Google Fonts only because that's the one stylesheet host this
  preview environment's CSP allows.

## Needs a manual check on the real, deployed page (cannot be verified from here)

- [ ] **PageSpeed Insights / CrUX** run on the actual deployed `/en-us/ad-yooz` after
  the rebuild — LCP, CLS, INP, and total byte weight, both mobile and desktop. This
  session has no live-site or network access at all, so none of these numbers exist yet
  for the new template.
- [ ] **Didomi cookie-banner placement on real mobile devices.** Didomi's on-page
  position/z-index is configured in Didomi's own dashboard, not in page source, so it
  could not be inspected. Load the real page on an actual small-viewport device (not
  just a resized desktop browser) and confirm the banner docks at the bottom without
  covering the H1 or the demo-form card on first load.
- [ ] **Real HubSpot form height** once live: the `min-height:520px` reservation here is
  sized from the field list implied by the custom Pappers-autocomplete JS
  (name/email/company/phone/country + hidden fields). Confirm against the actual
  rendered form — if HubSpot adds a consent checkbox, error-state text, or an extra
  field, the reserved height may need to increase, or CLS will reappear.
- [ ] **Font-loading strategy**: confirm the final Bricks implementation keeps the
  existing self-hosted Noto Sans + preload approach (see note above) rather than the
  Google Fonts link used in this preview build.
- [ ] **Third-party script audit**: confirm with marketing/IT whether the obfuscated
  loader script and `files.webyn.ai` widget seen in the live source are still wanted;
  neither was touched here, but the brief's "don't regress performance" goal is worth
  revisiting them against, given they add to total byte weight independent of anything
  in this template.
- [ ] **Existing site favicon / apple-touch-icon** — unaffected by this template, not
  re-verified.
- [ ] **Accessibility pass** (axe/Lighthouse) on the assembled Bricks page — this
  reference build uses semantic headings, `aria-label`s, and visible focus states, but a
  full audit needs the real, final markup once translated into Bricks elements.
- [ ] **Cross-browser/OS check** of the pill-button and font-weight overrides described
  in README "Design decisions," since they deliberately diverge from the current theme
  defaults.
