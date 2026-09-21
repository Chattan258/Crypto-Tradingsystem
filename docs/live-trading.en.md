# Live Trading Record

[English](live-trading.en.md) | [简体中文](live-trading.md)

[Project home](../README.md)

The screenshot below shows cumulative account profit from August 11 to November 9, 2025. Initial capital was 2,000 USDT, and I used a fixed 2,000 USDT as total portfolio capital when sizing orders, consistent with the non-compounding approach used in the backtest.

![Live cumulative profit](../assets/live-performance.png)

| Item | Record |
|---|---|
| Initial capital | 2,000 USDT |
| Screenshot period | 2025-08-11 to 2025-11-09 |
| Cumulative profit | +282.89 USDT |
| Drawdown limit | 6% |
| Date stopped | 2025-11-09 |

## Why I stopped and what followed

The backtest I referred to at the time had a maximum drawdown of approximately 5%, so I set the live drawdown limit at 6%. On November 9, returns fell from their peak and drawdown exceeded 6%, reaching roughly 6.7%. Although the account was still profitable overall, I stopped the strategy according to the original rule. I was also preparing for postgraduate entrance exams at the time, so I did not restart it afterward.

## Live trading versus the backtest

I initially set the backtest fee to 2.5 basis points, but the average live execution fee turned out to be approximately 3.8 basis points. This difference is why I want to continue studying order execution: how to choose a suitable limit-order placement strategy that reduces fees while completing the rebalance.

[Order execution and fees](execution.en.md)
