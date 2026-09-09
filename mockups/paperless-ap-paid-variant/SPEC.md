# Light paid-variant spec — `/paperless-accounts-payable`

**Do not rebuild this page.** It ranks #1 organically for "paperless accounts
payable software" and works. Campaign 04 MODERNISATION + 04b AP PROCESS
AUTOMATION are budgeted $350–1,200/mo precisely because paid spend here is
mostly buying incremental reach around a page that already converts organic
visitors — not funding a redesign. This is the minimum change set to make
the existing page behave correctly as a *paid* destination for that traffic.

Head keywords it must serve: **accounts payable workflow software**, **ap
workflow software**, **cloud based accounts payable**, **digital accounts
payable**, **accounts payable cloud**, **automated ap processing**,
**accounts payable process automation**. Visitor is problem-aware but
frames it as an upgrade ("we're still on paper"), not a cost problem — the
competing alternative in their head is the status quo, not a competitor.

## 1. Query-echo H1 check

The page's organic-ranking H1 is presumably built around "paperless
accounts payable software," which is the term being dropped to a floor bid
— paying for a click Yooz already owns organically buys little. Five of the
seven paid head terms above share "accounts payable" + "cloud"/"digital";
two ("automated ap processing," "accounts payable process automation")
are automation-flavored and sit in tension with the brief's own
instruction to keep automation vocabulary out of the headline, since this
visitor hasn't adopted that word yet.

**Recommendation:** keep the H1 anchored on "accounts payable" +
"digital"/"cloud" (inflectionally covers 5 of 7 terms and matches the
visitor's actual mental model) rather than building query-parameter H1
swapping — that infrastructure isn't justified at this budget. Accept a
QS trade-off on the 04b ad group's two automation-flavored terms; if QS
underperforms specifically on that ad group after launch, revisit with a
templated swap then, not preemptively.

- [ ] Confirm current H1 wording against the above; adjust in place if it
      doesn't already contain "accounts payable" plus a cloud/digital term.

## 2. Ad-to-page continuity

- [ ] Add an HTML comment block at the top of the page template listing
      the exact live ad headlines for campaigns 04 and 04b, so the copy
      team can keep the above-fold promise in sync as ads are edited.
      No visible page change — process fix only.

## 3. Form placement

- [ ] Confirm the existing demo-request form sits within the first two
      mobile scroll screens. If it currently sits below a long before/after
      visual or implementation-timeline block, don't duplicate the full
      form above the fold — add a single anchor-linked CTA button in the
      hero that scrolls to the existing form. Keep the form itself once,
      at its current position.
- [ ] Secondary path (guide download) stays a tertiary text link, not a
      second full form.

## 4. Mobile above-fold audit

- [ ] H1 not truncated or overflowing at 390px viewport.
- [ ] A CTA (button or anchor link to the form) visible without scrolling.
- [ ] All tap targets ≥ 44×44px.
- [ ] No horizontal scroll introduced by any hero-visual change.

## 5. What NOT to touch

URL, information architecture, the organic-ranking copy blocks (before/after
visuals, six-stage process language, existing meta title/description —
these already rank #1, so only touch metadata if ad-to-page continuity
specifically requires it). No new sections, no new CTA, no redesign.

## What the mockup shows

`above-fold-mockup.html` is the hero-only recommendation from item 1 and
part of item 3 — a rewritten eyebrow + H1 + subhead that echoes the paid
head terms in the visitor's own "off paper" language, plus a CTA that
anchors down to the existing form rather than duplicating it. Everything
below the fold is unchanged and is not mocked up.
