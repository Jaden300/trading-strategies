# Quant-Trading

Python backtesting and parameter-optimization framework for 5 trading strategies, each paired with a TradingView Pine Script. Scan the S&P 500 daily for live signals, backtest any strategy on any ticker, and visualize results with one command.

## Strategies

| Strategy | Type | Win Rate | Avg Hold |
|---|---|---|---|
| **Elektro BB** | Mean reversion (BB + RSI oversold entry) | ~80-100% | Months-years |
| **DCA Long** | Always-in with safety order ladder | ~100% | Weeks-months |
| **Bollinger WMA** | Breakout above WMA | ~87% | Months-years |
| **RMA ATR Bands** | Asymmetric ATR channel trend | ~64% | Weeks-months |
| **EMA Trail** | EMA crossover + ratcheting trailing stop | ~50-60% | Weeks |

All strategies are long-only, optimized across 10 large-cap US stocks, backtested 2021-2026 on daily bars, $1,500 capital, 33% risk per trade, 1.5% commission per leg.

## Install

```bash
conda env create -f requirements_conda.yml
conda activate trading
```

## Usage

**Visualize a backtest** - price chart, equity curve, drawdown:
```bash
python visualize.py --strategy elektro --ticker NVDA
python visualize.py --strategy rma_atr --ticker AAPL --save
```
Strategies: `rma_atr` · `ema_trail` · `bb_wma` · `elektro` · `dca`

**Compare all 5 strategies** on one ticker:
```bash
python compare.py --ticker NVDA
```

**Run the daily scanner** (after market close):
```bash
python strategy/strategy_elektro/scanner.py
python strategy/strategy_dca/scanner.py
python strategy/strategy_rma_atr/scanner.py
python strategy/strategy_bb_wma/scanner.py
python strategy/strategy_ema_trail/scanner.py
```

**Re-optimize parameters** (cross-asset grid search):
```bash
python strategy/strategy_rma_atr/tests/test_largecap.py
```

**TradingView Pine Scripts** - ready to paste, defaults set to optimized params:
```
strategy/strategy_<name>/pine_<name>_largecap.pine
```

## Credits

See [CREDITS.md](CREDITS.md) for the original TradingView Pine Script authors this repo is based on.

> Uses [yfinance](https://github.com/ranaroussi/yfinance) - free for personal/educational use only.
