# Yooz paid-campaign landing page template

Deliverable for: replacing `/en-us/ad-yooz` and establishing a shared, parameterized
template for the ERP (`ad-sage`, `ad-epicor`, `ad-dynamics`, `ad-cdk`, `ad-karmak`,
`ad-procede`) and industry-vertical (construction, automotive, trucking) variants.

Live preview of the template: **https://claude.ai/code/artifact/7c518349-bc76-4005-bb7a-4864b4c4d11a**

---

## Step 0 — What's actually running the site

**Access note:** this session has no WordPress admin/SFTP/DB access and no outbound
network access to `getyooz.com` (confirmed blocked at the environment's network-egress
policy — even a fetch to `example.com` was blocked). The findings below come from the
full page source of `/en-us/ad-yooz` that was pasted into this conversation, not a live
crawl. `/en-us/ad-sage` was **not** inspected — see `content/ad-sage.example.json` for
what that means for the Sage instance.

### Stack
- **WordPress**, theme = **Bricks Builder** (`wp-theme-bricks`) with a child theme
  (`wp-child-theme-custom-theme`), styled by an agency-built layer the CSS calls
  `agencepardos` and a custom "S2" component library (`.s2-nav-*`, `.s2-header-*`,
  `.s2-demo-talk`, etc.) for header/nav and a few marketing patterns.
- **SEO**: Rank Math PRO generates title/meta/canonical/OG/Twitter tags and the only
  JSON-LD currently on the page — a single `BreadcrumbList`. No `Organization` or
  `SoftwareApplication` schema exists today.
- **Performance**: FlyingPress (full-page cache, critical-CSS inlining, deferred
  non-critical CSS via the `media="print"` swap trick, deferred JS) + Perfmatters
  (image lazy-load via `data-src` with dimensions preserved, and — notably — the demo
  video is **already** a click-to-load YouTube facade: a static thumbnail + play button,
  iframe injected only on click). Noto Sans is **already** self-hosted as a variable
  font with `fetchpriority="high"` preloads. This is a better starting point than the
  brief assumed on video/LCP and font-loading; the template below preserves both
  patterns rather than reinventing them.
- **Multi-language**: Polylang (`en-us`, `en-gb`, `es`, `fr` — matches the four
  BrightEdge accounts visible to this session).
- **Content type**: the page is a post of a **custom post type called `sea`**
  (Search Engine Advertising) — `postid-18941`, `single-sea`. Every stat, heading, and
  paragraph is typed directly into Bricks elements on that one post. There is **no ACF
  or repeatable-field layer today** — this is exactly the "hand-copied structure"
  described in the brief, confirmed at the source level.
- **HubSpot form**: embedded via `hbspt.forms.create({ portalId: "2205679", formId:
  "1b3ffee0-1aa1-4f18-9073-db1d433a3dff", target: "#hubspot-form-6a97d3ee9e847" })`,
  loaded from `js.hsforms.net/forms/embed/v2.js` (deferred). Wrapped in custom JS that
  adds a company-name autocomplete against a French/EU business registry (Pappers) for
  European locales — a harmless no-op on the US page since country resolution returns
  empty for `en-US`. "Request a Demo" buttons elsewhere on the page don't open a second
  form — they're anchor links back to this one embed (`href="#hsForm_...`). On submit,
  it redirects to the same URL with `?hubspot_redirect=1`.
