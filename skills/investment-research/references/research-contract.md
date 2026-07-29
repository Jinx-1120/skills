# Research Contract

Use this contract when drafting or reviewing a medium- to long-term equity research report. The report can use different section names, but it must answer each decision question with evidence, assumptions, inference, and investment judgment kept distinct.

## Required Report Spine

### 1. Executive conclusion

Draft this section after completing the research, then place it at the beginning of the report. Keep it to one decision sentence, one compact Bayesian ACH table, one upside line and one invalidation line.

The decision sentence must state the action label, valuation range, current-price relationship and data cutoff. Do not summarize every report section or merely say that the company is good or the industry is promising.

Use this compact shape:

```text
Decision: [buy / hold / watch / reduce / avoid] because the current price is [below / within / above] the decision range, while the leading hypothesis is [H] at [posterior].

| Competing hypothesis | Posterior | Most discriminating evidence |
| --- | ---: | --- |
| H1 | x% | ... |
| H2 | x% | ... |
| H3 | x% | ... |

Upside condition: ...
Invalidation: ...
```

Keep the detailed evidence, valuation reconciliation and scenario mechanics in the body.

### 2. Industry lens and peer set

Answer why the target company should be studied under the selected industry lens now.

Include:

- Formal industry classification and why it is insufficient or sufficient.
- Current revenue and profit driver.
- Customer demand chain and capital-expenditure link.
- Product or technology cycle that controls margins and growth.
- Market valuation anchor.
- Peer set with core, partial, and weak comparability labels.

### 3. Position among peers

Show where the company sits against peers using a compact table plus interpretation.

Minimum dimensions:

- Market capitalization and revenue scale.
- Revenue and profit growth.
- Gross margin, net margin, and return on equity.
- Asset turnover, working-capital efficiency, and cash conversion.
- Product generation or technology position.
- Customer quality, customer concentration, geography, and delivery ability when material.
- Valuation multiples.

Do not rank the company only by valuation multiple. A high multiple may reflect better growth, better margin structure, or crowded expectations.

### 4. Industry capacity

Answer whether the industry can support company growth.

Analyze:

- Addressable market size and what part is truly relevant to the company.
- Demand source: new build, replacement, penetration, outsourcing, localization, or price/mix upgrade.
- Customer budget and adoption cadence.
- Supply constraints, capacity expansion, qualification cycle, and bottlenecks.
- Price erosion and product mix effects.
- Competitive intensity and market-share ceiling.

Translate the industry analysis into a plausible revenue envelope. Do not use a desired equity value or market capitalization to set the industry scenario.

### 5. Company growth ability and competitive advantage

Answer whether the company can obtain the industry growth and why.

Separate growth ability into:

- Customer acquisition and share gain.
- Technology iteration and product roadmap.
- Mass-production and delivery execution.
- Cost control and product mix.
- Working-capital and cash-flow discipline.
- Management communication and capital allocation.

For high return on equity, explain the source:

- Product profitability: margin, mix, pricing power, cost curve.
- Turnover: inventory, receivables, fixed-asset intensity, operating cycle.
- Leverage: debt, payables, financial risk, equity base.

### 6. Financial quality

Use financial analysis to test the thesis, not to decorate the report.

Minimum checks:

- Revenue, gross profit, operating profit, net profit, and growth.
- Gross margin, operating margin, net margin, and expense ratios.
- Operating cash flow, free cash flow, and cash conversion versus profit.
- Inventory, receivables, payables, and working-capital trend.
- Capital expenditure and whether growth is becoming more capital intensive.
- Balance-sheet safety and dilution or financing needs.

### 7. Valuation and price-in judgment

Use cash-flow valuation and relative valuation to answer whether the current price already reflects expectations.

The conclusion should identify:

- What growth, margin, and cash-flow assumptions the current market capitalization implies.
- What has already been priced in.
- What remains underappreciated, if anything.
- Whether upside comes from earnings upgrades, multiple expansion, lower risk premium, or some combination.
- Whether the probability of high alpha is still attractive after the latest price move.

### Bayesian ACH conclusion inference

Use ACH after the full evidence chain and valuation work are complete. It is a conclusion-inference method, not a replacement for industry, company, financial or valuation analysis.

Default to three mutually exclusive hypotheses defined relative to expectations embedded in the current price:

- **H1 — expectations are too low:** durable business outcomes and cash flow are likely to exceed what the current price implies.
- **H2 — expectations are broadly fair:** execution is likely to match what is already priced in, leaving limited excess return.
- **H3 — expectations are too high:** peak earnings, weaker execution or valuation compression is likely to make outcomes fall short of the price.

Add a fourth hypothesis only for a genuinely distinct state such as a binary regulatory event, refinancing failure or major asset outcome. Tailor the wording to the company rather than forcing a fixed market-regime taxonomy.

Set priors explicitly. Reuse a prior report's posterior only if the hypotheses, security, valuation basis and material facts remain comparable; otherwise reset to equal or disclosed base-rate-informed priors.

Build a small evidence matrix from the report's most discriminating evidence:

- industry capacity and demand durability;
- peer-relative ability to capture growth;
- margin, return on equity and cash-conversion quality;
- balance-sheet and capital-allocation risk;
- cash-flow value, relative value and reverse-valuation implications;
- measurable catalysts and invalidation evidence.

Update in Bayesian form:

```text
P(H_i | E) is proportional to P(H_i) times the likelihood of the discriminating evidence under H_i.
```

Group dependent observations before updating. Revenue growth, profit growth and the same earnings announcement are usually one evidence cluster, not three independent confirmations; share price, market capitalization and valuation multiples may also encode the same market evidence.

Use rounded probabilities as disciplined judgments, not statistical precision. They must sum to 100%, and no hypothesis may receive 100%. If the top two are roughly within 10 percentage points or the ordering changes under reasonable valuation assumptions, state a mixed conclusion and prefer the more conservative action.

### 8. Future value improvement path

Describe value creation as a logic chain, for example:

```text
industry demand expands -> company share or product mix improves -> revenue grows -> margin or cash-flow conversion improves -> market raises certainty pricing -> equity value rises
```

Name the measurable signals that would confirm each link.

### 9. Invalidation conditions

State what evidence would prove the thesis wrong or materially weaker.

Common categories:

- Industry demand slows or customer capital expenditure is cut.
- Product prices fall faster than volume or mix can offset.
- Market share is diluted by peers.
- Technology route changes and weakens the company's advantage.
- Gross margin, net margin, or cash-flow conversion breaks.
- Inventory, receivables, or capital expenditure signals deteriorate.
- The stock price rises faster than the business outlook, weakening risk-reward.

## Quality Bar

The report is not complete unless a reader can trace:

```text
industry lens -> peer set -> industry capacity -> company ability -> financial quality -> valuation -> price-in judgment -> Bayesian ACH -> concise decision -> upside path -> invalidation
```
