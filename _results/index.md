---
layout: default
title: "📊 Strategy Results"
has_children: true
nav_order: 1
permalink: /results/
description: >
  View sweep-tested strategy configurations for the VOLT crypto trading engine — ranked by Sharpe, alpha vs HODL, PnL, and win rate.
---

# 📊 Strategy Results

Welcome to the strategy lab.  
Each config here has been sweep-tested using the VOLT engine on real market data — then ranked and published with:

- 📈 **Sharpe Ratio** – risk-adjusted return  
- 🚀 **Alpha vs HODL** – performance vs passive holding  
- 💰 **Net PnL** – actual profit in simulated equity  
- 🎯 **Win Rate** – trades closed in profit

The goal isn’t to chase perfect hindsight performance — it’s to find robust, filtered systems that beat buy-and-hold in real conditions.

---

## 🧠 How These Results Are Generated

Each config on this page is the outcome of:

1. A historical **backtest** using your chosen pair + timeframe  
2. A parameter **sweep** over SL/TP, EMAs, filters, and features  
3. A **postprocessing step** that ranks and selects the top performers  
4. An auto-generated [📈 PineScript]({{ "/pine/" | relative_url }}) that mirrors the logic  
5. A published `.json` and `.pine` file for full transparency

You can view the full [🧠 Build Log]({{ "/blog/" | relative_url }}) for each iteration, fix, or strategy change.

---

## 🔎 Interpreting the Results

These strategies are not high-frequency bots or prediction machines. They are:

- ✳️ Filter-based  
- 🐢 Low-trade-frequency  
- 🔁 One-position-at-a-time  
- ✅ Designed for clarity and sustainability

Look for strategies with strong alpha vs HODL, realistic drawdown, and 3+ trades minimum.

---

## 📂 Available Strategy Reports

You can explore each strategy below by symbol + timeframe:

- [BTCUSDT 15m – Apr 19, 2025]({{ "/results/btc_15m_20250419" | relative_url }})

More pairs and timeframes coming soon.

---

## 🛠 Related Tools

- [📈 PineScripts]({{ "/pine/" | relative_url }})  
- [🧠 Build Log]({{ "/blog/" | relative_url }})  
- [📬 Contact]({{ "/contact/" | relative_url }}) to suggest strategies or request symbols  
