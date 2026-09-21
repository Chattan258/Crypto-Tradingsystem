# Nine-Factor Equal-Weight Portfolio Backtest

[English](portfolio.en.md) | [简体中文](portfolio.md)

[Project home](../README.md)

![Portfolio cumulative return and drawdown](../assets/portfolio-cn.png)

## Portfolio construction

1. Calculate values for each of the 9 factors.
2. Generate long and short positions independently for each factor.
3. Calculate each factor's returns from price changes, trading fees, and funding payments.
4. Assign each factor a weight of 1/9 and combine returns and positions using those weights.
5. Aggregate returns by day to calculate cumulative returns, drawdown, and performance metrics.

Costs are calculated separately within each factor before returns are combined. In live execution, trades from different factors may offset one another, changing the quantities traded and the resulting fees.

## Backtest configuration

| Setting | Value |
|---|---|
| Portfolio method | Equal weight |
| Initial capital | 100,000 |
| Number-of-assets parameter per factor | 20 |
| Trading fee parameter | 0.00025, or 2.5 basis points |
| In-sample | 2022-01-01 to 2024-09-01 (boundary date excluded) |
| Out-of-sample | 2024-09-01 to 2025-09-22 |
| Daily return coverage | 2022-01-01 to 2025-09-22 |
| Daily observations | 1361 |

Local data end on September 22, 2025, with only part of the final day available.

Portfolio performance uses the backtest fee above. The average live execution fee was approximately 3.8 basis points; see the [trading system](execution.en.md) for details.

| Factor | Weight | Parameters |
|---|---|---|
| factor_1005 | 1/9 | `{'a': 246, 'b': 13, 'c': 158, 'period': 131}` |
| factor_1025 | 1/9 | `{'a': 220, 'b': 210, 'c': 316, 'period': 112}` |
| factor_1034_2h | 1/9 | `{'a': 3, 'b': 201, 'c': 157, 'd': 125, 'e': 136, 'f': 190, 'g': 10, 'h': 243}` |
| factor_1039_4h | 1/9 | `{'a': 127, 'b': 304, 'c': 228, 'd': 240, 'e': 84}` |
| factor_1042 | 1/9 | `{'a': 393, 'b': 304, 'c': 67, 'd': 265, 'e': 146, 'f': 269}` |
| factor_1043 | 1/9 | `{'a': 101, 'b': 108, 'c': 145}` |
| factor_1047_2h | 1/9 | `{'a': 266, 'b': 304, 'c': 385, 'd': 66, 'e': 230}` |
| factor_1048_4h | 1/9 | `{'a': 16, 'b': 229, 'c': 361, 'd': 300, 'e': 347, 'f': 78}` |
| factor_1052 | 1/9 | `{'a': 350, 'b': 297, 'c': 74, 'd': 22, 'e': 217, 'f': 285, 'g': 82, 'h': 286}` |

## Performance

| Period | Start | End | Cumulative return | Annualized return (arithmetic) | Sharpe | Max drawdown |
|---|---|---|---:|---:|---:|---:|
| In-sample | 2022-01-01 | 2024-08-31 | 107.08% | 40.1% | 3.739 | 4.2% |
| Out-of-sample | 2024-09-01 | 2025-09-22 | 36.37% | 34.3% | 3.795 | 2.1% |
| Full period | 2022-01-01 | 2025-09-22 | 143.45% | 38.5% | 3.743 | 4.2% |

Cumulative returns are the sum of daily returns, and drawdown is measured against fixed initial capital. Period performance is calculated from the continuous backtest without resetting positions at the boundary.

[Period performance data](../reports/portfolio-periods.csv) · [Portfolio backtest record](../reports/portfolio-summary.txt)
