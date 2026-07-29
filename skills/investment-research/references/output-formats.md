# Output Formats

Use this reference when the user asks for a saved Markdown or Word report.

## Format Choice

Default to Markdown when the user does not specify a format. Use Word when the user asks for a course submission, formal report, `.docx`, or Word document.

Markdown is best for fast iteration, review, and version control. Word is best for submission, sharing, and final formatting.

## Standalone Report Rules

The report must read as an independent research product.

Do not include:

- Mentions of old versions, new versions, previous reports, teacher comments, prompts, or chat history.
- Meta-language such as "according to the user's correction" or "this revision fixes".
- Unsupported certainty, exact upside claims without a valuation base, or investment conclusions detached from price.

Do include:

- Report date and data cutoff.
- Target company, ticker, listing venue, and currency/unit conventions.
- Valuation base date and share price or market capitalization.
- Source classes and whether important figures are audited, preliminary, estimated, or model-derived.
- Tables for peer comparison and valuation assumptions when useful.
- An appendix or note for major assumptions and unresolved data gaps.

## Concise Executive Conclusion

Write the executive conclusion after completing the analysis, then place it first. Keep it compact even when the report body is long.

Use only:

1. One decision sentence containing the action label, valuation range, current-price relationship and data cutoff.
2. One three- or four-row Bayesian ACH table containing each competing hypothesis, its rounded posterior and one decisive evidence item.
3. One line for the value-upside condition.
4. One line for the main invalidation condition.

Do not add a second summary, a long list of supporting facts, or a paragraph-by-paragraph recap. The ACH table is the visible bridge from evidence to conclusion; full evidence and probability reasoning belong in the report body.

## Markdown Report

Save the report as `.md` when requested. Use clear headings, compact tables, and source notes. Keep calculation tables reproducible enough that the user can inspect assumptions.

## Word Report

When producing Word:

- Create a real `.docx` document rather than screenshots or pasted images.
- Preserve tables as editable tables where feasible.
- Use a professional report structure with title, date, section headings, tables, and source notes.
- Reopen, extract text, inspect metadata, or render the document when feasible before reporting completion.
- If Word creation or read-back cannot be verified, say so explicitly and provide the Markdown source as the reliable artifact.

## Final Response

When returning to the user, include:

- The saved report path, if a file was created.
- The valuation base date and whether latest market or announcement data was included.
- The main conclusion in one or two sentences; do not reproduce the full ACH table unless the user asks.
- Any verification performed on the artifact.
