<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0f2027,100:2c5364&height=180&section=header&text=Trader%20Sentiment%20Analysis&fontSize=38&fontColor=ffffff&animation=fadeIn" />
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=20&pause=1000&color=2C5364&center=true&vCenter=true&width=650&lines=Bitcoin+Sentiment+%C3%97+Trader+Behavior+Analysis;Fear+%26+Greed+Index+%C3%97+Hyperliquid+Trade+Data;Predictive+Modeling+%2B+Trader+Archetype+Clustering" alt="Typing SVG" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-ML%20Model-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white" />
</p>

# Trader Performance vs Market Sentiment Analysis

An analysis of how Bitcoin market sentiment (Fear/Greed Index) relates to trader behavior and performance on Hyperliquid, exploring whether sentiment regimes predict trading outcomes and how traders adjust behavior in response to market mood.

## Overview

This project merges Hyperliquid's historical trade data with the Bitcoin Fear/Greed sentiment index to answer three core questions:
- Does trader performance (PnL, win rate) differ across sentiment regimes?
- Do traders change behavior (frequency, position size, long/short bias) based on sentiment?
- Can trading outcomes be predicted from sentiment and behavioral features, and do distinct trader archetypes emerge?

## Setup

**Requirements:**
- Python 3.x
- Jupyter Notebook
- Libraries: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`

Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn jupyter
```

## How to Run

1. Make sure both dataset files are in the **same folder** as `analysis.ipynb`:
   - `fear_greed_index.csv` — Bitcoin sentiment data
   - `historical_data.csv` — Hyperliquid trade data
2. Launch Jupyter:
   ```bash
   jupyter notebook analysis.ipynb
   ```
3. Run all cells top to bottom (Kernel → Restart & Run All) to reproduce the full analysis, charts, and model outputs.

## Data

- **Sentiment dataset:** 2,644 rows — daily Fear/Greed classification.
- **Trade dataset:** 211,224 rows — individual trades with account, coin, execution price, size, side, PnL, and fees.
- No missing values or duplicates in either dataset.
- Datasets were merged on date, giving a combined dataset spanning five sentiment regimes: Extreme Fear, Fear, Neutral, Greed, and Extreme Greed.

**Note:** The trade dataset does not include an explicit leverage field. Where leverage-style segmentation was needed, **trade volume (Size USD) is used as a practical proxy** for position aggressiveness.

---

## Methodology

Trades were grouped by sentiment classification to compare win rate, average PnL, trade frequency, position size, and long/short balance across regimes. Accounts were further segmented by trade volume, trading frequency, and profitability to identify distinct trader behaviors. A correlation analysis and Random Forest classifier were used to test which features actually predict trade outcomes, and K-Means clustering was applied to group accounts into behavioral archetypes.

## Key Findings

### Performance across sentiment regimes
Extreme Greed is where traders perform best overall — the highest win rate (46.5%) and highest average profit per trade ($67.89). Fear days generate the highest *total* profit, but that's a volume effect (61,837 trades) rather than a quality effect — average PnL per trade in Fear ($54.29) trails Extreme Greed. Extreme Fear is the weakest regime on nearly every metric (37.1% win rate, $34.54 avg PnL).

### Behavioral shifts by sentiment
- **Frequency:** Traders are most active during Fear (61,837 trades), more so than during either extreme.
- **Position size:** Traders take their *largest* average positions during Fear ($7,816) and *smallest* during Extreme Greed ($3,112) — the inverse of what the win-rate data would justify.
- **Directional bias:** Buy/sell ratios stay fairly balanced across all regimes (e.g., Fear: 30,270 buys vs. 31,567 sells), so sentiment shifts activity and sizing more than directional bias.

### Trader segments
| Segment | Result |
|---|---|
| High vs. Low Volume | $48.48 vs. $49.82 avg PnL/trade — negligible difference; size doesn't buy skill |
| Frequent vs. Infrequent | $42.49 vs. $96.94 avg PnL/trade — infrequent traders earn more than double per trade |
| Winners vs. Losers | 95.6% of trades sit under net-winning accounts vs. 4.4% under net-losing accounts |

### Correlation analysis
Trade size correlates strongly with fees (r = 0.75) but only weakly with profit (r = 0.12) — larger trades reliably cost more without reliably paying off more.

### Predictive model
A Random Forest classifier predicting trade Win/Loss from sentiment, size, fee, and execution price achieved **85% accuracy** (F1: 0.87 losses, 0.81 wins). Execution Price (44.3%), Fee (25.5%), and Size USD (24.4%) drove most of the predictive power, while sentiment alone contributed only ~5.7% — suggesting sentiment shapes *behavior* more than it directly determines trade-level *outcomes*.

### Trader archetypes (K-Means clustering)
Clustering accounts by PnL, volume, trade count, fees, and win rate surfaced three distinct behavioral groups:
- **Selective High-Impact Traders:** Low trade count (~1,695) but the highest average PnL per trade ($290.01) and win rate (40.8%) — quality over quantity.
- **High-Volume Whales:** Comparable trade count to the baseline group but ~10x the total volume ($219.8M) and far higher fees per trade ($5.85 avg), without a meaningfully better win rate.
- **Steady Volume Traders:** The largest group by count, with moderate PnL ($32.95/trade), moderate volume, and the lowest average fees.

## Strategy Recommendations

**1. Reduce position size during Fear regimes.** Fear is where traders size up the most despite a middling win rate, and size predicts fees far more reliably than profit. A practical rule: cap trade size near the Neutral-day average rather than scaling up during Fear.

**2. Favor selective, high-conviction trades over frequency — especially during Extreme Greed.** Infrequent traders earn more than double the per-trade PnL of frequent traders, and Extreme Greed is the highest-quality regime overall. Rather than trading more often, the data supports fewer, larger, more deliberate trades during this regime.

## Conclusion

Market sentiment shapes not just how much traders trade, but how well they trade. Fear days see the highest activity and largest position sizes, yet only middling win rates, while Extreme Greed — despite lower activity — delivers the best win rate and highest per-trade profit. Traders currently behave in the opposite direction of what the data supports: sizing up in their weaker regime and sizing down in their stronger one. The clearest takeaway is that discipline beats activity — selective, lower-frequency trading consistently outperforms high-frequency trading, and aligning position size with actual regime quality (rather than emotional or habitual responses to sentiment) is the central opportunity this analysis surfaces.

## Files

- `analysis.ipynb` — full notebook: data preparation, exploratory analysis, sentiment comparison, segmentation, predictive model, and clustering
- `fear_greed_index.csv` — Bitcoin sentiment dataset
- `historical_data.csv` — Hyperliquid trade dataset
- `README.md` — this file

<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:2c5364,100:0f2027&height=100&section=footer" />
</p>
