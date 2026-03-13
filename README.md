# Footmap v1 — Heat & Volume

A **footprint-chart approximation** for [TradingView](https://www.tradingview.com/), written in **Pine Script v6**.

Footprint charts reveal *where* volume was traded inside each candle, giving you a clearer picture of buying / selling pressure at individual price levels — information that a plain candlestick chart hides.

---

## Features

| Feature | Description |
|---|---|
| **Heatmap boxes** | Each confirmed candle is split into N equidistant price levels. A coloured box is drawn for every level; opacity is proportional to volume (more opaque = more volume). |
| **Buy / Sell colour** | Levels dominated by estimated buying pressure are green; selling pressure is red. |
| **Point of Control (POC)** | The highest-volume level per bar is highlighted in gold with a dashed centre line. |
| **POC volume label** | The volume traded at the POC level is displayed next to the bar (K / M suffixed). |
| **Delta label** | Net buy−sell imbalance (Δ) is shown below each candle. |
| **Cumulative Δ** | Running total of all bar deltas, displayed as a live label to the right of the last bar. |

---

## How Volume Is Approximated

Pine Script does not expose tick-by-tick or order-book data, so the indicator estimates buying and selling pressure from the candle's anatomy:

```
buy_vol  = volume × (close − low)  / (high − low)
sell_vol = volume × (high − close) / (high − low)
```

Volume is then distributed across each price level proportionally to how much of the candle's range that level covers.

> **Note:** This is an *approximation*. On markets where real footprint data is available (CME futures, crypto exchanges with trade tape), the actual distribution may differ.

---

## Installation

1. Open TradingView → **Pine Editor**.
2. Copy the contents of [`footmap_v1.pine`](footmap_v1.pine) and paste them into the editor.
3. Click **Add to chart**.

The indicator runs as an **overlay** on the main price chart.

---

## Settings

### Footprint

| Input | Default | Description |
|---|---|---|
| Price levels per bar | 8 | How many horizontal slices each candle is divided into (2–30). |
| Bars to display | 20 | Number of most-recent confirmed bars to keep drawing objects for (1–50). |
| Show Point of Control | ✓ | Highlight the highest-volume level per bar. |
| Show delta labels | ✓ | Display Δ (buy − sell) below each bar. |
| Show POC volume label | ✓ | Show volume traded at the POC level. |

### Display

| Input | Default | Description |
|---|---|---|
| Opacity – high volume | 20 | Transparency of boxes at the peak-volume level (0 = fully opaque). |
| Opacity – low volume | 80 | Transparency of boxes at the lowest-volume level (95 = nearly invisible). |

### Colors

| Input | Default |
|---|---|
| Buy colour | `#00C853` (green) |
| Sell colour | `#D50000` (red) |
| POC colour | `#FFD700` (gold) |
| Positive delta label | `#00BFA5` (teal) |
| Negative delta label | `#FF6F00` (orange) |

---

## File Structure

```
footmap.v1/
├── footmap_v1.pine   ← Pine Script v6 source
└── README.md         ← this file
```

---

## License

See [LICENSE](LICENSE).
