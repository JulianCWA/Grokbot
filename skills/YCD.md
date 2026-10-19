# YCD

When to use it:
Pull the date of a single quantitative data point (Excel YCD).

Required inputs and access:
- Ticker (apply YCprefixes / YC-calling-rules)
- Metric / calc (required)

Excel formula:
=YCD(ticker, calc, [date])

Use when you only need the as-of date of a YCP-style point. For the value itself use YCP (with retrieve date = "Y").

What to return:
- The formula.
- The date or a note if no data.

What requires approval:
- Nothing for drafting.
