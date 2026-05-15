---
name: fundamental-analysis
description: Conduct a rigorous, decision-oriented fundamental analysis of a publicly listed company (stock, ADR, or equity-linked security) and produce an investment-quality write-up. Use when the user asks "should I invest in [ticker/company]?", "analyze [company] fundamentals", "is [ticker] fairly valued?", "do a deep dive on [company]", "fundamental analysis of [X]", "is [stock] a buy?", "research [company] as an investment", or any equivalent investment-research framing. The output gives a clear verdict in today's market, a one-page executive summary upfront, and a detailed analysis below covering business model, moats, growth, competitive position, financials, valuation, management quality, shareholding structure, and risks.
---

# Fundamental Analysis of a Publicly Listed Asset

## Purpose

Produce a rigorous, decision-oriented fundamental analysis of a publicly listed company that lets a non-expert reader (a) understand the business from scratch and (b) decide whether it is a good investment in today's market.

The deliverable is opinionated. It ends with a clear verdict (Buy / Accumulate / Hold / Trim / Avoid), the price level / valuation band that would change the view, and the highest-conviction reasons for and against the call. Hedged "on the one hand, on the other hand" conclusions are a failure mode — name the call, then defend it.

This is research, not advice. Always close with a disclaimer (see Template).

---

## When to use this skill

Trigger whenever the user wants an investment-grade view of a single publicly listed equity — common phrasings include "analyze", "deep dive", "should I buy/invest in", "is X overvalued/undervalued", "fundamental analysis of", "evaluate [ticker] for my portfolio".

Do **not** use this skill for:
- Pure technical / chart analysis (no fundamentals requested).
- Macro or sector overviews not tied to a specific listed name.
- Private companies, pre-IPO, or crypto (the framework leans on public filings and market prices).
- Quick factual lookups ("what's AAPL's P/E?") — answer those directly.

If the user names a company but it isn't clear which listing (e.g., dual-listed, multiple share classes, ADR vs. local line), confirm the ticker/exchange before starting.

---

## Workflow

Follow these phases in order. Each phase should inform the next — don't write the verdict before doing the work.

### Phase 1 — Scope and clarify

Before researching, confirm the following with the user (use AskUserQuestion if anything is unclear; otherwise state your assumptions explicitly at the top of the report):

1. **Ticker and listing** — exact ticker + exchange (e.g., `MSFT / NASDAQ`, `RELIANCE / NSE`, `7203 / TSE`).
2. **Investor horizon** — short-term tactical (<1y), medium (1–3y), or long-term compounder (3–5y+). Default to long-term unless told otherwise.
3. **Currency for valuation** — usually the listing currency; flag FX exposure if material.
4. **Comparison set** — let the user override the peer set; otherwise pick 3–5 closest comparables yourself and justify.
5. **Any constraints** — ESG screens, income vs. growth preference, position-sizing context, existing exposure.

### Phase 2 — Information gathering

Use WebSearch / web_fetch and any connected data tools to pull, at minimum:

- **Primary filings**: latest annual report (10-K / 20-F / equivalent), latest quarterly report (10-Q / 6-K), most recent earnings release and call transcript, latest proxy / DEF 14A or equivalent governance filing.
- **Multi-year financial history**: 5 years of income statement, balance sheet, and cash flow. 10 years if available and relevant (e.g., to see through a cycle).
- **Investor materials**: latest investor day deck, segment disclosures, guidance.
- **Market data**: current price, 52-week range, market cap, enterprise value, average daily volume, short interest, beta.
- **Consensus**: sell-side consensus estimates, target price range, recommendation distribution (use to triangulate, not anchor).
- **Industry context**: market size and growth rate, top competitors' market share, regulatory environment, recent industry news.
- **Recent news (last 6–12 months)**: earnings beats/misses, M&A, management changes, regulatory actions, large litigation, activist involvement.
- **Insider activity and shareholding structure**: insider transactions in the last 12 months, top institutional holders, free float, promoter/founder/family stakes if relevant.

Always note **as-of dates** for every data point. Markets move; the report must be timestamped.

If a data point is unavailable or paywalled, say so explicitly rather than guessing. Distinguish "I couldn't verify" from "this is the figure".

### Phase 3 — Business understanding

Build the picture from scratch as if the reader has never heard of the company.

