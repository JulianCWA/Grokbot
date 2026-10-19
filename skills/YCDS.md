# YCDS

When to use it:
Pull the series of dates corresponding to a historical metric (Excel YCDS).

Required inputs and access:
- Ticker (apply YCprefixes / YC-calling-rules)
- Metric / calc (required)
- Start date (required)
- Optional: end date, reverse, transpose

Excel formula:
=YCDS(ticker, calc, start_date, [end_date], [reverse], [transpose])

Use when you need the date series that matches a YCS pull. For the values themselves use YCS.

What to return:
- The formula.
- The date list or a note if empty.

What requires approval:
- Nothing for drafting.
