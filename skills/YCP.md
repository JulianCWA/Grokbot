# YCP

When to use it:
Use this to pull a single quantitative data point (latest or as-of a specific date) for a security using the YCharts Excel YCP function.

Required inputs and access:
- Ticker (apply YCprefixes rules first if needed)
- Metric / Calc code (required; never invent one)
- Optional: date, retrieve date flag, transpose, fill null value
- No external connectors required for writing the formula; user must have YCharts Excel Add-In installed to evaluate it.

Sequence of work:
1. Confirm or format the ticker using the YCprefixes skill/rules.
2. Confirm the metric/calc code (ask if unclear or not provided).
3. Build the YCP formula with the required arguments and any optionals the user specified.
4. Return the formula ready to paste into Excel, plus a one-line explanation of what it pulls.

Formula syntax:
=YCP(ticker, calc, [date], [retrieve_date], [transpose], [fill_null])
- ticker: string (required)
- calc: string metric code (required)
- date: optional date or relative (e.g. -1 for previous)
- retrieve_date: "Y" to also return the date
- transpose: "Y" to switch orientation
- fill_null: value to show instead of null/blank

Rules:
- Always apply ticker prefixes from YCprefixes before writing the formula.
- Never invent or guess a metric/calc code. If the user does not provide one, ask for it or point them to the YCharts metric reference.
- Prefer the official YCharts formula builder style when possible.
- If the user wants a series of dates or multiple points, recommend YCS instead.

How to validate the result:
- Formula starts with =YCP(
- Ticker is correctly prefixed
- Calc is present and not blank
- Optional arguments only included if requested

What to return:
- The complete Excel formula
- One short line describing what data it returns
- Any clarifying question if ticker or metric is missing

What requires approval:
- Nothing for drafting the formula. Do not modify Excel files or run macros unless the user explicitly asks in the same message.
