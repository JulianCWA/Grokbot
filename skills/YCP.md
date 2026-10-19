# YCP

When to use it:
Pull one quantitative data point (latest or as-of a date) — either as an Excel YCP formula or the matching API call.

Required inputs and access:
- Ticker (apply YCprefixes / YC-calling-rules)
- Metric / calc (required except for macro I: — leave blank)
- Optional: date, retrieve date, transpose, fill null

Sequence of work:
1. Apply YCprefixes and YC-calling-rules.
2. Build the formula or API request.
3. Return it with a short description and any error/null note.

Excel formula:
=YCP(ticker, calc, [date], [retrieve_date], [transpose], [fill_null])

Parameters:
- ticker: required, correctly prefixed
- calc: required (blank for I:)
- date: optional; blank = most recent
- retrieve_date: "Y" to also return the date (spills two cells)
- transpose: "Y"
- fill_null: quoted value (e.g. "N/A") to replace ERR: NO DATA

API:
POST /v3/excel/points
data = {"points": "TICKER,metric"} or {"points": "TICKER,metric,YYYY-MM-DD"}
# Mutual fund: "M:TICKER,metric"
# Macro: "I:CODE,"

Response (verified):
results[metric]["" or date]["results"] = [value_date, value]
or [null, null]

Examples:
=YCP("MSFT","price")
=YCP("M:MEIIX","total_monthly_return")
=YCP("I:USGDP")
=YCP("MTUM","price","2024-12-31",,,"N/A")

Rules:
- Follow YC-calling-rules for prefixes, blank metric, null vs Calc Not Found vs INVALID COMPANY, fill null, and decimals.
- If the user wants a series, recommend YCS.

What to return:
- The complete formula or points string / Python snippet.
- One short line describing the result or expected null/error.

What requires approval:
- Nothing for drafting. Execute only if the user explicitly asks.
