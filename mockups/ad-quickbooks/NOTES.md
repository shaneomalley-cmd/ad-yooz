# Build notes — /ad-quickbooks

## Design plan

Same composition as the other ERP pages (Primary → Blue form band), with
one structural addition: a "qualifier" callout directly under the hero
CTAs — a Pink-left-bordered Grey 10 box that names who this page is *not*
for, in one sentence, rather than just who it is for.

**Why it's placed there:** per 08-fit-erp.md's per-page note, QuickBooks
signals SMB intent more than any other ERP term, and NEG-03 (the
account's negative-keyword list) is applied hardest to this ad group.
Negative keywords stop the wrong query from triggering the ad; they can't
stop someone who searched a *legitimate* variant of "quickbooks ap
automation" but is, say, a two-person shop approving three bills a month.
The on-page qualifier is the complementary lever — it lets that visitor
self-select out before filling a 6-field form neither side wants
completed, rather than converting them into a lead sales has to
disqualify.

**ASCII wireframe, first screen (1440px):**

```
┌─────────────────────────────────────────────────────────┐
│ yooz                          The Lean Advantage  Pricing│
├─────────────────────────────────────────────────────────┤
│  Built for finance teams running QuickBooks Online/Desktop│
│  QuickBooks AP automation │ for teams processing real     │      ┌─────────────┐
│                             invoice volume.                │      │   Z-shape   │
│  See the exact fields that sync before you book a call.   │      │  hero image │
│  Yooz connects to QuickBooks Online and Desktop...         │      │  placeholder│
│  [Book a demo]  [See the connector →]                      │      └─────────────┘
│  ┃ Built for finance teams processing a meaningful volume  │
│  ┃ ...a QuickBooks bookkeeping app will serve you better.  │
│  ⟳ Exports to 250+ financial systems                       │
└─────────────────────────────────────────────────────────┘
```

## Checked against the archetype brief

- **Query echo:** H1 contains "QuickBooks AP automation" verbatim.
- **Per-page note — NEG-03 / volume qualifier:** addressed via the hero
  qualifier callout described above. This is a copy-side complement, not a
  substitute — NEG-03 itself is an ad-group-level negative-keyword setting
  outside this page's scope; flagging that separation so paid search
  doesn't assume the page build closes that ticket.
- **Do-not #1:** screenshots, sync table and capability block are
  QuickBooks-specific (class/location tracking, Online vs. Desktop
  parity, 1099 vendor flag) — not the NetSuite or SAP page with the name
  swapped.
- **Do-not #2:** no ERP × capability section built.
- **Capability block framing:** deliberately did not claim QuickBooks is
  "outgrown" in absolute terms — "Built to scale past QuickBooks' ceiling"
  describes Yooz's approval routing, not a claim about QuickBooks' own
  limitations that could read as disparaging a partner platform.

## QS checklist

1. **Query echo in H1** — "QuickBooks AP automation" verbatim.
2. **Title/meta** — title "QuickBooks AP Automation | Yooz" (33 chars);
   meta description ~135 chars, contains "QuickBooks AP automation."
3. **Ad-to-page continuity** — comment block with placeholder ad headline
   slots, plus an explicit NEG-03 note for the copy/paid-search team.
4. **Transparency/navigability** — standard header/footer.
5. **Mobile parity** — verified at 390px, zero non-table overflow. The
   qualifier callout stacks cleanly; the module card collapses to a column
   below 640px per the pattern established on ad-netsuite/ad-sap.
6. **Speed posture** — single file, ~15KB, no JS, no raster images.
7. **Accessibility floor** — one `<h1>`, semantic landmarks, skip link,
   scoped table headers, labelled fields, focus-visible via tokens.css.

## Conversion mechanics

Form stays 6 fields — the qualifier is a copy lever, not a field-count
lever. Reducing fields for this page specifically would work against the
self-selection goal (a shorter form lowers the bar for exactly the
under-threshold lead this page is trying to filter).

## Open questions

- Confirm with paid search that NEG-03's actual keyword list still needs
  applying at the ad-group level — this page assumes it isn't fully live
  yet, since the brief calls it out as something to apply, not something
  already done.
- Whether "a QuickBooks bookkeeping app will serve you better" is the
  right tone, or too blunt for a page that still wants the visitor's
  goodwill even if they don't convert — worth a copy-team read.
- No QuickBooks reference customer was supplied; customer block is fully
  tokenized pending one.