- **Analytics**: Google Tag Manager loaded through the first-party subdomain
  `svsd.getyooz.com` exactly as the brief requires — **do not touch this.** Also present
  but out of scope to remove without confirming with marketing/IT: the HubSpot tracking
  script (`js.hs-scripts.com`, required for the form/CRM to function), a Cloudflare Web
  Analytics beacon, an obfuscated third-party loader, and `files.webyn.ai` (appears to
  be a chat/agent widget, already deferred behind Perfmatters' interaction-based delay).
  None of these were added by this work and none should be.
- **Cookie consent**: Didomi (`sdk.privacy-center.org`), with HubSpot's own cookie
  banner explicitly disabled (`window.disableHubSpotCookieBanner = true`) so Didomi is
  the single consent surface. Didomi's actual on-page position/z-index is configured in
  Didomi's own dashboard, not visible in page source — **cannot be verified from source
  alone,** see checklist.

### Does the current setup support parameterization cleanly?
Not today, but the smallest change gets there without a platform change:

1. **Add one ACF field group to the `sea` post type** (schema in
   `template/acf-field-group-sea-landing-page.json`, importable as-is via ACF's
   "Import Field Group" JSON feature) covering every field the brief asks for:
   `primary_keyword_phrase`, `segment_name`, `hero_stat`, `integration_logos`,
   `proof_testimonial`, benefit statements, the fraud module, etc.
2. **Add one ACF Options page** (`acf-options-shared-stats`) for the numbers that must
   never drift between pages or between a page and its ad copy: `customer_count`,
   `erp_count`, the headline cost-reduction stat, and the problem-section pain-point
   stats. Every `sea` post reads these instead of hardcoding them. **This is the fix for
   the "600,000 users vs. 7,000 customers" drift** — there becomes exactly one field to
   edit, and if the ad-copy generation process is pointed at the same options page (or
   an API/export of it), the page and the ads can no longer disagree.
3. **Rebuild the Bricks content once, using Bricks' native ACF dynamic-data tags**
   (e.g. `{acf_hero_stat_value}`) instead of hardcoded text nodes, and assign that
   Bricks template as the default template for the `sea` post type (or via Bricks'
   template-condition system). Every existing and future `sea` post — `ad-yooz`,
   `ad-sage`, `ad-epicor`, the vertical pages — then renders from the *same* template
   with different field values, which is the actual fix for "one hand-copied structure."

This session has no WP admin/Bricks-editor access, so step 3 could not be performed
directly. What's delivered instead: the ACF schema (a real, importable artifact), and a
full HTML/CSS/JS reference build of the redesigned template with every dynamic field
marked, so it can be translated into Bricks elements section-by-section, or the CSS
reused close to verbatim (it's written against the theme's own custom properties —
`var(--primary)`, `var(--base)`, etc.).

---

## Design decisions worth flagging

- **Single-theme, no dark-mode variant.** This is a locked paid-media brand system —
  the same page needs to render identically regardless of OS theme so ads and landing
  pages stay visually consistent — so colors are painted explicitly rather than
  remapped for `prefers-color-scheme`, matching how the live site itself behaves today.
- **Button radius**: the brand guideline calls for a fully pill-rounded primary button;
  the live theme's default `.bricks-button` uses `border-radius:6px`. The template CSS
  overrides this for the primary CTA only (scoped class, not a global theme edit) —
  flagging in case a site-wide button-radius change is actually wanted instead.
- **Body font weight**: current theme sets body copy to Noto Sans weight 300 (same as
  headings); the brand guideline specifies body = Regular (400). Template uses 400 for
  body per the written guideline — a deliberate refinement, called out here rather than
  silently changed.
- **CTA count**: the live page currently has three "Request a Demo" touchpoints (hero
  form + two anchor buttons). The brief caps this at "one CTA action, repeated at most
  once more." The template keeps the hero form as the one true action and **one**
  repeated button at the final CTA; the old mid-page "Request a Demo" button in the
  Problem section is removed (no replacement CTA there — the stats and calculator carry
  that section).
- **Fraud-guide CTA style**: brand guideline explicitly assigns whitepaper-style,
  lower-commitment downloads to the tertiary (pink text + arrow) style, not the primary
  pill button the live page currently uses there. Template follows the written
  guideline over the current implementation.
- **Superlatives removed**: three lines on the live page violate the brief's own "no
  unsupported superlatives" rule and were rewritten rather than carried forward:
  - Meta description: *"the most powerful AP Automation software on the market"* → cut,
    kept the two verified numbers (80% cost cut, 250+ ERPs).
  - Client-logos band: *"the #1 AP Automation Service Provider"* → rewritten to
    *"Join Clients Across Construction, Automotive, Trucking, and Beyond Who Run AP on
    Yooz"* (a true claim tied to the existing logo grid).
  - Benefit block: *"the only all-in-one finance automation platform"* → removed; that
    whole block of five benefit statements (Ultimate Protection / Infinitely Adaptable /
    Redefined Simplicity / Client Obsessed / Highest Return) was adjective-driven and
    didn't meet requirement 7 ("concrete, NOT vague adjectives"), so it was rewritten to
    five claims that each cite a fact established elsewhere on the same page (see
    `content/ad-yooz.json` → `_benefit_statements_note`).
  - Restore any of these as specific ranking claims only if you have a citable source
    (e.g. a named G2 category-leader badge) — the template doesn't invent one.
- **New security/compliance badge row** (requirement 9): no SOC 2 or GDPR badge/asset
  exists anywhere in the fetched page source. Rather than publish a plausible-looking
  badge, the template renders this row in an explicit "unverified" visual state
  (dashed border, `[VERIFY: ...]` label) so it can't accidentally ship as a real claim
  before Legal/Security confirms current certification status.

---

## Files in this delivery

- `template/ad-yooz-landing-template.html` — full reference build, brand-compliant,
  populated with the real ad-yooz content. Also published as a live Artifact (link at
  top of this file) for visual review.
- `template/acf-field-group-sea-landing-page.json` — importable ACF schema (two field
  groups: per-page content on `sea`, and the shared-stats Options page).
- `content/ad-yooz.json` — populated content instance for the general/brand page,
  matching the ACF schema field-for-field.
- `content/ad-sage.example.json` — **illustrative only**, not fetched from the live
  `/en-us/ad-sage` page (out of scope this pass, see Step 0 access note above). Shows
  how the same template renders a second, ERP-scoped instance, with every Sage-specific
  number marked `[VERIFY]` rather than guessed.
- `CHECKLIST.md` — technical checklist: what changed structurally vs. what needs a
  manual PageSpeed Insights / CrUX check on the live, deployed page.
