# ⚡ VOLT — Trading System Dashboard

> **Status:** The dashboard at [cryptocav.github.io/volt-trading-dash](https://cryptocav.github.io/volt-trading-dash/) is live and currently evolving to showcase **PRISM**, our active allocation engine. PRISM powers all current signals, which are posted daily on Telegram.

👉 Join the signal feed: [@volt\_signals](https://t.me/volt_signals)

---

## 🌀 PRISM — Precision Relative Investment Signal Model

**PRISM** is a lightweight, modular crypto allocation engine that intelligently allocates USDC into the strongest trending assets based on daily market momentum.
It is designed to outperform passive strategies like BTC buy-and-hold or staying flat by filtering out low-quality setups using trend, volatility, and market regime awareness.

---

## 🌐 About the Dashboard

The [VOLT Trading Dashboard](https://cryptocav.github.io/volt-trading-dash/) is the public-facing hub for this system. Initially built to visualize trading logs and benchmark performance, it will now evolve to:

* Highlight the **live PRISM signals**
* Display daily allocations with visual charts
* Compare historical performance vs BTC and flat USDC
* Archive past strategies and results
* Showcase config sweeps and PineScript exports

This site serves as a transparent window into the system’s logic, results, and improvements—with all signals traceable and reproducible from open-source code.

---

## 🚀 Features

* **Daily Scanning** of crypto symbols with trend + volatility filters
* **Momentum-Based Ranking** to find relative strength
* **Backtesting Engine** for historical performance vs BTC and flat
* **Weekly Parameter Sweeping** to retune strategy for current regime
* **Telegram Alerts** to send live allocation signals
* **Modular CLI Runner** to coordinate daily/weekly execution
* **Local OHLCV Caching** for efficient, low-latency data use

---

## 🧱 Project Structure

```
prism/
🖚️ runner.py              # Main CLI orchestrator
🖚️ scanner.py             # Daily scanning logic
🖚️ sweep.py               # Weekly parameter grid search
🖚️ backtest.py            # Historical simulation engine
🖚️ telegram.py            # Telegram alert sender
🖚️ utils.py               # Shared data/tools
🖚️ config.yaml            # Strategy configuration file
🖚️ .env                   # Telegram credentials
🖚️ data/                  # Cached OHLCV CSVs
🖚️ logs/                  # Allocation logs
```

---

## ⚙️ Setup

### 1. Clone the Repo

```bash
git clone https://github.com/cryptocav/prism.git
cd prism
```

### 2. Create a Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Add a `.env` File

```env
TELEGRAM_TOKEN=your_telegram_bot_token
TELEGRAM_CHAT_ID=@volt_signals
```

### 5. Define Your Strategy in `config.yaml`

```yaml
capital: 200
max_alloc: 5
interval: "1d"
momentum_window: 12
trend_span: 8
use_adx: false
use_volatility_filter: true
volatility_threshold: 0.07
market_strength_threshold: 0.15
start_date: "2024-01-01"
symbols:
  - BTCUSDT
  - ETHUSDT
  - SOLUSDT
  ...
```

---

## 📈 CLI Usage

### 🔍 Daily Scan (with Telegram)

```bash
python runner.py --daily
```

### 🔕 Daily Scan (no alert)

```bash
python runner.py --daily --no-alert
```

### ⟲ Weekly Parameter Sweep

```bash
python runner.py --weekly
```

### 🔕 Weekly Sweep (no alert)

```bash
python runner.py --weekly --no-alert
```

### 📊 Backtest Strategy

```bash
python runner.py --backtest --plot
```

---

## 🧠 How It Works

### Allocation Logic

Each day:

* Filter coins by:

  * Momentum > 0
  * Price > EMA(trend span)
  * ATR ratio < volatility threshold
* Apply market regime filter (e.g. >15% of coins must be trending)
* Rank by momentum
* Allocate capital equally to top N coins (max\_alloc)

### Sweep Logic

Each week:

* Run grid search over `momentum_window`, `trend_span`, `market_strength_threshold`, etc.
* Save results to CSV + JSON
* Select best config based on final capital
* Output to `best_config.yaml` and Telegram

### Backtest Logic

Simulate strategy over historical data vs:

* BTC buy-and-hold
* Staying flat in USDC

Tracks:

* Equity curve
* Sharpe ratio
* Max drawdown
* Volatility

---

## 📤 Telegram Alerts

Enable alerts by:

1. Creating a bot via @BotFather
2. Getting your chat ID
3. Adding to `.env`

```env
TELEGRAM_TOKEN=your_token
TELEGRAM_CHAT_ID=@volt_signals
```

Alerts include:

* Daily allocations
* Weekly sweep config winners

---

## 🗓️ Cron Job Examples

### Daily Scan at 10:00 UTC

```cron
0 10 * * * cd /path/to/prism && /path/to/python3 runner.py --daily
```

### Weekly Sweep on Sunday at 12:00 UTC

```cron
0 12 * * SUN cd /path/to/prism && /path/to/python3 runner.py --weekly
```

---

## 📚 Future Improvements

* ✅ PineScript exporter
* ✅ ADX and volatility filters
* ⏳ Dynamic allocation sizing (e.g. weighted by momentum)
* ⏳ Live price integration
* ⏳ Portfolio dashboard view (via Streamlit or Flask)
* ⏳ Automated `config.yaml` overwrite from `best_config.yaml`
* ⏳ Export to Google Sheets

---

## 🤝 Credits

Created by [@cavpatrol](https://github.com/cryptocav)
Strategy design + ops by Cav
