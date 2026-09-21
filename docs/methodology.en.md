# Methodology

[English](methodology.en.md) | [简体中文](methodology.md)

[Project home](../README.md)

## Strategy construction

I rank assets by their factor values at each point in time and establish long and short positions. Each factor is calculated independently, and the resulting positions are combined with equal weights.

## Research periods

| Period | Dates | Purpose |
|---|---|---|
| In-sample | 2022-01-01 to 2024-09-01 | Factor parameter training and research |
| Out-of-sample | 2024-09-01 to 2025-09-22 | Evaluation after training |

September 1, 2024 belongs to the out-of-sample period. The in-sample period ends before that date, and the out-of-sample period includes September 22, 2025. The portfolio backtest runs continuously, carrying positions through the boundary; performance is calculated separately for each period.

The single-factor pages retain historical parameter experiments. The portfolio page reports results calculated over the periods above.

## Performance calculations

Daily return is the day's profit or loss divided by fixed initial capital. Hourly returns are summed into daily returns before performance metrics are calculated.

| Metric | Definition |
|---|---|
| Cumulative return | Sum of daily returns |
| Arithmetic annualized return | Mean daily return multiplied by 365 |
| Sharpe ratio | Mean daily return divided by its sample standard deviation, multiplied by the square root of 365; risk-free rate is zero |
| Maximum drawdown | Largest decline in cumulative return from its previous peak, measured against fixed initial capital |
| Return-to-drawdown ratio | Arithmetic annualized return divided by maximum drawdown |

Drawdown uses fixed initial capital as the denominator. The program rounds drawdown to three decimal places before calculating the return-to-drawdown ratio. Each period's drawdown is calculated from its own returns, while the full return curve remains continuous.

## Portfolio and costs

Initial capital is 100,000, and the trading fee parameter is 0.00025. Trading fees and funding payments are included in each factor's returns before they are combined with weights of 1/9. Positions are combined using the same weights.

During the live trading period, my account's taker fee was 0.0005 and maker fee was 0.0002, with an average execution fee of approximately 0.00038. Backtest results retain the original 0.00025 fee assumption. See [transaction costs and execution research](execution.en.md) for the comparison.

For this live trading run, each rebalance used a fixed 2,000 USDT as total portfolio capital, with order quantities determined by target positions. This matches the fixed-capital, non-compounding approach of the backtest. Account screenshots and historical backtests are recorded separately; see the [live trading record](live-trading.en.md).

## Experiment records

The [single-factor experiments](research-cases.en.md) contain six cases, each with six candidate parameter sets. The [experiment overview](experiment-inventory.en.md) lists 53 historical single-factor reports. The [portfolio record](../reports/portfolio-summary.txt) and [period performance data](../reports/portfolio-periods.csv) contain portfolio results for the stated periods.
