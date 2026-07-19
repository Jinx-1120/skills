---
name: investment-research
description: "Use when the user asks for a medium- to long-term investment research report on a listed company: deciding the correct industry lens, selecting comparable public peers, judging industry capacity, analyzing company position, financial quality, growth ability and competitive advantage, valuing the equity with cash-flow and relative valuation, deciding whether the current price already reflects expectations, identifying value-upside paths and invalidation conditions, and producing a Markdown or Word-ready report."
---

# Investment Research

Produce an evidence-backed medium- to long-term equity research report. The report must answer investment questions directly rather than filling a generic industry/company/valuation template.

## Boundary

Use this skill for listed-company research when the user wants a medium- to long-term investment view, course report, equity valuation report, industry-plus-company analysis, peer comparison, or a Markdown/Word report artifact.

Do not use it for pure intraday timing, short-term technical trading, broad market commentary with no target company, or a quick one-number data lookup. If the user asks for a live trade action, separate the long-term investment conclusion from execution timing and portfolio constraints.

## Seven Required Questions

Every completed report must answer:

1. Why should this company be researched under this industry lens now?
2. Where does the company sit among comparable listed peers?
3. Is industry capacity large and durable enough to support company growth?
4. Can the company obtain that growth, and what peer-relative advantages support it?
5. Does the current price already reflect expectations, and is there still investment value?
6. What drives future value improvement, and what is the logic chain?
7. What evidence would invalidate the investment thesis?

Read [references/research-contract.md](references/research-contract.md) when drafting the report structure or checking that these questions are answered.

## Workflow

### 1. Confirm scope and freshness

Identify the target company, listing venue and ticker, requested output format, report date, data cutoff, valuation base date and current or requested share price. If the user provides peers or an industry lens, treat them as a candidate set, not proof.

For facts that can change, use current primary or high-trust sources unless the user explicitly fixes an older cutoff. Record source dates, fiscal periods, announcement timestamps where material, currencies, units, and stale gaps. If a material event appears after the selected cutoff, label it as a post-cutoff event and state whether it is incorporated or only discussed separately.

### 2. Decide the industry lens before choosing peers

Start with formal classifications, then choose the investment research lens from current revenue and profit drivers, customer demand, product cycle, capital-expenditure chain, technology iteration, margin structure, and the market's actual valuation anchor.

Explain why the chosen lens is better than a broader administrative category or a narrower product label. Do this before any valuation scenario labels.

### 3. Build the peer set

Select comparable listed companies by economic exposure, not by name similarity. Classify each peer as core, partial, or weakly comparable based on business overlap, demand driver, product generation, customer base, geography, profitability, and size. If the user supplies peers, verify comparability and flag weak peers rather than silently using them.

### 4. Test industry capacity

Estimate whether the industry can support the target company's growth through addressable market size, demand drivers, replacement or new-build cycle, customer capital expenditure, supply constraints, price erosion, market-share ceiling, and competitive intensity.

Derive revenue and margin assumptions from this industry work. Do not start from a desired market capitalization or valuation result.

### 5. Assess company position and growth ability

Compare the target against peers on scale, growth, profitability, cash conversion, balance sheet, customer acquisition, delivery ability, technology iteration, product mix, and management communication quality. Decompose high return on equity into product profitability, asset turnover, and leverage so the source of returns is explicit.

### 6. Value the equity

Use at least one cash-flow valuation and one relative valuation unless the user narrows the task. Read [references/evidence-and-valuation.md](references/evidence-and-valuation.md) for valuation discipline, source hierarchy, price-in analysis, and invalidation rules.

Keep scenario assumptions internally consistent. A sensitivity change such as terminal growth must not be mixed with undisclosed changes to revenue, margin, cash-flow conversion, discount rate, or share count.

### 7. Synthesize investment value

Do not mechanically average valuation outputs. Use cash-flow valuation to frame intrinsic value, relative valuation to frame market pricing, and the current market capitalization to infer what expectations are already embedded.

Conclude with the current risk-reward, whether investment value remains, what would create high alpha, what is already priced in, and what evidence would change the conclusion.

### 8. Produce the artifact

Default to Markdown when the user does not specify a file type. Produce Word when requested. Read [references/output-formats.md](references/output-formats.md) before creating a saved report file.

The final report must be standalone and self-consistent. Do not mention prior versions, teacher feedback, prompt context, hidden assumptions, or the process of answering review comments. Convert review feedback into analysis dimensions inside the report.

## Completion Check

Before finishing, verify that:

- All seven required questions are answered explicitly.
- The industry lens is justified before peer comparison and valuation.
- Data dates, source classes, fiscal periods, units, and valuation base price are visible.
- Facts, model assumptions, inferences, and investment judgments are separable.
- Cash-flow and relative valuation results are reconciled without circular logic.
- Value-improvement paths and thesis invalidation conditions are concrete.
- Any Markdown or Word artifact was created and read back or otherwise checked.
