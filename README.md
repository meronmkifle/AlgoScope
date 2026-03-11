# AlgoScope · NinjaTrader Algo Portfolio Optimizer

> **Free, browser-based portfolio analysis for algorithmic futures traders.**  
> Upload your NinjaTrader or Tradovate trade exports, compare strategies side-by-side, and find the optimal allocation mix — all without sending your data anywhere.

<svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/></svg> **Live tool:** [https://algoscopepro.netlify.app/](https://algoscopepro.netlify.app/) *(or open `index.html` directly in any browser)*  
<svg xmlns="http://www.w3.org/2000/svg" width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="9" cy="21" r="1"/><circle cx="20" cy="21" r="1"/><path d="M1 1h4l2.68 13.39a2 2 0 0 0 2 1.61h9.72a2 2 0 0 0 2-1.61L23 6H6"/></svg> **Ready-made NinjaTrader strategies:** [ninjatraderalgos.com](https://ninjatraderalgos.com)

---

![AlgoScope Overview](https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Overview%20Page.png)

---

## The Problem This Solves

NinjaTrader is excellent for developing and analysing individual algorithms. You can backtest a single strategy, review its performance report, tweak parameters, and iterate. That part works well.

But the moment you're running two or more algos simultaneously — which most serious automated traders eventually do — NinjaTrader gives you no native way to answer the questions that actually matter at the portfolio level: How are these strategies interacting? Are they genuinely diversified, or are they all losing on the same days? If I have $50k to allocate, how much should go behind each one? What does my combined equity curve look like, and how bad could a drawdown get across the whole portfolio?

That gap is what AlgoScope was built to fill. It takes the trade exports you already have from NinjaTrader and lifts the analysis up to the portfolio level: correlations, combined drawdowns, optimal allocation, stress testing. Everything NinjaTrader's built-in reporting doesn't cover when you're running multiple strategies together.

---

## What It Does

Most traders run multiple automated strategies and have no way to know how they interact with each other — or how much capital to put behind each one. This tool answers that question.

Load your trade history CSVs, and the optimizer tells you:

- Which strategies are genuinely adding value versus overlapping each other
- What the best capital split would be according to 10 different mathematical methods
- How your portfolio would have performed in the worst conditions (Monte Carlo stress testing)
- Whether your chosen allocation actually holds up on data the optimizer hasn't seen (Walk-Forward Validation)

Everything runs in your browser. No account needed, no data sent anywhere, no cloud, no sign-up.

---

## How to Export Your CSV

### NinjaTrader
1. Open **NinjaTrader 8**
2. Go to **Account Performance**
3. Click the **Trades** tab *(important — not Executions or Orders)*
4. Right-click anywhere in the table → **Export to CSV**

### Tradovate
1. Log in to **Tradovate**
2. Go to **Account → History**
3. Click the **Orders** tab *(important — not Fills or Positions)*
4. Click **Export** → CSV

The tool auto-detects both formats. It also accepts NinjaTrader Performance Reports.

---

## Features

### <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></svg> Strategy Analysis — 30+ Metrics Per Strategy

Every uploaded strategy gets a full performance breakdown across returns, risk, drawdown, tail risk, and positioning.

![Strategy Analysis](https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Strategies%20Page.png)

- **Returns:** Total P&L, daily breakdown, win rate, average win/loss, profit factor
- **Risk-adjusted:** Sharpe ratio, Sortino ratio, Calmar ratio
- **Drawdown:** Max drawdown, max drawdown %, recovery factor
- **Tail risk:** Value at Risk (95% and 99%), CVaR / Expected Shortfall
- **Positioning:** Kelly Criterion (full, half, quarter), expectancy per trade
- **Distribution:** Skewness, kurtosis, Z-score, win/loss streaks
- **Time breakdown:** Performance by hour of day, day of week, monthly calendar heatmap

---

### <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><line x1="21" y1="12" x2="3" y2="12"/><line x1="21" y1="6" x2="3" y2="6"/><line x1="21" y1="18" x2="3" y2="18"/></svg> 10 Portfolio Optimisation Methods

The optimizer runs all 10 methods simultaneously and shows the result of each in a side-by-side comparison table. Click any row to instantly apply that allocation.

![Optimiser — Methods & Allocation](https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Optimiser%20Part%201%20.png)

| Method | What It Finds |
|---|---|
| **Max Sharpe** | Highest return per unit of risk |
| **Max Sortino** | Highest return relative to downside volatility only |
| **Max Calmar** | Best return-to-drawdown ratio |
| **Min Drawdown** | Allocation with the smallest worst-case loss |
| **Risk Parity** | Each strategy contributes equally to total portfolio volatility |
| **Half-Kelly Sizing** | Capital allocation based on each strategy's Kelly Criterion, scaled to 50% |
| **Max Expectancy** | Highest expected profit per trade |
| **Max Profit Factor** | Best ratio of gross profits to gross losses |
| **Equal Weight** | Neutral starting baseline — same size for everything |

Use the interactive sliders to manually fine-tune your allocation and watch portfolio metrics update in real time.

![Optimiser — Sliders & Live Metrics](https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Optimiser%20Part%202.png)

---

### <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M9 3H5a2 2 0 0 0-2 2v4m6-6h10a2 2 0 0 1 2 2v4M9 3v18m0 0h10a2 2 0 0 0 2-2v-4M9 21H5a2 2 0 0 1-2-2v-4m0 0h18"/></svg> Walk-Forward Validation

The most important feature for avoiding overfitting.

The optimizer trains on the first 70% of your data, then tests the resulting allocation on the remaining 30% — data it has never seen. If the Max Sharpe allocation still outperforms equal-weight on the test set, that's a signal the allocation is robust, not just fitted to historical patterns.

Results: Out-of-sample Sharpe, P&L, max drawdown, split date, and a clear **Robust / Review** verdict.

---

### <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="7.5" cy="7.5" r="1.5"/><circle cx="18.5" cy="5.5" r="1.5"/><circle cx="11.5" cy="11.5" r="1.5"/><circle cx="7.5" cy="16.5" r="1.5"/><circle cx="17.5" cy="17.5" r="1.5"/></svg> Efficient Frontier

A scatter chart showing every possible combination of your strategies across all allocation ratios. The x-axis is risk, the y-axis is return. Your current allocation and optimal points are highlighted, so you can see at a glance whether you're near the theoretical best.

![Efficient Frontier](https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Efficient%20Frontier%20Page.png)

---

### <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/></svg> Correlation Matrix

Daily correlation heatmap across all loaded strategies. Green means uncorrelated (good diversification), red means correlated (concentrated risk). Highlights the lowest-correlation pairs and flags any strategies that move too closely together.

![Correlation Matrix](https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Correlation%20Page.png)

---

### <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><polyline points="22 12 18 12 15 21 9 3 6 12 2 12"/></svg> Monte Carlo Simulation

Runs 1,000 random sequences of your historical trades to stress-test the portfolio. Shows P5, P25, P50, P75, P95 outcome bands — the realistic range of outcomes, not just the average.

![Monte Carlo Simulation](https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Monte%20Carlo%20Page.png)

---

### <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg> Risk Analysis

Deep dive into tail risk, Kelly sizing, and drawdown dynamics per strategy — including CVaR, VaR at 95%/99%, Z-score streak independence, and full Kelly / Half Kelly / Quarter Kelly position sizing.

![Risk Analysis](https://raw.githubusercontent.com/meronmkifle/AlgoScope/main/Risk%20Analysis%20Page.png)

Also includes:
- **Diversification Score** — how uncorrelated your strategies are (aim >60%)
- **Tail Risk & Portfolio CVaR** — on the worst 5% of trading days, what is your average loss?

---

## Who This Is For

- NinjaTrader algo traders running multiple strategies simultaneously
- Prop firm traders across multiple funded accounts
- Systematic traders evaluating whether their strategy mix is actually diversified
- Anyone building or scaling a multi-strategy futures portfolio

---

## <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="11" width="18" height="11" rx="2" ry="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg> Privacy

All CSV data stays in your browser. Nothing is uploaded to any server. There is no backend. No account, no login, no cloud storage. The tool works fully offline — download the HTML file and open it directly.

---

## <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M10 13a5 5 0 0 0 7.54.54l3-3a5 5 0 0 0-7.07-7.07l-1.72 1.71"/><path d="M14 11a5 5 0 0 0-7.54-.54l-3 3a5 5 0 0 0 7.07 7.07l1.71-1.71"/></svg> Partner Tools

The Partner Tools page inside the app lists trusted tools for futures traders. Affiliate quick-links are also available in the sidebar for one-click access while you work.

| Tool | Category | Highlight |
|---|---|---|
| [NinjaTrader](https://ninjatrader.com) | Trading Platform | Free futures commissions |
| [ninjatraderalgos.com](https://ninjatraderalgos.com) | Algo Strategies | Built by this team |
| [QuantVPS](https://www.quantvps.com/?via=136674) | VPS / Infrastructure | NinjaTrader-optimised |
| [FlowBots / Replikanto](https://flowbots.ninja/?wpam_id=461) | Trade Copier | Multi-account copier |
| [FTMO](https://trader.ftmo.com/?affiliates=ScGFVtpEMpmvzWBTVeba) | Prop Firm | Up to 90% profit split |
| [FTUK](https://ftuk.com/?ref=1091) | Prop Firm | UK-based prop firm |
| [Alpha Futures](https://app.alpha-futures.com/signup/Meron019421/) | Prop Firm | Futures-first prop firm |
| [TradingView](https://www.tradingview.com/?aff_id=136674) | Charting | Industry standard charts |
| [TraderSync](https://tradersync.com?ref=meron38) | Trade Journal | AI-powered journaling |
| [PropFirmMatch](https://www.propfirmmatch.com/?a_aid=trade42) | Prop Firm Finder | Compare all prop firms |
| [Tradovate](https://tradovate.com) | Futures Broker | Flat-rate commissions |
| [Rithmic](https://rithmic.com) | Data & Execution | Pro order routing |

Some links are affiliate links. Commissions help keep this tool free and ad-free. Only tools that are genuinely useful to futures traders are listed.

---

## <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="#00ff88" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 8h1a4 4 0 0 1 0 8h-1"/><path d="M2 8h16v9a4 4 0 0 1-4 4H6a4 4 0 0 1-4-4V8z"/><line x1="6" y1="1" x2="6" y2="4"/><line x1="10" y1="1" x2="10" y2="4"/><line x1="14" y1="1" x2="14" y2="4"/></svg> Support

If you find this tool helpful, consider buying me a coffee!

<a href="https://buymeacoffee.com/qhl34mcne4" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>

---

*Built by [ninjatraderalgos.com](https://ninjatraderalgos.com) · [GitHub](https://github.com/meronmkifle/AlgoScope)*
