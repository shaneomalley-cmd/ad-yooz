# Placeholders — `/ad-ap-roi` (Archetype 12, Calculator)

Every `{{TOKEN}}` used in `index.html`. Per Foundation §2, no statistic,
customer name, logo, award, analyst position, rating, price or capability
is invented. This page is unusual among the archetypes: its whole point
is a *working* calculator, so its five coefficients live as real numbers
inside the script's `CONFIG` object rather than as literal `{{TOKEN}}`
text in the HTML — but every one of those numbers is visibly labelled
"illustrative placeholder" in the on-page "Show the assumptions"
disclosure, alongside its token name, so nothing here is presented to a
visitor as a real published figure.

| Token | What it needs | Owner |
|---|---|---|
| `{{BENCHMARK_COST_PER_INVOICE_MANUAL}}` | A real, citable published benchmark for manual cost per invoice (currently a $15.00 illustrative placeholder in `CONFIG.benchmarkCostPerInvoiceManual`). Substituted for the "I don't know" toggle and shown as a comparison figure. | Product marketing / finance benchmarking |
| `{{BENCHMARK_COST_PER_INVOICE_AUTOMATED}}` | A real, citable published benchmark for automated cost per invoice (currently $3.50 placeholder in `CONFIG.benchmarkCostPerInvoiceAutomated`). Comparison-only; not used in the arithmetic. | Product marketing / finance benchmarking |
| `{{BENCHMARK_TOUCHES_PER_INVOICE}}` | A real, citable published benchmark for average manual touches per invoice (currently 3, placeholder in `CONFIG.benchmarkTouchesPerInvoice`). Narrative context only. | Product marketing / finance benchmarking |
| `{{ASSUMED_TIME_SAVING_PCT}}` | The percentage reduction in cost/cycle-time automation is modelled to deliver (currently 60%, placeholder in `CONFIG.assumedTimeSavingPct`). This is Yooz's own modelling assumption, not a third-party citation — needs product-marketing sign-off against real customer outcome data before publishing. | Product marketing / customer success |
| `{{ASSUMED_IMPLEMENTATION_COST}}` | A one-time switching/implementation cost assumption used only to model payback period (currently $15,000, placeholder in `CONFIG.assumedImplementationCost`). Added beyond the brief's four named coefficients — flagged in NOTES.md — because payback period can't be computed without one. Ideally replaced with a real representative onboarding-fee figure from sales/finance, not a fabricated flat number. | Sales / finance |
| `{{BENCHMARK_HIGH_VOLUME_THRESHOLD_PER_MONTH}}` | A real, citable published threshold for what counts as "high volume" invoice processing (used to echo the head keyword "how many invoices is considered high volume" in Section 2). Nothing in the brand guidelines gives this a number — currently addressed qualitatively without a number attached. | Product marketing / finance benchmarking |
| `{{AD_HEADLINE_1..3}}` | Live RSA headline text from Campaign 10 (Pricing & ROI / Benchmarks & KPIs ad groups), pasted into the ad-to-page continuity comment at the top of `index.html`. | Paid media / copy |
| `{{AD_DESCRIPTION_1..2}}` | Live RSA description text, same purpose as above. | Paid media / copy |
| `{{COMPANY_ADDRESS}}` | Physical business address for the footer (required for Quality Score's transparency/navigability check). Same token/value as `/mockups/ad-yooz/index.html` — one source of truth. | Legal / ops |

## Verified facts used directly (not tokens)

None on this page. Unlike `/ad-yooz`, this page makes no claims about ERP
connector count or capture channels — its only numeric claims are the
five illustrative CONFIG placeholders above, all explicitly labelled as
such in the on-page assumptions disclosure rather than asserted as fact.

## Open question affecting this manifest

See NOTES.md "Open questions" — whether `/ad-ap-roi` should be a
standalone tool (as built here), a variant of the existing "Yooz Score"
assessment, or a stripped-down calculator feeding into it. If the answer
is anything other than "standalone," several of the placeholders above
(particularly the benchmark citations) may end up sourced from or
replaced by the Yooz Score's own data model instead.
