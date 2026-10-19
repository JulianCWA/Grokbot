# YC-calling-rules

When to use it:
Apply these rules whenever you build a YCharts Excel formula or clone it as a Python/API call (YCP, YCS, YCI, YCH, YCD, YCDS).

Required inputs and access:
- Ticker and the appropriate metric / info / holdings field.
- Live API key required only for actual API calls (never store, print, or log it).

Sequence of work:
1. Format the ticker with YCprefixes (or the rules below).
2. Apply the shared rules.
3. Build the specific function (see the matching skill).

Ticker formatting:
- Stocks / ETFs: bare ticker (AAPL, SPY)
- Mutual funds: M: prefix (M:FBIOX, M:MEIIX). Canadian: M:TICKER.TO
- Economic indicators: I: prefix (I:10YTR, I:USGDP)
- Indexes: ^ prefix (^SPX, ^SPXTR)
- Portfolios: P: prefix (P:12345)
- SMAs: S: prefix
- Tip: 5-character mutual fund tickers ending in X can use =IF(AND(LEN(A1)=5,RIGHT(A1,1)="X"),"M:"&A1,A1)

Shared rules:
- No date argument → most recent value.
- Macro (`I:`): leave the metric blank.
- Mutual funds: always use the M: prefix and the /mutual_funds/M: path for API calls.
- As-of date can be earlier than requested. Always check the returned value date.
- Valid ticker + date before data exists, or metric with no value for that security: API returns [null, null]; Excel shows ERR: NO DATA.
- Invalid calc for that security type: API “Calc Not Found.”; Excel ERR: INVALID CALC.
- Wrong or missing prefix: Excel ERR: INVALID COMPANY.
- Fill Null (Excel): optional argument (must be quoted, e.g. "N/A") that replaces ERR: NO DATA or nulls. Available on YCP, YCS, YCI, YCH.
- Units are decimals in the API (0.0565 = 5.65%). Prices and levels are raw numbers.
- Never invent metric codes.
- Never log or persist the API key.

Verified API endpoints:
- YCP: POST /v3/excel/points with points="TICKER,metric" or "TICKER,metric,YYYY-MM-DD"
- YCS: GET /v3/companies/{TICKER}/series/{metric}?start_date=&end_date=  
  Mutual fund: /v3/mutual_funds/M:{TICKER}/series/{metric}  
  Index: /v3/indices/^{CODE}/series/level  
  Macro: /v3/indicators/I:{CODE}/series  
  Optional resample: &resample_frequency=monthly|weekly&resample_function=last|mean
- YCH: GET /v3/companies/{TICKER}/holdings or /v3/mutual_funds/M:{TICKER}/holdings (top 25)

What to return:
- The formula or ready Python request.
- One-line note if a quirk or error case applies.

What requires approval:
- Nothing for drafting. Execute live API calls only if the user explicitly asks.
