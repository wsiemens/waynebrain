# WayneBrain

One `docker compose up` starts all dashboards. Visit `http://localhost` for the landing page.

## Quick Start

```bash
docker compose up -d
```

Then open http://localhost.

## Projects

| Dashboard | URL |
|-----------|-----|
| Quicken2 | http://localhost:8000 |
| Trade Journal | http://localhost:8001 |
| Crypto Dashboard | http://localhost:8002 |
| Ninja Strat | http://localhost:8003 |
| Squeeze Dashboard | http://localhost:8004 |
| Sector Relative Strength | http://localhost:8005 |

## Requirements

- Docker Desktop
- The following paths must exist on the host:
  - `C:/Users/wayne/QUANT-SCIENCE/QSAutomate/data/qsconnect/database/` (for squeeze, sector, crypto)
  - `C:/Users/wayne/Documents/NinjaTrader 8/db/minute` (for ninja_strat)

## Rebuild after code changes

```bash
docker compose up -d --build
# or for a single service:
docker compose up -d --build tradejournal
```

## Stop

```bash
docker compose down
```
