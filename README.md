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
├── footmap_v1.pine          ← Footmap Heat & Volume — Pine Script v6 source
├── market_profile_v1.pine   ← Multi-Session Market Profile — Pine Script v6 source
└── README.md                ← this file
```

---

# Multi-Session Market Profile [Clone]

A **multi-session Market Profile** overlay for [TradingView](https://www.tradingview.com/), written in **Pine Script v6**.

Displays a classic Market Profile histogram for the live session alongside compact side columns for up to 6 completed past sessions, all drawn on the main price chart.

---

## Features

| Feature | Description |
|---|---|
| **Gray histogram** | Live-session volume distribution across price rows, proportionally sized. |
| **Red POC cells** | The highest-volume price row (Point of Control) highlighted in red/crimson. |
| **Blue VA cells** | Rows inside the configurable Value Area highlighted in blue. |
| **Volume numbers** | Per-row volume displayed as M / K / raw integers. |
| **Side session columns** | Up to 6 completed sessions shown as narrow coloured columns to the left of the live histogram. |
| **Current-price line** | Horizontal blue line tracking the current close price, with a price label. |
| **Round-number line** | A semi-transparent blue line drawn at the nearest round-number level. |

---

## Installation

1. Open TradingView → **Pine Editor**.
2. Copy the contents of [`market_profile_v1.pine`](market_profile_v1.pine) and paste them into the editor.
3. Click **Add to chart**.

The indicator runs as an **overlay** on the main price chart.

---

## Settings

### Profile Settings

| Input | Default | Description |
|---|---|---|
| Past Sessions to Show | 6 | Number of completed sessions displayed as side columns (1–6). |
| Row Height (price units) | 0.20 | Height of each price row. Tune per instrument (XAU/USD ≈ 0.20, NQ ≈ 5, ES ≈ 1). |
| Value Area % | 70.0 | Percentage of total session volume defining the Value Area (10–100). |
| Histogram Width (bars) | 18 | Width in bars of the live-session histogram (5–50). |
| Side Column Width (bars) | 6 | Width in bars of each completed-session side column (2–14). |
| Gap Between Columns | 1 | Bar gap inserted between adjacent session columns (0–4). |

### Display Options

| Input | Default | Description |
|---|---|---|
| Show Volume Numbers | ✓ | Display volume text labels inside each price row. |
| Highlight POC (red) | ✓ | Colour the Point of Control row red. |
| Highlight Value Area | ✓ | Colour Value Area rows blue (side columns) / darker gray (live histogram). |
| Show Current-Price Line | ✓ | Draw a horizontal blue line + label at the current close price. |
| Show Live Session Histogram | ✓ | Render the proportional histogram for the ongoing session. |

---

## License

See [LICENSE](LICENSE).
