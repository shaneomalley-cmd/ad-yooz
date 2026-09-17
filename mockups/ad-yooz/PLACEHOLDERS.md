# Configuration — `/ad-yooz` (Archetype 01, Brand)

**Superseded 2026-09-17:** this page no longer uses `{{TOKEN}}` placeholders.
Every unresolved integration or time-sensitive claim is now gated behind
`landingPageConfig`, declared near the top of `index.html`'s `<body>`. A
component tied to an incomplete field renders nothing — not a placeholder,
not an empty card — until real values are supplied. Edit the config object,
not the markup, to bring a section live.

## Fields currently null/false, and what unlocks each one

| Config path | Unlocks | Owner |
|---|---|---|
| `booking.schedulerEnabled` / `schedulerEmbedUrl` / `schedulerProvider` | The embedded scheduler in the hero's booking widget, replacing the fallback form once it loads successfully. | Sales ops / RevOps |
| `booking.immediateCalendarInvite` | Swaps the booking microcopy to "Pick a slot and receive your calendar confirmation." Only set once the integration is tested to consistently deliver an immediate invite. | Sales ops |
| `booking.displaysAssignedSpecialist` / `supportsErpBasedAssignment` | Not currently used by any rendered copy — reserved per the brief's constraint that specialist-assignment or ERP-based-routing claims must never appear unless the scheduler itself implements them. | Sales ops |
| `booking.supportsPricingConversationTag` / `pricingConversationUrl` | Changes "Ask About Pricing" to "Talk Pricing Instead" and routes it to a dedicated pricing-conversation booking destination, on both the pricing section and the final CTA. | RevOps |
| `fallbackForm.portalId` / `formId` | HubSpot portal/form ID, if the fallback form becomes a HubSpot embed instead of the native form. | Marketing ops |
| `fallbackForm.submissionEndpoint` | A custom POST destination for the native fallback form. Until set, the form is fillable but submission is intentionally inert (see `index.html`'s submit handler) — it never claims success without a real destination. | Web/dev |
| `fallbackForm.privacyPolicyUrl` | Turns the plain-text "Yooz Privacy Policy" mention in the form's privacy notice into a real link. | Legal |
| `reviews.g2` / `reviews.capterra` (rating + reviewCount + verifiedDate + profileUrl, all four) | The G2/Capterra tiles in the proof strip and the Reviews section, plus the dynamic rating prefix on FAQ 3. All four fields must be present — a partial set stays hidden. | Marketing / review-platform owner |
| `reviews.trustRadius` / `gartnerPeerInsights` (enabled + profileUrl) | A neutral "View the Yooz listing" link in the Reviews section. These two never render a rating (the brief prohibits inventing one for either platform). | Marketing |
| `competitorComparison.enabled` / `url` | The optional sixth FAQ item comparing Yooz to other AP automation providers. Not part of the brief's example config object — added here since the brief describes the same gated pattern for this content. | Product marketing |
| `customerDestinations.loginUrl` / `supportUrl` / `helpCenterUrl` | The header's "Log in" link and the entire "Already a Yooz Customer?" section (hidden outright if all three stay null). | Customer success / IT |
| `media.heroImagePath` | Not currently wired to any layout — see NOTES.md "Open questions." No hero image slot exists in the markup today; adding one needs a layout decision for how it coexists with the booking widget in the hero's right column. | Design / brand |
| `media.demoVideoPath` / `demoVideoPosterPath` | A click-to-play product preview video in "What You'll See in the Demo" (poster-first, lazy, no autoplay, native controls on play). | Product marketing |
| `media.demoStillPaths` (used only if no video path) | Up to three annotated product stills in the same section. | Product marketing |
| `company.publicAddressConfirmed` / `publicAddress` | The footer's physical address line. Stays hidden, not placeholder text, until confirmed. | Legal / ops |

## Also still required, not part of `landingPageConfig`

- **Campaign 01 Brand RSA export** (current headlines/descriptions) — needed
  for the ad-to-page continuity comment at the top of `index.html`. Left as
  a developer-only `<!-- TODO -->`, not rendered.
- **Paid-landing-page indexing directive** — this project has no established
  rule for index/noindex on paid landing pages. Left as a developer-only
  `<!-- TODO -->` rather than assumed; no `<meta name="robots">` tag has
  been added.
- **Footer legal links** (`Privacy Policy`, `Terms`, `Contact`) currently
  point to `getyooz.com/privacy-policy`, `/terms`, `/contact` — carried
  over from the prior build, not newly re-verified in this pass. Confirm
  these are the correct live paths before launch.

## Verified facts used directly (not gated)

Per the brief, these are used as plain copy, not placeholders:
- "connections with more than 250 ERP and financial systems"
- "7,000+ customers, 600,000+ users" (hero subhead, as supplied)
- The named ERP/financial-system environments in FAQ 2 (Sage, Sage Intacct,
  NetSuite, Microsoft Dynamics, QuickBooks, Acumatica, CDK, Karmak, Tekion)
- The SOC 1 Type 2 and GDPR wording in FAQ 5, used exactly as supplied —
  do not edit this language without Security/Legal sign-off, since it was
  written specifically to avoid SOC 2 / ISO 27001 / certification claims
  the brief prohibits.