- What does the company actually do? Describe in one paragraph a smart 14-year-old could follow.
- **Revenue map**: break revenue by segment, geography, customer type, product. Show the mix and how it has shifted over 3–5 years.
- **What is growing vs. what is shrinking?** Tag each segment as growth engine, mature/cash cow, or declining/legacy.
- **Unit economics**: how does the company actually make money on a per-unit / per-customer / per-transaction basis? Gross margin by segment if disclosed.
- **Customer concentration** and **supplier concentration** — single points of failure.
- **Business model classification**: transactional, subscription/recurring, project-based, capital-intensive, asset-light, platform/network, regulated utility, commodity, etc. Different models warrant different valuation lenses.

### Phase 4 — Industry and competitive position

- **TAM / SAM / SOM** if it can be reasonably estimated; otherwise size the market with named third-party sources.
- **Industry structure**: Porter's Five Forces in 4–6 sentences (don't draw the diagram unless asked, just synthesize the forces). Concentration: oligopoly, fragmented, monopoly-ish.
- **Market share** vs. top 3 peers, trend over 3–5 years (gaining, holding, losing).
- **Moat assessment** — name the moat type(s) and rate durability:
  - Network effects
  - Switching costs
  - Cost advantages (scale, process, location, input access)
  - Intangible assets (brand, patents, regulatory licenses)
  - Efficient scale (small-market natural monopoly)
  - Data advantage
- For each claimed moat, give the **evidence** (pricing power across cycles, customer retention/churn, gross margin durability, share gains under competitive attack). A moat without evidence is a story, not a moat.
- **Competitive threats** — incumbents, new entrants, substitutes, disintermediation. Be specific (name the competitors).

### Phase 5 — Financial analysis

Pull and analyze 5+ years of financials. Don't dump tables — interpret them. Cover:

**Growth and quality of growth**
- Revenue CAGR (3y, 5y), organic vs. inorganic split, volume vs. price mix where disclosable.
- Gross margin and operating margin trend — expanding, stable, or compressing?
- EBITDA and EBIT growth, operating leverage.
- Net income growth — and whether it tracks operating cash flow (divergence is a flag).

**Returns on capital**
- Return on equity (ROE), return on invested capital (ROIC), return on assets (ROA). Compare to cost of capital (WACC) — ROIC > WACC is value creation; below is value destruction.
- Decompose ROE (DuPont): margin × turnover × leverage. Where is the return coming from?

**Cash flow quality**
- Operating cash flow vs. reported net income (conversion ratio).
- Free cash flow (OCF − capex). FCF margin and FCF/share trend.
- Working capital movements — releases or absorptions, and why.
- Capex intensity: maintenance vs. growth capex if disclosed.

**Balance sheet health**
- Net debt, net debt / EBITDA, interest coverage (EBIT / interest).
- Debt maturity profile and refinancing risk in next 24 months.
- Off-balance-sheet items (operating leases, JVs, guarantees).
- Goodwill / intangibles as % of equity — impairment risk.
- Liquidity: current ratio, quick ratio for working-capital-heavy businesses.

**Capital allocation track record**
- How has management spent cumulative FCF over 5 years? Reinvestment, M&A, buybacks, dividends, debt paydown.
- M&A scorecard: any disclosed deal IRRs, write-downs, or accretion vs. promise.
- Buyback timing — buying back near highs or systematically?
- Dividend policy and coverage.

**Earnings quality red flags**
- Recurring "one-time" charges.
- Aggressive revenue recognition / channel stuffing.
- Receivables growing faster than revenue.
- Tax rate anomalies.
- Frequent restatements or auditor changes.
- Heavy use of non-GAAP / adjusted metrics that strip recurring costs (especially stock-based comp).

### Phase 6 — Long-term growth prospects

- Forward revenue drivers, segment by segment. Distinguish **structural** (TAM growth, share gain, pricing) from **cyclical** (capex cycle, commodity price).
- 3–5 year revenue and earnings power scenarios (bear / base / bull) with explicit assumptions.
- Catalysts in next 6–18 months (product cycles, regulatory decisions, capacity coming online, expected margin inflections).
- Cyclical position — where in the cycle is the industry?

### Phase 7 — Management and governance

- **CEO and CFO**: tenure, background, prior track record (look up; cite). Insider or outside hire?
- **Skin in the game**: insider ownership %, recent buys/sells (a CEO selling into weakness is a flag; insider buying with own cash is a positive).
- **Compensation structure**: pay-for-performance? What metrics drive bonuses? Heavy equity comp at high prices is dilutive — quantify SBC as % of revenue or FCF.
- **Board quality**: independence, related-party transactions, classified board, dual-class shares.
- **Capital allocation discipline** (cross-link to Phase 5).
- **Communication quality**: do they pre-announce, sandbag, or guide aggressively then miss? Read 4–8 recent earnings transcripts for tone.
- **Red flags**: high executive turnover, founder/CEO sales of large stakes, related-party transactions, governance downgrades, regulatory or audit issues.

