# YCH

When to use it:
Pull the top 25 holdings of a fund or portfolio (Excel YCH or the matching API call).

Required inputs and access:
- Ticker of a fund or portfolio (apply YCprefixes / YC-calling-rules)
- Optional: show weights, weight type (portfolios), transpose, fill null

Sequence of work:
1. Apply YCprefixes and YC-calling-rules.
2. Build the formula or API request.
3. Return the holdings list (or the request).

Excel formula:
=YCH(ticker, [show_weights], [weight_type], [transpose], [fill_null])

Parameters:
- ticker: required
- show_weights: "Y" to include weights
- weight_type: "current" or "target" (portfolios only)
- transpose: "Y"
- fill_null: quoted value

API (verified):
GET /v3/companies/{TICKER}/holdings
Mutual fund: GET /v3/mutual_funds/M:{TICKER}/holdings
Returns top 25 items: {weight, name, security_id}

Note: Limited to 25 holdings. Full holdings must be exported from the website.

What to return:
- The formula or API request.
- The list of holdings (or note that it is top 25).

What requires approval:
- Nothing for drafting. Execute only if the user explicitly asks.
