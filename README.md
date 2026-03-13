# footmap.v1

A **PineScript v6** footprint-style volume heatmap indicator for [TradingView](https://www.tradingview.com/).

---

## Overview

**Footmap Volume Map** visualises the volume distribution at each price level within a candlestick bar, similar to a professional footprint chart. It estimates buy and sell volume using lower-timeframe data and renders a colour-coded heatmap directly on the chart.

### Key Features

| Feature | Description |
|---|---|
| **Volume Profile per Bar** | Splits each bar into configurable price rows and distributes volume across them using lower-timeframe (LTF) data. |
| **Buy / Sell Estimation** | Uses the Close-Location-Value (CLV) method — `(close − low) / (high − low)` — to estimate the buy/sell split. |
| **Heatmap Colouring** | Intensity scales from neutral to the dominant colour (green for buying, red for selling). |
| **Point of Control (POC)** | The price level with the highest volume is highlighted with a distinct border. |
| **Delta Display** | Each level optionally shows `+buy − sell` delta alongside total volume. |
| **Bar Summary Labels** | Total volume and aggregate delta displayed above each bar. |
| **Two Colour Modes** | *Heatmap* (intensity by total volume) or *Delta* (direction by buy/sell dominance). |

---

## Installation

1. Open [TradingView](https://www.tradingview.com/) and go to the **Pine Editor** (bottom panel).
2. Click **Open → New blank indicator**.
3. Delete the default code and paste the entire contents of **[`footmap.pine`](footmap.pine)**.
4. Click **Add to chart**.

> **Note:** The indicator requires a lower-timeframe data feed. Make sure the **Lower Timeframe** input (default `1` minute) is strictly lower than your chart's timeframe.

---

## Inputs

### Structure

| Input | Default | Description |
|---|---|---|
| Price Levels (Rows) | `10` | Number of price rows per bar (2–40). |
| Display Bars | `5` | How many recent bars render the footmap (1–20). |
| Lower Timeframe | `1` (1 min) | Timeframe used to source granular volume data. |

### Display

| Input | Default | Description |
|---|---|---|
| Show Delta per Level | `true` | Show buy−sell delta alongside volume at each row. |
| Highlight POC | `true` | Yellow border around the highest-volume row. |
| Show Bar Totals | `true` | Summary label (total vol + delta) above each bar. |
| Show Volume Numbers | `true` | Numeric labels inside each price-level box. |
| Color Mode | `Heatmap` | `Heatmap` = intensity by volume; `Delta` = intensity by direction. |

### Colors

All colours (buy, sell, POC, text, background, delta labels) are fully customisable via the indicator settings panel.

---

## How It Works

```
Chart Bar (e.g. 5 min)
┌──────────────────────┐
│  request.security_   │  ← Fetches 1-min OHLCV bars that fall
│  lower_tf()          │     inside the chart bar
└──────────┬───────────┘
           │
     ┌─────▼──────┐
     │ CLV Method  │  ← Estimates buy vs sell volume for each
     │ per LTF bar │     lower-timeframe bar
     └─────┬───────┘
           │
   ┌───────▼────────┐
   │ Row Allocation  │  ← Maps each LTF bar's price range to
   │ (price bins)    │     the chart bar's row grid and
   └───────┬─────────┘     distributes volume proportionally
           │
   ┌───────▼────────┐
   │  Heatmap Boxes  │  ← Draws colour-coded boxes per row
   │  + Labels       │     with volume/delta text
   └────────────────┘
```

---

## Limitations

- PineScript does not provide tick-level or Level 2 data. Volume distribution is **estimated** from lower-timeframe OHLCV bars.
- TradingView limits the number of drawing objects (boxes, labels) per indicator. Very large `Display Bars × Price Levels` combinations may exceed these limits.
- The lower timeframe must be available on your data plan and must be strictly less than the chart timeframe.

---

## License

[MIT](LICENSE) © 2026 Alby Anil
