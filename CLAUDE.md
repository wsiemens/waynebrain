# CLAUDE.md

Unified Docker Compose launcher for all WayneBrain dashboard projects.

## Projects

| Service | Port | Project | Description |
|---------|------|---------|-------------|
| quicken | 8000 | `../quicken2` | Personal finance — accounts, transactions, QIF import |
| tradejournal | 8001 | `../tradejournal` | Trading performance tracking across brokers |
| crypto | 8002 | `../CryptoDashboard` | Crypto portfolio and transaction history |
| ninja | 8003 | `../ninja_strat` | NinjaTrader strategy analysis and backtesting |
| squeeze | 8004 | `../SqueezeDashboard` | TTM Squeeze, momentum signals, unusual options |
| sector | 8005 | `../SectorRelativeStrength` | Sector rotation and relative strength rankings |
| arbitrage | 8006 | `../arbitrage` | Walmart/Amazon price gap and arbitrage opportunities (Node.js + MySQL) |
| insiders | 8007 | `../insiders` | Insider buys — politicians (STOCK Act) and executives (Form 4) |
| landing | 80 | `./nginx` | Static landing page linking to all services |

## Commands

```bash
# Start everything
docker compose up -d

# Start a single service
docker compose up -d tradejournal

# Rebuild after code changes
docker compose up -d --build tradejournal

# Stop everything
docker compose down

# View logs
docker compose logs -f tradejournal
```

## Architecture

Each project has its own Dockerfile and is built from its sibling directory. The nginx `landing` service serves a static landing page at `http://localhost` linking to each project on its own port.

## External Dependencies

- `C:/Users/wayne/QUANT-SCIENCE/QSAutomate/data/qsconnect/database/` — shared DuckDB volume:
  - `qsconnect.duckdb` — squeeze, sector, crypto
  - `options.duckdb` — squeeze options tab
  - `hsi.duckdb` — squeeze HSI tickers
  - `insider.duckdb` — insiders
- `C:/Users/wayne/Documents/NinjaTrader 8/db/minute` — NinjaTrader data (ninja)
- Docker named volume `arbitrage-mysql` — MySQL persistence for arbitrage

## Notes

- Stop individual project docker-compose instances before running this to avoid port conflicts.
- Data files (SQLite, uploads) are bind-mounted from each project directory so data persists across rebuilds.
- `docker compose up -d <service>` recreates a running container if its config changed (env vars, volumes, image).
