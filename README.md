# SPY 0DTE Automated Options Execution Engine

An event-driven algorithmic trading engine engineered in Python to evaluate, filter, and execute intraday momentum breakout setups on SPY 0DTE (Zero Days to Expiration) contracts using live streaming data.

---

## Strategy & Logic

* **Confluence Signal Generation:** Combines a 9-period Exponential Moving Average (9 EMA) directional bias with Volume-Weighted Average Price (VWAP) dynamic standard deviation envelopes to pinpoint high-volume intraday breakouts.
* **Option Selection Logic:** Dynamically queries option chains to select contracts matching target delta criteria (0.30 - 0.50) while tracking implied volatility.
* **Automated Risk Controls:**
  * Strict percentage stop-losses based on real-time option bid degradation.
  * Trailing profit tiers calibrated to capture rapid contract price expansion while hedging against accelerated theta decay.
  * Daily drawdown circuit-breaker that halts all execution threads upon hitting maximum risk loss limits.

---

## System Architecture

```text
├── data/
│   ├── historical/          # Sample 1-minute OHLCV tick data
│   └── stream_handler.py    # WebSocket client for streaming market data
├── indicators/
│   ├── ema.py               # 9 EMA calculation module
│   └── vwap.py              # Volume-Weighted Average Price engine
├── execution/
│   ├── alpaca_client.py     # Alpaca REST API execution wrapper
│   └── ibkr_client.py       # Interactive Brokers TWS API gateway
├── strategy/
│   ├── engine.py            # Main evaluation and signal detection loop
│   └── risk_manager.py      # Stop-loss, trailing target, and max loss gates
├── .env.example
├── .gitignore
├── requirements.txt
└── run_bot.py               # Entry-point runner
```

---

## Tech Stack

* **Language:** Python 3.10+
* **APIs & Brokerages:** Alpaca Trade API, Interactive Brokers (TWS / ib_insync)
* **Libraries:** pandas, numpy, websockets, python-dotenv

---

## Quick Start

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/RAdeelAleem/spy-0dte-algo-engine.git](https://github.com/RAdeelAleem/spy-0dte-algo-engine.git)
   cd spy-0dte-algo-engine
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Configure environment:**
   ```bash
   cp .env.example .env
   ```
   Add your paper trading API credentials in `.env`.

4. **Run paper execution:**
   ```bash
   python run_bot.py --mode paper
   ```

---

## License
MIT License
