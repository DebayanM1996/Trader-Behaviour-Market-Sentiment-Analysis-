# Trader-Behaviour-Market-Sentiment-Analysis
Data analysis project exploring how market sentiment (Fear–Greed Index) influences trader activity, profitability, and behavior using historical trading data and Power BI visualization.
---

## Background and Overview  
The objective was to explore how **market sentiment (Fear–Greed Index)** influences **trader behavior and performance** using historical trading data from the Hyperliquid platform.

By combining trade-level performance metrics with market sentiment, the project aimed to identify behavioral patterns such as whether traders act more aggressively or cautiously during varying market conditions.

**Datasets used:**
1. **Bitcoin Market Sentiment (Fear–Greed Index)** – Daily sentiment classification and score.
2. **Historical Trader Data (Hyperliquid)** – Transaction-level execution records with price, size, PnL, and fees.

---

## Data Structure
After cleaning and aggregation, both datasets were joined and merged into a **daily-level analytical view**.  
Each record represents one trading day with summarized performance metrics and its corresponding market sentiment.

| Column | Description |
|---------|-------------|
| `date` | Trading date (daily level) |
| `total_trades` | Number of trades executed on that day |
| `unique_accounts` | Distinct active traders |
| `total_volume_usd` | Total traded volume in USD |
| `total_size_tokens` | Total token quantity traded |
| `avg_exec_price` | Average trade execution price |
| `sum_fee` | Total transaction fees |
| `sum_closed_pnl` | Aggregate realized profit/loss |
| `pnl_per_trade` | Average profit/loss per trade |
| `buy_sell_ratio` | Ratio of buy to sell trades |
| `volume_per_trade` | Average trade volume |
| `fg_value` | Fear–Greed Index score (0–100) |
| `fg_class` | Sentiment label – Fear, Neutral, Greed |
| `fg_score_0_1` | Normalized sentiment score (0–1) |
| `is_greed` | Boolean flag for Greed/Extreme Greed days |

---

## Derived / Feature-Engineered Columns
| Feature | Formula | Purpose |
|----------|----------|----------|
| `pnl_per_trade` | `sum_closed_pnl / total_trades` | Measures efficiency of trading activity |
| `buy_sell_ratio` | `buys / sells` | Detects trading bias toward buys or sells |
| `volume_per_trade` | `total_volume_usd / total_trades` | Indicates trade sizing trends |
| `fg_score_0_1` | Min-Max normalization of `fg_value` | Standardizes sentiment for numeric comparison |
| `is_greed` | True if `fg_class` in (“Greed”, “Extreme Greed”) | Binary indicator for optimistic market states |

---

## Data Preparation Notes
**Tools Used:**  
- Python (Pandas, NumPy) for data wrangling and aggregation  
- Power BI for visualization  

**Processing Workflow:**
1. Converted timestamps (`Timestamp`, `Timestamp IST`) to standardized `date`.  
2. Cleaned and converted numeric fields (`Execution Price`, `Size USD`, `Closed PnL`, `Fee`).  
3. Aggregated trade-level data into daily summaries (`groupby(date)`).  
4. Merged with Fear–Greed Index data on `date`.  
5. Normalized sentiment values (`fg_value` → 0–1 range).  
6. Exported the final dataset with sever rows (`cleaned_trader_sentiment.csv`) for Power BI dashboarding.

---

## Executive Summary
The analysis investigated how trader performance metrics respond to changing market sentiment.  
Key findings:

- **Higher trading activity during Greed phases:** total trades and volumes peak under optimistic sentiment.  
- **Improved efficiency during Fear phases:** fewer trades but higher average PnL per trade.  
- **Neutral days** display moderate activity and balanced buy/sell behavior.  

The behavioral trends align with market psychology — fear promotes discipline, while greed encourages over-trading i.e. negative sentiment encourages risk aversion, whereas positive sentiment leads to higher trading activity and potential overexposure.

---

## Deep Dive
<details>
<summary><strong>1. Volume and Sentiment Correlation</strong></summary>

Trading volume and number of trades were highest on “Greed” and “Extreme Greed” days, dropping significantly on “Fear” days — indicating lower confidence during pessimistic sentiment.
</details>

<details>
<summary><strong>2. Profitability Trends</strong></summary>

Average PnL per trade was highest during Fear days despite fewer trades.  
Traders appeared more selective and risk-averse, leading to improved trade quality.
</details>

<details>
<summary><strong>3. Buy/Sell Behavior</strong></summary>

The `buy_sell_ratio` exceeded 0.9 on Greed days, revealing bullish bias.  
During Fear phases, the ratio fell below 0.8, suggesting defensive positioning or reduced participation.
</details>

<details>
<summary><strong>4. Volatility Reflection</strong></summary>

Fluctuations in `avg_exec_price` and `volume_per_trade` mirrored sentiment shifts, reinforcing that market emotion influences trade sizing and price dispersion.
</details>

---

## Conclusion
This project demonstrates how **emotional market sentiment directly impacts trading outcomes**.  
By converting granular trading logs into a sentiment-aligned daily view, it highlights measurable behavioral biases: over-trading in greed, discipline in fear, and neutrality in balanced markets.  

The workflow—from raw CSVs to a Power BI dashboard—illustrates practical end-to-end analytics: **data engineering, feature creation, insight generation, and visualization** for real-world decision-making.

