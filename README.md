# WayneBrain

One `docker compose up` starts all dashboards. Visit `http://localhost` for the landing page.

## Quick Start

```bash
docker compose up -d
```

Then open http://localhost.

## Dashboards

| Dashboard | URL | Description |
|-----------|-----|-------------|
| Quicken2 | http://localhost:8000 | Personal finance — accounts, transactions, QIF import |
| Trade Journal | http://localhost:8001 | Trading performance tracking across brokers |
| Crypto Dashboard | http://localhost:8002 | Crypto portfolio and transaction history |
| Ninja Strat | http://localhost:8003 | NinjaTrader strategy analysis and backtesting |
| Squeeze Dashboard | http://localhost:8004 | TTM Squeeze, momentum signals, unusual options |
| Sector Relative Strength | http://localhost:8005 | Sector rotation and relative strength rankings |
| Arbitrage | http://localhost:8006 | Walmart/Amazon price gap and arbitrage opportunities |
| Insider Watch | http://localhost:8007 | Insider buys — politicians (STOCK Act) and executives (Form 4) |

## Requirements

- Docker Desktop
- Host paths that must exist:
  - `C:/Users/wayne/QUANT-SCIENCE/QSAutomate/data/qsconnect/database/` — DuckDB files for squeeze, sector, crypto, insiders (`qsconnect.duckdb`, `options.duckdb`, `hsi.duckdb`, `insider.duckdb`)
  - `C:/Users/wayne/Documents/NinjaTrader 8/db/minute` — NinjaTrader minute data

## Commands

```bash
# Start everything
docker compose up -d

# Restart a single service (picks up env/config changes)
docker compose up -d squeeze

# Rebuild after code changes
docker compose up -d --build tradejournal

# Stop everything
docker compose down

# View logs
docker compose logs -f tradejournal
```
