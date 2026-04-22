# Primetrade.ai — Analysis Write-Up
**Author:** Data Science Intern Assignment  
**Period Analyzed:** January 2024 – May 2025  
**Dataset:** Hyperliquid Trader Data + Bitcoin Fear/Greed Index

---

## 1. Methodology

### Data Sources
- **Fear/Greed Index:** Daily Bitcoin market sentiment score (0–100) with classification labels — Extreme Fear, Fear, Neutral, Greed, Extreme Greed.
- **Hyperliquid Trader Data:** 211,224 individual trade records across 32 unique accounts including execution price, trade size, direction, PnL, and fees.

### Data Preparation
1. Converted timestamps and aligned both datasets on a common daily `date` column.
2. Identified that trader data prior to 2024 was 80–100% sparse per month — analysis was restricted to **January 2024 onwards** for consistency.
3. Merged datasets using an inner join on `date`, resulting in **~196,854 trade-level rows** covering **~480 trading days**.
4. Dropped irrelevant columns: Transaction Hash, Order ID, Trade ID, Timestamp IST, Side, Start Position.

### Key Metrics Created
| Metric | Description |
|---|---|
| `is_win` | Boolean — trade PnL > 0 |
| `leverage` | Size USD / Start Position |
| `leverage_category` | Bucketed: Low, Medium, High, Very High |
| `win_rate_%` | % of winning trades per account |
| `avg_size_usd` | Average trade size per account |
| `num_trades_that_day` | Daily trade count |
| `daily_pnl` | Daily PnL per account |
| `long_short_ratio` | Daily long vs short trade ratio |
| `sentiment_group` | Simplified: Fear / Greed |
| `trader_type` | Frequent (≥3195 trades) / Infrequent |
| `winner_type` | Consistent Winner (win rate ≥39%) / Inconsistent |

---

## 2. Insights

### Insight 1 — Fear Days Drive Bigger Losses Despite Higher Activity
Traders place **~60% larger positions on Fear days** (~$7,800 USD) compared to Greed days (~$4,900 USD), and trade **~600 more times per day**. Yet when they lose on Fear days, average losses are **~$200 vs ~$155 on Greed days** — about 30% deeper. The increased activity and position sizing during fearful markets directly leads to larger drawdowns.

> **Chart support:** Average Position Size (Fear vs Greed) + Average Loss Size (Fear vs Greed)

---

### Insight 2 — Less Trading = More Profit
Infrequent traders (below median 3,195 trades) earn on average **~$101 USD per trade**, more than double the **~$45 USD** earned by frequent traders. This gap widens even further on Greed days — infrequent traders earn **~$125 USD** vs frequent traders' **~$41 USD**. Overtrading appears to hurt returns through impulsive decisions and accumulated fees.

> **Chart support:** Avg PnL Frequent vs Infrequent + Frequency vs Sentiment breakdown

---

### Insight 3 — Low Leverage Wins Overall, But High Leverage Has a Place on Fear Days
Low leverage traders (1–2x) average **~$52 USD PnL** vs Very High leverage (10x+) at **~$43 USD** — confirming that more leverage doesn't mean more profit overall. However, on **Fear days specifically**, Very High leverage traders outperform (~$56 vs ~$50 USD). On **Greed days**, Low leverage clearly dominates (~$44 vs ~$35 USD). Sentiment context matters for leverage decisions.

> **Chart support:** Avg PnL by Leverage Category + Leverage Performance by Sentiment

---

### Bonus Insight — Win Rate is Unaffected by Sentiment
Both Fear and Greed days show an identical win rate of **~41%** — below the 50% threshold. This means sentiment does not influence how often traders win or lose. The real differentiator between Fear and Greed days is **loss magnitude**, not win frequency.

> **Chart support:** Win Rate on Fear vs Greed Days

---

## 3. Strategy Recommendations

### Strategy 1 — "On Fear Days: Slow Down, Size Down"
> *During Fear days, reduce position size by at least 30% and avoid increasing trade frequency.*

**Why:** Fear days consistently show larger position sizes, more trades, and deeper losses. Traders who behave reactively during Fear — trading more and betting bigger — end up with the worst outcomes. Capital preservation should be the priority.

**Applies most to:** Frequent traders and Very High leverage traders — these two segments are hurt the most during Fear.

---

### Strategy 2 — "On Greed Days: Stay Disciplined, Trade Selectively"
> *During Greed days, stick to low leverage (1–2x) and trade infrequently but with conviction.*

**Why:** On Greed days, infrequent traders earn ~3x more than frequent traders (~$125 vs ~$41 USD). Low leverage outperforms high leverage on Greed days. The data suggests that patience and discipline — not aggression — is what actually capitalizes on favorable market conditions.

**Applies most to:** All trader segments, but especially high-frequency and high-leverage traders who currently underperform on Greed days.

---

## 4. Summary Table

| Question | Finding |
|---|---|
| Does PnL differ by sentiment? | Slightly higher on Fear days, but losses are 30% deeper |
| Does win rate differ by sentiment? | No — identical ~41% on both |
| Do traders change behavior? | Yes — more trades and bigger sizes on Fear days |
| Best performing segment? | Infrequent + Low leverage traders |
| Worst performing segment? | Frequent + High leverage traders on Greed days |
| Best sentiment for trading? | Greed days with disciplined strategy |

---

*Analysis period: January 2024 – May 2025 | 32 unique trader accounts | ~196,854 trades*
