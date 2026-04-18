# CLAUDE.md

Unified Docker Compose launcher for all WayneBrain dashboard projects.

## Projects

| Service | Port | Project |
|---------|------|---------|
| quicken | 8000 | `../quicken2` |
| tradejournal | 8001 | `../tradejournal` |
| crypto | 8002 | `../CryptoDashboard` |
| ninja | 8003 | `../ninja_strat` |
| squeeze | 8004 | `../SqueezeDashboard` |
| sector | 8005 | `../SectorRelativeStrength` |
| arbitrage | 8006 | `../arbitrage` |
| insiders | 8007 | `../insiders` |
| landing | 80 | `./nginx` (landing page only) |

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

- `C:/Users/wayne/QUANT-SCIENCE/QSAutomate/data/qsconnect/database/` — shared DuckDB volume (squeeze, sector, crypto, insiders)
- `C:/Users/wayne/Documents/NinjaTrader 8/db/minute` — NinjaTrader data (ninja)
- MySQL volume `arbitrage-mysql` — managed by Docker (arbitrage)

## Notes

- Stop individual project docker-compose instances before running this to avoid port conflicts.
- Data files (SQLite, uploads) are bind-mounted from each project directory so data persists across rebuilds.
