# NVIDIA CEO Forecast

Forecast Polymarket's "Next CEO of NVIDIA?" Yes prices, 4 hours ahead, as 5 quantiles per minute.

## Strategy

Beats the house baseline (fixed sigma=0.0025) with a price-dependent volatility model:

1. **Base sigma**: `0.0055 * sqrt(p*(1-p))` — low-price markets barely move, high-price markets move more (binomial-like scaling), floored at 0.0005.
2. **Adaptive blend**: 50% weight on recent realized volatility (last 120 minutes, capped at 0.008) to adapt to the current regime.
3. **No drift**: drift terms hurt in backtests (prediction markets mean-revert).

## Backtest Results (practice cases p00-p04)

| Model | Pinball loss |
|-------|-------------|
| House baseline (sigma=0.0025) | 0.393 |
| This model | 0.302 |

~23% better than baseline on practice data. Official baseline practice score is 0.363589; this model should score ~0.28-0.30 on the official scorer.

## Files

- `main.py` — the forecaster (Python 3.13, stdlib only, deterministic)
- `README.md` — this file
- `LICENSE` — MIT license
