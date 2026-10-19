# YC Ticker Formating

When to use it:
Use this whenever you need to format a ticker or security identifier for a YCharts Excel formula (YCP, YCS, YCD, YCI, etc.) or when the user asks which prefix to apply.

Required inputs and access:
- The security or ticker the user wants (or a description of the asset class if the ticker is unknown).
- No external connectors required; this is a formatting rule set.

Sequence of work:
1. Identify the asset class from the ticker or description.
2. Apply the correct prefix/suffix from the rules below.
3. Return the correctly formatted ticker and a one-line reason.
4. If the asset class is unclear, ask one clarifying question before guessing.

Rules:
- Ordinary US stocks and ETFs: no prefix (e.g. AAPL, SPY, MSFT)
- US mutual funds: M: prefix (e.g. M:DODGX, M:FCNTX)
- Economic indicators: I: prefix (e.g. I:10YTR, I:USICUI)
- Indices: ^ prefix (e.g. ^SPXTR, ^GSPC)
- Separately managed accounts (SMAs): S: prefix (e.g. S:0P0001NKBP)
- Canadian ETFs: .TO suffix (e.g. XIU.TO)
- Canadian mutual funds: M: prefix + .TO suffix (e.g. M:FID631.TO)
- Never invent a prefix. If you are unsure of the asset class, stop and ask.

How to validate the result:
- Confirm the formatted ticker matches one of the patterns above.
- Do not add extra characters or spaces.

What to return:
- The correctly formatted ticker
- One short line stating which rule was applied
- If unclear: the clarifying question instead of a ticker

What requires approval:
- Nothing. This is read-only formatting guidance. Never write formulas or change files unless the user explicitly asks in the same message.
