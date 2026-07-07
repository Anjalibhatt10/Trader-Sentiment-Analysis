# Trader Behavior Analysis Report

## Methodology

Two datasets were used:

- Fear & Greed Index
- Historical Trader Dataset

The datasets were cleaned, missing values and duplicates were checked, date columns were converted into datetime format, and both datasets were merged using the common date column.

Exploratory Data Analysis (EDA) was then performed to analyze trader performance under different market sentiments.

Several metrics including Closed PnL, Win Rate, Trade Size, Buy/Sell Ratio, Fees, and Trader Segmentation were analyzed using tables and visualizations.

---

## Key Insights

1. Trader profitability varies across different market sentiments.

2. Fear periods recorded higher trading activity compared to other sentiment categories.

3. High-volume and frequent traders generally achieved better average profitability.

4. Buy and Sell activity remained relatively balanced across market conditions.

5. Market sentiment can provide useful context for evaluating trading behavior.

---

## Strategy Recommendations

1. Consider using market sentiment as an additional signal when making trading decisions rather than relying on it alone.

2. Apply stricter risk management during periods of extreme market sentiment and adjust position sizes based on historical performance.

---

## Conclusion

This project demonstrates that combining market sentiment with historical trading data provides valuable insights into trader behavior. While sentiment alone does not determine profitability, it can be an important factor in developing data-driven trading strategies.