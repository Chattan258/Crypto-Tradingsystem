# Crypto Quantitative Backtesting and Trading System

[English](README.md) | [简体中文](README.zh-CN.md)

This is my personal exploration of quantitative trading in blockchain-based crypto assets, covering factor discovery, portfolio backtesting, and live trading.

The strategy takes a cross-sectional long–short approach: it compares factor values across assets at each point in time, ranks them to build long and short positions, and combines these into a multi-factor portfolio. During the research process, I used genetic algorithms and Bayesian optimization to search for parameters, alongside genetic programming to explore factor expressions. In live trading, the system uses the OKX API to update market data, read account positions, and execute orders.

I have brought together the experiments, system design, and live trading records here. For personal privacy reasons, factor formulas, core source code, and related materials are not publicly available at this time.

[Factor experiments](docs/research-cases.en.md) · [Portfolio backtest](docs/portfolio.en.md) · [Trading system](docs/execution.en.md) · [Live trading](docs/live-trading.en.md) · [Experiment directory](docs/experiment-inventory.en.md)

## How the system works

![System architecture](assets/architecture-cn.png)

Research and trading run separately. The research side calculates factors, searches for parameters, and runs backtests. The trading side reads the selected strategy configuration, updates market data, calculates target positions, and places orders for the difference between target and actual holdings.

The main tools are Python, pandas, NumPy, SciPy, Numba, and Matplotlib. Genetic programming uses DEAP, and exchange access uses CCXT.

[Modules and data flow](docs/architecture.en.md)

## Individual factor results

I compare in-sample and out-of-sample results to assess factor performance. The six experiments below include factors that remain profitable out of sample, as well as those whose returns weaken substantially or turn negative.

![In-sample and out-of-sample factor performance](assets/research-overview.png)

For example, the one-hour version of `factor_1043` is profitable in both periods, while the two-hour version of `factor_1018` becomes much weaker out of sample. These results led me to pay closer attention to performance beyond the training period.

The six cases were selected from 53 saved single-factor reports. Each report retains six candidate parameter sets; the chart above uses the first set from each report. The [experiment page](docs/research-cases.en.md) includes the parameters and other candidates, and the [experiment overview](docs/experiment-inventory.en.md) lists all reports.

## Nine-factor portfolio backtest

The portfolio combines nine factors, each with a weight of 1/9. Parameters are trained in sample, and data from September 1, 2024 onward are used for out-of-sample evaluation.

![Nine-factor portfolio backtest](assets/portfolio-cn.png)

| Period | Start | End | Cumulative return | Annualized return (arithmetic) | Sharpe | Max drawdown |
|---|---|---|---:|---:|---:|---:|
| In-sample | 2022-01-01 | 2024-08-31 | 107.08% | 40.1% | 3.739 | 4.2% |
| Out-of-sample | 2024-09-01 | 2025-09-22 | 36.37% | 34.3% | 3.795 | 2.1% |
| Full period | 2022-01-01 | 2025-09-22 | 143.45% | 38.5% | 3.743 | 4.2% |

Initial capital is 100,000. Daily returns are added using fixed initial capital, without compounding; drawdown is also measured against fixed initial capital. Positions carry through the sample boundary, with performance reported separately for each period.

Costs are calculated within each factor before returns are combined. Details are in the [portfolio backtest](docs/portfolio.en.md) and [methodology](docs/methodology.en.md).

## Live trading

I ran this cross-sectional long–short strategy with 2,000 USDT. The account screenshot below covers August 11 to November 9, 2025 and shows a cumulative profit of 282.89 USDT.

![Live cumulative profit](assets/live-performance.png)

The backtest I referred to at the time had a maximum drawdown of approximately 5%, so I set a 6% limit for live trading. On November 9, drawdown exceeded that limit. Although the account was still profitable overall, I stopped the strategy as planned.

I was preparing for postgraduate entrance exams at the time and did not restart the strategy. The live trading record therefore ends on November 9, 2025.

[Live trading record and why I stopped](docs/live-trading.en.md)

## Further research

Live trading highlighted a difference in transaction costs. The backtest assumed a fee of 2.5 basis points, while the average fee paid in live trading was approximately 3.8 basis points. My account's maker and taker fees were 2 and 5 basis points, respectively.

I would like to study execution using order book data, comparing how order price, waiting time, and cancellation and resubmission frequency affect fills. Alongside lower fees, I need to consider slippage, fill rates, and whether rebalancing completes on time.

[Order execution and transaction costs](docs/execution.en.md)

## Repository contents

`docs/` contains methodology and system descriptions, `assets/` contains figures, and `reports/` contains parameter and performance records. Raw market data, account information, and strategy source code remain local.