### Phase 8 — Shareholding structure

- **Free float** vs. promoter/founder/family/government stakes.
- **Top institutional holders** and concentration. Quality of holders (long-only vs. fast money).
- **Insider ownership** and recent insider trading activity.
- **Pledged shares** (especially relevant in EM / Indian context — flag if any).
- **Dual-class** or weighted-voting structures — who actually controls the company?
- **ADR / GDR** dynamics if relevant.
- **Recent placements, follow-on offerings, or major secondary sales** — supply overhang.

### Phase 9 — Valuation

Triangulate across at least two of the following; do not rely on a single number.

**Multiples vs. peers and own history**
- P/E (trailing, forward), EV/EBITDA, EV/Sales, P/B, P/FCF, PEG.
- Pick the multiple that fits the business: EV/EBITDA for capital-intensive, P/E for stable earners, P/Sales or EV/Sales for unprofitable growth, P/B for financials, FFO multiples for REITs, EV/Reserves for resource names.
- Compare to (a) own 5- and 10-year median, (b) closest peers. Is the premium/discount justified by growth, returns, or moat?

**Scenario-based fair value**
- Bear / Base / Bull fair values with probability weights and explicit assumptions on growth and margins. Show expected value vs. current price.

**Yield / income perspective** (for mature businesses)
- Dividend yield, FCF yield, shareholder yield (dividend + buybacks − dilution).

