# 01 — Brand

**Prerequisite: read `00-FOUNDATION.md` first.**
**Build this first regardless of the campaign build order — this page carries the design system every other page imports.**

## Pages
`/ad-yooz` (exists, rebuilding) and `/ad-yooz-vs` (new)

## Who lands here
Campaign 01 BRAND, ad groups: Yooz core, Yooz evaluation, Yooz vs competitor. Bid capped at $5 — this is the cheapest traffic in the account and already runs at 72% impression share.

Head keywords for the H1 echo: **yooz**, **yooz ap automation**, **yooz software**, **getyooz**. On `/ad-yooz-vs`: **yooz vs [competitor]**.

They already know Yooz. This is a navigational search or a final check before committing.

## The competing alternative in their head
Nothing — or, on `/ad-yooz-vs`, the single competitor they are checking against.

## What the first screen must do
**Get out of the way.** Product, a price signal, and a booking widget above the fold. That is the whole brief. This is the shortest page in the set and the only one where brevity is the conversion strategy.

## Section order
1. Hero + CTA
2. Short proof strip
3. Booking calendar
4. FAQ

## Proof that works here
Named customers, G2 badges, and a live calendar. Use `{{CUSTOMER_LOGO_1..6}}`, `{{G2_RATING}}`, `{{G2_REVIEW_COUNT}}`.

## Conversion
- **Primary:** demo booked. Use an embedded **calendar widget**, not a form — the visitor is ready and a form adds a step. Render as a placeholder block sized for a real scheduler embed, captioned `SCHEDULER EMBED — 3-column week view, 30-min slots`.
- **Secondary:** pricing conversation. A quiet text link, not a competing button.
- Form fallback (if scheduler fails to load): 5 fields.

## Do not
- Re-explain what AP automation is. They know. No "What is AP automation?" section, no category education, no problem-agitation copy.
- Bury the calendar below a long hero narrative.

## Brand composition
Primary layout — Pattern BG, Grey 10 content box, Rich Blue type, Pink CTA. This is the canonical expression of the brand, which is why the system is derived here. The reference website hero in the brand guidelines uses exactly this: large Light H1 in Rich Blue, Paragraph beneath, single Pink CTA, graded cutout hero image right-aligned with the Z anchored bottom-left.

## `/ad-yooz-vs` variant
Same brand hero treatment, then inherit the **archetype 10 (Displacement)** body: honest comparison table, one-line difference statement, migration path. Build this variant only after archetype 10 exists, then compose the two.

## Additional deliverable
This page also emits `/mockups/_system/tokens.css` and `/mockups/_system/components.html` per the Foundation output spec. Treat the specimen sheet as a real deliverable — every subsequent archetype depends on it being complete and correct.
