# market-research

A static market monitoring site for daily tracking of:
- Semiconductor
- AI compute
- Energy
- Gold

## Features

- Multi-source quote ingestion with fallback chain:
  - Yahoo Finance
  - Alpha Vantage (optional API key)
  - CN fallback feed (limited symbols)
- Snapshot modes:
  - intraday
  - post_close
- Configurable alert rules by snapshot mode:
  - daily move threshold
  - breakout window
  - volume spike multiple
- Digest generation with multi-source headlines:
  - Google News RSS
  - Yahoo Finance RSS
  - CN RSS proxy source
- Feishu webhook notification:
  - idempotency key guard
  - retry with exponential backoff

## Structure

- `scripts/update_market_watch_data.py`: data pipeline
- `market_watch/`: static web app
- `.github/workflows/sync-market-watch.yml`: scheduled CI sync
- `.vscode/tasks.json`: local run tasks
- `.env.example`: environment variables template

## Quick Start

1. Create virtual environment and install dependencies (none required beyond Python stdlib currently).
2. Configure env vars from `.env.example`.
3. Run local dry-run:

```powershell
.\.venv\Scripts\python.exe .\scripts\update_market_watch_data.py --snapshot-type intraday --skip-news --request-timeout 6 --dry-run
```

4. Run full update:

```powershell
.\.venv\Scripts\python.exe .\scripts\update_market_watch_data.py --snapshot-type intraday
```

5. Open the static page:

- `market_watch/index.html`

## Notes

- For Feishu notifications, set `FEISHU_MARKET_WEBHOOK`.
- Alert thresholds are in `market_watch/alert_rules.json`.
