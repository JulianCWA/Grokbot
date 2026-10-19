# YCI

When to use it:
Pull a qualitative / info field (Excel YCI or the matching API call). Examples: sector, inception_date, frequency, source, adjustment.

Required inputs and access:
- Ticker (apply YCprefixes / YC-calling-rules)
- Info field code (required)
- Optional: transpose, fill null

Sequence of work:
1. Apply YCprefixes and YC-calling-rules.
2. Build the formula or API request.
3. Return the field value (or the request).

Excel formula:
=YCI(ticker, info_field, [transpose], [fill_null])

API (verified examples):
GET /v3/companies/{TICKER}/info/{field}
GET /v3/mutual_funds/M:{TICKER}/info/{field}
GET /v3/indicators/I:{CODE}/info/{field}

Examples:
=YCI("MSFT","sector")
=YCI("I:USGDP","adjustment")
GET /v3/companies/MTUM/info/earliest_performance_date

What to return:
- The formula or API request.
- The field value or a note if missing.

What requires approval:
- Nothing for drafting. Execute only if the user explicitly asks.
