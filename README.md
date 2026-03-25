# 📊 Trader Performance vs Market Sentiment
## Primetrade.ai — Data Science Intern Assignment

---

## Overview

This project analyzes how **Bitcoin market sentiment (Fear/Greed Index)** relates to **trader behavior and performance** on the Hyperliquid perpetual futures exchange.

**Dataset summary:**
| Dataset | Rows | Period |
|---------|------|--------|
| Fear/Greed Index | 2,644 | Feb 2018 – May 2025 |
| Historical Trader Data | 211,224 trades | May 2023 – May 2025 |
| Unique traders | 32 | — |

---

## Setup & Run

```bash
# Install dependencies
pip install pandas numpy matplotlib seaborn scipy scikit-learn jupyter

# Place data files in the same directory:
#   fear_greed_index.csv
#   historical_data.csv

# Run notebook
jupyter notebook trader_sentiment_analysis.ipynb
```

---

## Methodology

### Part A — Data Preparation
1. Loaded both CSVs and documented shape, nulls, and duplicates
   - **Result:** Both datasets are clean — 0 missing values, 0 duplicates
2. Parsed `Timestamp IST` (format `DD-MM-YYYY HH:MM`) → normalized daily dates
3. Merged on `date`; filtered F/G to trader date range (2023–2025)
4. Created key metrics per (date × account):
   - `total_pnl`, `win_rate`, `trades`, `avg_size_usd`, `long_ratio`

### Part B — Analysis
- **B1:** PnL distribution, win rate, and drawdown compared Fear vs Greed (t-test)
- **B2:** Trade frequency, position size, long/short bias by sentiment
- **B3:** Trader segmentation: frequent/infrequent, high/low size, consistent winner
- **7 charts** + 1 bonus model chart

### Part C — Actionable Output
- Two strategy rules derived from empirical evidence

### Bonus
- Random Forest classifier predicts next-day sentiment  
- **5-fold CV Accuracy: 90.6% ± 6.5%** (well above 80% majority baseline)

---

## Key Findings

| # | Insight | Evidence |
|---|---------|----------|
| 1 | Fear days → higher PnL | Avg PnL: $5,185 (Fear) vs $3,973 (Greed) |
| 2 | Fear days → higher activity | 105 vs 83 avg trades/day |
| 3 | Fear days → lower drawdown | −$20,800 vs −$36,868 max drawdown |

---

## Strategy Recommendations

### Strategy 1 — Fear-Day Accumulation Protocol
> **During Extreme Fear (F/G < 30):** Increase long position size by 20–30%  
> with strict stop-losses (<2%). Fear days show highest PnL and lowest drawdowns.

### Strategy 2 — Greed-Day Risk Reduction
> **During Extreme Greed (F/G > 70):** Reduce trade frequency by 30%,  
> cap position sizes at 80% of normal. Greed periods show larger drawdowns and lower per-trade PnL.

---

## Files

```
├── trader_sentiment_analysis.ipynb   # Main analysis notebook
├── README.md                          # This file
├── fear_greed_index.csv               # Input data (place here)
├── historical_data.csv                # Input data (place here)
├── chart1_pnl_distribution.png
├── chart2_behavior.png
├── chart3_long_short.png
├── chart4_cumulative_pnl.png
├── chart5_segments.png
├── chart6_heatmap.png
├── chart7_scatter.png
└── chart8_feature_importance.png
```

---

*Submitted for Primetrade.ai Data Science Intern — Round 0*
