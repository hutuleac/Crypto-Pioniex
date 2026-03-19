# Crypto-Pioniex · Futures Monitor

Real-time crypto futures dashboard for 4H setup analysis. Fetches live data from Binance Futures with automatic Bybit fallback — no backend, no build step, just open `index.html`.

## Features

- **Live metrics** — Price, Funding Rate, RSI 4H, ATR, OI, CVD across 5d/14d/30d
- **Signal analysis** — 10-category interpretation per symbol (Trend Macro/Swing, Pressure, Setup, Risk, FVG, EMA, Vol Spike)
- **Scoring engine** — Composite 0–10 score combining 7 weighted factors
- **Bot parameters** — Auto-generated entry/SL/TP/leverage when score ≥ 8.0
- **Dual-provider** — Binance Futures primary, Bybit V5 fallback per symbol
- **Symbol manager** — Add/remove symbols live without reload

## Supported Indicators

| Indicator | Description |
|-----------|-------------|
| RSI 4H | Momentum oscillator (OB > 70, OS < 30) |
| ATR 4H | Volatility for SL/TP sizing |
| Flow% 24h | Buy vs sell pressure on 1H × 24 |
| POC 5d/14d | Point of Control — max-volume price zone |
| AVWAP 5d/14d/30d | Anchored volume-weighted average price |
| CVD 5d/14d/30d | Cumulative Volume Delta (ACC/DIS) |
| EMA 50/200 | Trend filter + Golden/Death Cross |
| Market Structure | HH+HL (Bullish) vs LH+LL (Bearish) on 4H and 30d |
| OI / OI% 7d | Open Interest level and 7-day change |
| FVG | Fair Value Gaps on last 100 4H candles |
| Liquidity Sweep | Buy/Sell sweep detection on 4H |

## Usage

1. Open `index.html` in any modern browser
2. Default symbols: BTC, ETH, SOL, XRP, ZEC (all USDT perpetuals)
3. Add symbols via the input bar — auto-appends USDT if omitted
4. Data refreshes every 20 minutes automatically; use **Refresh** to force

## Scoring System

| Score | Status | Meaning |
|-------|--------|---------|
| ≥ 8.0 | Active | Bot parameters generated — entry/SL/TP shown |
| 6–7.9 | Watch | Partial confluence — monitor closely |
| < 6.0 | Wait | Insufficient signals |

Score components: Trend Macro (2.0) + Trend Swing (1.5) + Pressure (2.0) + CVD Quality (1.0) + Setup (2.0) + EMA (0.5) + FVG (0.5) + POC Confluence (0.5) − penalties

## Data Sources

| Provider | Endpoints Used |
|----------|---------------|
| Binance Futures | `/fapi/v1/ticker`, `/fapi/v1/klines`, `/fapi/v1/premiumIndex`, `/futures/data/openInterestHist` |
| Bybit V5 (fallback) | `/v5/market/tickers`, `/v5/market/kline`, `/v5/market/open-interest` |

No API keys required — all public endpoints.

## Deployment

Configured for [Vercel](https://vercel.com) via `vercel.json`. Any static host works.

```bash
# Vercel CLI
vercel --prod
```

## License

For educational and personal trading analysis only. Not financial advice.
