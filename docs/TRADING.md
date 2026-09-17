# TRADING

A market-making quant trading framework, built against a simulated trading-competition environment, not a live brokerage or exchange API.

## Why this reads as a competition framework, not a live trading system

Two details confirm this:

- **`from datamodel import Order`** — this import, along with the `state.order_depths` structure used throughout, matches the standard framework used in simulated algorithmic-trading competitions (the well-known pattern from the IMC Prosperity-style competition format), not a real exchange's API.
- **Fictional product names** ("Osmium", "Pepper") appear in the code comments as the tradable instruments, which are competition-specific synthetic assets, not real securities or tickers.

This distinction matters for how to treat the code: it's a strategy-design exercise against a simulator, not something that places real trades or carries real financial risk as committed.

## Files

| File | What it is |
|------|------------|
| `TRADE-QUANT-FRAMEWORK.py` | Base version: hybrid mean-reversion + momentum alpha signal (`0.65 * mean_reversion + 0.35 * momentum`), weighted fair-value estimation over a rolling price history window. |
| `Trade-Profit-Quant-Model.py` | "Enhanced high-profit" iteration built on the base: spread-aware dynamic position sizing, milder inventory skew (0.26), per-product tuning (more aggressive on some instruments, safer on others). |
| `Trade-Profit-Quant-Framework.py` | A related iteration in the same lineage; compare against the two above to see which specific parameters (skew, thresholds, sizing) changed between versions. |
| `TRADE-QUANT-DATA-FRAMEWORK.py` | "v2" of the enhanced version: higher position limits, larger base/dynamic sizing, further-tuned inventory skew (0.24), tighter quote offsets. |
| `Trade Profit Strategy Model.ipynb` | A large (1.6MB) notebook, presumably backtesting or exploring the strategies implemented in the `.py` files above. Open directly to inspect backtest results and parameter sweeps; not summarized here since notebook output cells aren't meaningfully representable as prose. |

## Core mechanism: alpha + fair value estimation

All four `.py` files share the same underlying pattern, iterated on across versions:

1. **Fair value** — an exponentially-weighted average of recent prices (`weights = np.exp(np.linspace(...))`), giving more influence to recent prices than older ones.
2. **Alpha signal** — a combination of mean-reversion (how far current price sits from fair value, in standard-deviation units) and momentum (recent price direction), blended with fixed weights.
3. **Position sizing and quoting** — later versions add spread-awareness (only quote when the bid-ask spread offers enough edge to be worth it) and per-product tuning (different risk tolerance for different instruments).

## Reading the version lineage

The four files aren't independent strategies; they're successive tuning passes on the same core alpha model, each pushing further toward "higher profit target" at the cost of larger position sizes and tighter risk parameters (per the comments in `Trade-Profit-Quant-Model.py` and `TRADE-QUANT-DATA-FRAMEWORK.py`, which explicitly state the profit-target progression: "hundreds → 10k-100k+" and "hundreds → 10k-50k+"). If you're picking this back up, the notebook is the place to check which version's parameters actually backtested best, since the code comments describe intent, not verified results.

## If you ever adapt this toward real trading

This is explicitly a simulation-competition framework as written. Adapting market-making logic like this to real capital and a live exchange involves materially different concerns: real transaction costs and slippage, regulatory requirements depending on jurisdiction and how the system is operated, real counterparty and inventory risk, and exchange-specific API constraints that a competition's `datamodel` abstraction doesn't model. Treat any of these files as a strategy-logic reference for that future work, not as something ready to point at a live market.
