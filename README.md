# Multi-Factor Equity Screener

Ranks the S&P 500 by combining five factor families — valuation,
profitability, momentum, volatility, and growth — into a single
composite score, with an interactive Plotly dashboard.

## What it does
- Pulls prices and fundamentals for ~500 equities via yfinance
- Computes five factor families per stock
- Normalizes cross-sectionally (z-score), weights, and ranks into deciles
- Outputs a ranked leaderboard + a 4-panel interactive dashboard

## Method
Cross-sectional z-score normalization → factor-family averaging →
weighted composite → decile ranking. Weights are renormalized per-stock
over available data for robustness to missing values.

## Data-quality engineering
Real market data is messy, and two artifacts surfaced during development:
- **Spinoff momentum artifact:** a recently spun-off ticker's discontinuous
  price history produced an 18-sigma momentum outlier that dominated the
  ranking. Fixed with a minimum-history filter and price-factor winsorization.
- **Corrupted valuation ratio:** a near-zero price-to-book inverted into an
  absurd book yield (~576). Fixed by winsorizing every inverted/derived
  metric at the point of creation.

Cleaning rule applied throughout: *winsorize every derived metric where it
is created*, not just the raw inputs.

## Quickstart
1. Open the notebook in Colab (badge above).
2. Run cells top to bottom.
3. Find the leaderboard and dashboard in `data/processed/`.

## Tech
Python · pandas · numpy · yfinance · scipy · plotly