**Sanity checks**
- What does the market seem to be pricing in (implied growth and margins to justify today's multiple)?
- Where is the multiple vs. its own history at similar margin / growth levels?

State the **conclusion**: undervalued, fairly valued, overvalued, and by roughly how much. Give a **fair value range**, not a single false-precision number.

### Phase 10 — Risk assessment

Enumerate risks. For each, give:
- **Description** (what could go wrong, concretely)
- **Likelihood** (low / medium / high)
- **Materiality** (impact on thesis: minor / meaningful / thesis-breaking)
- **Mitigants or signposts** (what you'd watch to know if it's playing out)

Cover at minimum:
- Business-specific: customer concentration, product cycle, competitive disruption.
- Financial: leverage, refinancing, covenants, dilution risk.
- Industry / cyclical: end-market softness, commodity exposure.
- Regulatory / political / legal: pending litigation, regulatory inquiries, anti-trust, sanctions, tariffs.
- Geopolitical / FX (where revenue / production crosses borders).
- ESG-material risks (climate, governance, social license — only where they hit the P&L or cost of capital).
- Macro sensitivity (rates, growth, inflation).
- **Tail risks** (low-probability, high-impact). Be honest about what could permanently impair capital.

### Phase 11 — Synthesis and verdict

Tie it together. State the call, the price (or valuation level) that would change it, the catalysts and signposts to watch, and what the position sizing implication is for a typical investor at this horizon.

The verdict should be one of:
- **Buy** — favorable risk/reward, clear thesis, asymmetric upside.
- **Accumulate** — long-term attractive but build the position on weakness or dollar-cost average.
- **Hold** — existing holders should stay, new money should wait.
- **Trim** — reduce position; risk/reward has deteriorated.
- **Avoid** — do not buy.

A "Pass / Too Hard" verdict is acceptable if the business is genuinely unanalyzable from outside; say so plainly rather than fudging.

---

## Output Format

The report has two parts: a one-page **Executive Summary** upfront, then **Detailed Analysis** below. Save the report as a Markdown file in the user's workspace, and after delivering it offer to convert to PDF, Word (.docx), or HTML on request (use the `pdf`, `docx`, or relevant skill).

### Executive Summary (top of document, ~1 page)

```
# [Company Name] ([Ticker / Exchange]) — Fundamental Analysis
*As of [Date] · Price: [X] · Market Cap: [Y] · 52-wk range: [low–high]*

## Verdict: [Buy / Accumulate / Hold / Trim / Avoid]
**Fair value range:** [low – high] (vs. current [price]) — implies [+/− X%] over [horizon].
**Horizon assumed:** [short / medium / long]

## In one paragraph
[2–4 sentences: what the company does, why it makes money, the headline call, and the single most important reason.]

## Top 3 reasons to own
1. ...
2. ...
3. ...

## Top 3 reasons to be cautious
1. ...
2. ...
3. ...

## What would change the view
- Bullish triggers: ...
- Bearish triggers: ...

## Key numbers at a glance
| Metric | Latest | 3y CAGR / Trend | vs. Peer Median |
|---|---|---|---|
| Revenue | | | |
| Operating margin | | | |
| FCF | | | |
| ROIC | | | |
| Net debt / EBITDA | | | |
| Forward P/E (or relevant multiple) | | | |
```

### Detailed Analysis (below)

Organize in the order of the workflow phases:

1. **Business Overview** — what the company does, segments, revenue mix, geography, what's growing vs. shrinking.
2. **Industry & Competitive Position** — market structure, market share, moat assessment with evidence, threats.
3. **Financials** — growth, profitability, returns on capital, cash flow quality, balance sheet, capital allocation, earnings quality.
4. **Long-Term Growth Prospects** — drivers, scenarios, catalysts.
5. **Management & Governance** — bios, skin in the game, comp structure, communication track record, red flags.
6. **Shareholding Structure** — free float, top holders, insiders, pledges, dual-class.
7. **Valuation** — multiples, DCF or reverse-DCF, scenario fair values, yield perspective, conclusion.
8. **Risks** — table with description, likelihood, materiality, signposts.
9. **Bull Case / Bear Case** — coherent one-paragraph narratives.
10. **Verdict & What to Watch** — restate the call, the signposts, and the position-sizing implication.

### Tone, length, and formatting

- Write like an analyst briefing a portfolio manager, not like a corporate IR page. Plain language, opinionated, but always show the work.
- **Length: the detailed section should be up to ~1,000 words; shorter is fine and often better.** The goal is a quick, accurate, comprehensive read — not exhaustive coverage. Compress ruthlessly; cut anything that doesn't move the verdict.
- Use tables for financial history, peer comps, and the risk matrix — they compress information densely. Use prose for the narrative; do not bullet-point the whole report.
- Cite sources inline with links (10-K, transcript, third-party data). Distinguish facts from analyst inferences.
- Always include **as-of date** and currency.

### Mandatory closing line

End the report with:
> *This is research, not investment advice. Stocks can lose value. Do your own due diligence and consider consulting a licensed financial advisor.*

---

## Quality bar / self-check before delivering

Run through this checklist before returning the report:

- [ ] Verdict is explicit, not hedged.
- [ ] Fair value is a **range**, not a single number, and is tied to explicit assumptions.
- [ ] Every claimed moat has evidence cited.
- [ ] Revenue, margin, and FCF trends are over **at least 5 years**.
- [ ] Valuation conclusion is triangulated across at least two methods, with explicit assumptions.
- [ ] Risks include at least one **thesis-breaking** scenario and signposts to watch.
- [ ] Management section reads from primary sources (proxy, transcripts), not press releases.
- [ ] Numbers are timestamped (as-of date) and currency-labeled.
- [ ] Every data point either has a source or is flagged as unverified.
- [ ] Disclaimer is present.

If any box is unchecked, fix it before sending.

---

## Common failure modes to avoid

- **Story-led, evidence-light**: gushing about "an incredible business" without ROIC numbers, share trends, or pricing-power evidence.
- **Single-method valuation**: relying on one multiple or peer comp without triangulating against history, scenarios, or implied expectations.
- **Anchored to consensus**: reciting the sell-side narrative rather than testing it.
- **Recency bias**: extrapolating the last two quarters as if they're the new normal.
- **Ignoring the balance sheet** in growth-stock writeups, or **ignoring growth optionality** in value writeups.
- **Burying the lede**: an executive summary that doesn't actually say buy or sell.
- **False precision**: $187.42 fair value. Use ranges.
- **Stock-based comp invisibility**: presenting adjusted EPS as if SBC weren't real dilution.
- **No "what would change my view"**: every thesis should be falsifiable.

---

## Tooling notes

- Default research stack: WebSearch + web_fetch for primary sources, transcripts (e.g., investor relations pages, SEC EDGAR, company filings sites for non-US), and reputable financial-data sites for ratios and historicals.
- If the user has a finance or markets plugin / connector enabled (Bloomberg, FactSet, Refinitiv, Tikr, Stratosphere, Koyfin, screener.in, etc.), prefer it over scraped web data.
- For non-US listings, source the local-language annual report if needed and translate the salient passages.
- For India-listed names specifically, also pull: BSE/NSE shareholding pattern (quarterly), promoter pledge data, related-party transactions schedule, and corporate-governance report.
- The final report is delivered as a Markdown file in the user's workspace. After delivery, offer to convert it to **PDF**, **Word (.docx)**, or **HTML** on request (use the `pdf`, `docx`, or relevant skill). Offer a slide version (`pptx`) only if the user asks.
