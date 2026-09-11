# Build notes — `/ad-ap-automation-enterprise` (Archetype 02 — Enterprise variant)

## Rebuild note (structural only — copy unchanged)

Same rebuild as the parent `/ad-ap-automation` page (see its `NOTES.md`
for the full rationale): this file previously used a draft class/token
vocabulary (`.wrap`, `.box`, `.t-h1`, `.tone-blue`/`.tone-pink`,
`.section-kicker`, `material-symbols-outlined`, undefined custom
properties like `--fs-h3`) that predated and didn't match the real
`/mockups/_system/tokens.css`. Rebuilt against `ad-yooz/index.html` as
the reference: `.container`, `.box-grey10`/`--sm|md|lg`,
`.text-h1`–`.text-h5`/`.text-para`/`.text-para-lg`, an `<em>` for the
two-tone headline split, `.section-eyebrow` (fixing the same
number+label concatenation bug as the parent page), `.icon` + Material
Symbols **Rounded** (was Outlined), and the shared `.site-header`/
`.site-footer` chrome. No section copy, stats, quotes or form fields
were changed. Verified in-browser at 1440px/390px: no horizontal
overflow; the same environment-only Material Symbols ligature gap noted
on the parent page applies here too.

## Design plan

Per `02-solution.md`: "the same archetype with the proof swapped... Only
70/month of verified volume — build it as a light variant of the parent
page, not a separate design effort." This file is built by copying the
parent Solution page's structure and CSS verbatim (same tokens, same
section order, same `.hero`/`.steps`/`.cap-grid`/`.demo-grid` layout rules)
and changing only:

1. **H1 query echo** — "Accounts payable software for large business"
   instead of the parent's "AP automation software" (different head term,
   per the brief).
2. **Hero subhead/paragraph** — reframed around multi-entity/SSO/scale
   rather than the parent's general vendor-switch framing.
3. **3-step section copy** — same three grouped stages
   (Capture / Review & Approve / Pay & Export), sentences adjusted to
   mention entity-level routing instead of rewritten wholesale.
4. **Two of six capability-grid cards swapped** — "Multi-entity,
   multi-currency" and "SSO & role-based access" replace nothing from the
   parent's set of six per se; the parent's six were re-ordered so these
   two lead, since they're the enterprise-relevant differentiators. The
   AI-reading and multi-channel-capture cards were dropped to hold the
   grid at six cards rather than growing it — see "Open questions" below.
5. **Proof section (§5) replaced entirely** — the brief's explicit ask:
   multi-entity, volume thresholds, security/SSO, implementation
   resourcing. Built as a 4-up stat strip (entity count, volume threshold,
   security certification, implementation timeline) plus two customer
   quote cards (reduced from the parent's three, to make room for the stat
   strip without the section growing heavier than the parent's) plus one
   tertiary link to implementation detail.
6. **Demo form volume options** — raised to enterprise-appropriate bands
   (2,000–10,000 / 10,000–50,000 / 50,000+) instead of the parent's bands
   starting under 500, since a large-business visitor selecting "under 500"
   would be a mis-routed lead.

Everything else — header, footer, ERP logo strip, dot patterns, Z frame,
button system, form field styling, instrumentation pattern — is identical
to `/ad-ap-automation` by design, per "light variant, not a separate design
effort."

## QS checklist confirmation

Same as the parent page (see its `NOTES.md` for the full walkthrough); the
one substantive difference:

1. **Query echo in H1** — "accounts payable software for large business"
   appears verbatim in the Rich Blue clause. ✅
2. **Title / meta description** — title is the head term itself, 46 chars,
   verbatim, well under the 60-char limit. Meta description leads with
   "Accounts payable software for large business" framing and states
   multi-entity/SSO directly (real claims from the brief, not tokens) before
   the tokenized differentiator clause. ✅

Page weight: `index.html` ≈ 22KB, sharing the same ~12KB `tokens.css` as the
parent page and every other archetype (one cached fetch across the site).

## Open questions

1. Whether dropping the AI-reading and multi-channel-capture capability
   cards from this variant (to make room for the two enterprise cards
   without growing past six) loses something the enterprise buyer still
   needs to see, or whether it's correctly assumed they'll cross-reference
   the parent page. Flagging rather than deciding — a marketing call.
2. Whether two customer quotes plus a stat strip is enough proof density
   for an enterprise buyer, or whether the stat strip should expand to
   include a security-certification badge sourced from Legal before this
   ships (see `PLACEHOLDERS.md` — currently an explicit unverified token).
3. Demo-form volume bands assume "large business" starts around 2,000
   invoices/month — confirm against actual segment thresholds used
   elsewhere in the account (e.g. the enterprise-tier definition used in
   `content/ad-yooz.json` in the sibling template project, if one exists)
   rather than the number chosen here by inference from the brief.
