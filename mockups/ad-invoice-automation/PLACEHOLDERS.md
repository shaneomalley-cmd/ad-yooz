# Placeholders — `/ad-invoice-automation` (archetype 05, Qualifier)

Every `{{TOKEN}}` used in `index.html`, what it needs, and who owns resolving it.

| Token | Where it's used | What's needed | Owner |
|---|---|---|---|
| `{{VOLUME_THRESHOLD}}` | H1, "not for you if" list, proof section | The actual minimum monthly supplier-invoice volume Yooz wants for this ad group. The brief suggests "500+" as an illustrative pattern but says explicitly to verify the real number before hard-coding it. This number also needs to match whatever volume the ad copy states — it's the single most load-bearing token on the page. | Growth / Sales ops (whoever owns ICP fit for this campaign) |
| `{{TEAM_SIZE_BAND}}` | Proof section | A real team-size range (e.g. "3–8") drawn from actual customer data for this segment. Not invented — see Claims discipline in `00-FOUNDATION.md`. | Sales ops / CS (existing customer AP team sizes) |
| `{{URL_AR_BILLING_REDIRECT}}` | "Not for you if" exit link (`data-yooz-event="qualifier-redirect-ar"`) | A real destination for AR/billing-seeking visitors. Yooz doesn't sell this — needs a decision on whether this points to an internal explainer page ("Yooz is AP, not AR — here's why") or an external resource. Do not point this at a competitor by name without legal/marketing sign-off. | Marketing / Legal |
| `{{AD_HEADLINE_1..3}}` | HTML comment block, top of file | The live RSA headlines for this ad group, for the copy team to confirm above-fold continuity against. | Paid media / copy team |
| `{{COMPANY_PHYSICAL_ADDRESS}}` | Footer | Yooz's registered business address for this locale (NORAM), required for the transparency/navigability QS requirement. | Legal / IT (whoever maintains the footer across the site) |

## Facts stated directly, not tokenized

Per `00-FOUNDATION.md` section 2, these two are verified brand-doc facts and are used
as plain text, not placeholders:

- "more than 250 financial systems" (Product section, Export stage)
- The multi-channel capture list — email, drag & drop, mobile, scan, sFTP,
  e-invoicing, fetcher, API (Product section, Capture stage)

## Explicitly not used on this page

No stat, customer name, logo, G2 rating, price, or competitor comparison appears
anywhere on this page. Per the archetype brief's "Proof that works here" section,
this page's proof is volume/team-size language and the disqualifier block itself —
not logos or awards — so none of those token categories were needed.
