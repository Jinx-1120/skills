# Evidence And Valuation Discipline

Use this reference when collecting data, building cash-flow valuation, comparing peers, or deciding whether the current price already reflects expectations.

## Source Hierarchy

Prefer sources in this order:

1. Company filings, exchange announcements, official investor-relations material, audited reports, and preliminary results announcements.
2. Exchange or official market data for closing price, shares, market capitalization, and corporate actions.
3. Recognized financial data providers and data portals for standardized financials and multiples.
4. Sell-side reports, trade press, expert commentary, and industry databases as interpretive or triangulation evidence.

When data can change, verify current facts unless the user fixes a historical cutoff. Always record report date, data cutoff, valuation base date, fiscal period, currency, units, and whether figures are audited, preliminary, estimated, or model-derived.

## Freshness Rules

- Distinguish the data cutoff from the report date.
- Distinguish a trading-day close from an after-hours announcement.
- Do not claim the market has priced in an announcement unless the stock has traded after that announcement was public.
- Treat preliminary result forecasts as powerful but unaudited evidence.
- When sources disagree, identify the source timestamp and explain which source controls the analysis.

## Cash-Flow Valuation

Choose the cash-flow model from the question being answered:

- Use equity free cash flow when valuing common equity directly and capital structure is stable or debt is not the main driver.
- Use firm free cash flow when operating assets, enterprise value, or capital-structure-neutral comparison matters.

When writing in Chinese, prefer Chinese terms such as "股权自由现金流贴现估值", "公司自由现金流贴现估值", and "加权平均资本成本" rather than leaving unexplained acronyms. If acronyms are useful, define them once and then keep the report readable.

Core formulas:

```text
equity free cash flow = net profit + depreciation and amortization - capital expenditure - increase in working capital + net borrowing

firm free cash flow = operating profit after tax + depreciation and amortization - capital expenditure - increase in working capital

terminal value = next-year free cash flow / (discount rate - perpetual growth rate)

equity value from firm free cash flow = enterprise value - net debt + non-operating assets and adjustments
```

Scenario design must come from business drivers:

```text
addressable market -> company share -> revenue -> margin -> free-cash-flow conversion -> discount rate -> terminal growth -> equity value
```

Do not start from a desired equity value, market capitalization, or share price and then backfill assumptions.

## Sensitivity Discipline

When testing sensitivity, change one variable or a clearly named group of variables at a time. If a result changes because both terminal growth and revenue assumptions changed, disclose both. Never compare a prior valuation result with a revised result as if only one variable changed when the operating base, cash-flow rate, discount rate, or share count also changed.

Check that:

- Perpetual growth is lower than the discount rate.
- Perpetual growth is economically plausible for the company, industry maturity, and macro environment.
- Discount rate reflects business risk, country risk, leverage, and interest-rate environment.
- High terminal growth is supported by durable reinvestment opportunity, not just near-term industry heat.
- Cash-flow conversion is consistent with working capital, capital expenditure, and margin assumptions.

## Relative Valuation

Build the peer set by economic comparability first and listing convenience second.

For each peer, capture:

- Business exposure and comparability label.
- Market capitalization, enterprise value if available, and share-price date.
- Revenue, profit, growth, margins, return on equity, and cash-flow quality.
- Common multiples such as price-to-earnings, price-to-sales, price-to-book, and enterprise-value multiples when available.

Use multiple interpretation rules:

- A high multiple can be justified by higher growth, better margin, stronger cash conversion, lower risk, or scarcity.
- A low multiple can reflect lower quality, weaker growth, cyclicality, or poor comparability.
- Remove or separately discuss loss-making, one-off distorted, or structurally different peers.
- Identify the closest anchor peer rather than treating all peers equally.

## Price-In And Alpha Judgment

The price-in question asks what the current market capitalization already assumes.

Analyze:

- Implied revenue, net profit, free cash flow, or multiple needed to justify the current price.
- Whether the latest business evidence is already visible in traded market prices.
- Whether future upside requires earnings upgrades, multiple expansion, lower risk premium, or only continued execution.
- Whether the expected return is enough after downside and invalidation risks.

Do not call a stock attractive only because the company is high quality. Do not call it fully priced only because valuation multiples are high. Tie the judgment to expectations embedded in price versus evidence likely to change those expectations.

## Invalidation Rules

Every thesis needs explicit disconfirming evidence. Include leading indicators, not only backward-looking annual results.

Examples:

- Order intake or customer capital expenditure weakens.
- Product generation loses relevance or qualification timing slips.
- Peer share gains dilute the target company's growth.
- Price erosion overwhelms volume and mix improvement.
- Gross margin, net margin, or cash-flow conversion deteriorates for structural reasons.
- Working capital, inventory, receivables, or capital expenditure signal lower-quality growth.
- The stock rerates beyond the upside case without matching business evidence.
