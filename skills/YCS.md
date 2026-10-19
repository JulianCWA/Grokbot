# YCS

When to use it:
Pull a historical series of a quantitative metric (Excel YCS or the matching API call). Prefer this over repeated YCP calls when you need many dates.

Required inputs and access:
- Ticker (apply YCprefixes / YC-calling-rules)
- Metric / calc (required except for macro I: — leave blank)
- Start date (required)
- Optional: end date, reverse, transpose, retrieve dates, fill null, resample frequency, fill method, aggregation method

Sequence of work:
1. Apply YCprefixes and YC-calling-rules.
2. Build the formula or API request.
3. Return the series (or the request) with a short note on any nulls or resampling.

Excel formula:
=YCS(ticker, calc, start_date, [end_date], [reverse], [transpose], [retrieve_dates], [fill_null], [resample_frequency], [fill_method], [aggregate_function])

Parameters:
- ticker: required, correctly prefixed
- calc: required (blank for I:)
- start_date: required
- end_date: optional (blank = through today)
- reverse: "Y" to reverse order
- transpose: "Y"
- retrieve_dates: "Y" to include dates
- fill_null: quoted value to replace nulls / ERR: NO DATA
- resample_frequency: e.g. monthly, weekly, quarterly
- fill_method: "Forward" or "Backward"
- aggregate_function: e.g. last, mean, sum, max

API (verified):
GET /v3/companies/{TICKER}/series/{metric}?start_date=YYYY-MM-DD&end_date=YYYY-MM-DD
Mutual fund: /v3/mutual_funds/M:{TICKER}/series/{metric}?...
Index: /v3/indices/^{CODE}/series/level?...
Macro: /v3/indicators/I:{CODE}/series?...
Optional: &resample_frequency=monthly&resample_function=last

Response: results[metric].data = [[date, value], ...]

Examples:
=YCS("MSFT","price","2024-01-01","2024-06-30")
=YCS("M:MEIIX","total_monthly_return","2023-01-01")
GET /v3/companies/MSFT/series/price?start_date=2024-01-01&end_date=2024-06-30&resample_frequency=monthly&resample_function=last

Rules:
- Follow YC-calling-rules for prefixes, blank metric on macros, null handling, and decimals.
- For a single point use YCP instead.

What to return:
- The formula or ready API request.
- Note on series length or any nulls.

What requires approval:
- Nothing for drafting. Execute only if the user explicitly asks.
