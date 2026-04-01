# Gold Situation Room

A fully static, Bloomberg-terminal-style gold market dashboard. No server required — deploys directly to GitHub Pages with automated hourly data updates via GitHub Actions.

## Architecture

```
index.html          Static single-page dashboard (reads data/*.json)
fetch_data.py       Python script that fetches all market data
data/*.json         Pre-fetched JSON data files (auto-updated hourly)
.github/workflows/  GitHub Actions workflow for data pipeline
```

**Data sources:**
- **Price & market data:** yfinance (Gold futures, Silver, Oil, S&P500, Bitcoin, DXY, Copper, ETFs, Miners)
- **Macro indicators:** FRED CSV endpoints (Real yields, DXY, CPI, Fed Funds, M2, 10Y yield)
- **News:** RSS feeds (Kitco, BullionVault)
- **Central banks:** WGC/IMF IFS compiled data (updated quarterly in code)
- **COT positioning:** CFTC disaggregated futures data

No API keys required.

## Deploy to GitHub Pages

1. **Push to GitHub** — push this repo to a GitHub repository

2. **Enable GitHub Pages:**
   - Go to **Settings > Pages**
   - Under "Source", select **Deploy from a branch**
   - Branch: `main`, folder: `/ (root)`
   - Click **Save**

3. **Enable Actions permissions:**
   - Go to **Settings > Actions > General**
   - Under "Workflow permissions", select **Read and write permissions**
   - Click **Save**

4. **Run the first data fetch:**
   - Go to **Actions** tab
   - Click **Fetch Gold Data** workflow
   - Click **Run workflow** button
   - Wait for it to complete — this populates the `data/` directory

5. Your dashboard is now live at `https://<username>.github.io/<repo>/`

## How it works

- **GitHub Actions** runs `fetch_data.py` every hour (on the hour)
- The script fetches fresh market data and writes JSON files to `data/`
- Actions commits and pushes the updated JSON files
- The static `index.html` loads these JSON files via `fetch()` and renders the dashboard
- The page auto-refreshes data every 5 minutes (just reloads JSON, not the whole page)
- A manual **Refresh** button in the header triggers an immediate data reload

## Manual data refresh

### From GitHub (trigger Actions)
1. Go to **Actions** > **Fetch Gold Data**
2. Click **Run workflow**

### Locally
```bash
pip install -r requirements.txt
python fetch_data.py
# Open with a local server (needed for fetch() to work):
python -m http.server 8000
# Visit http://localhost:8000
```

## Sections

1. **Price Command Center** - Gold spot + gradient area chart + multi-currency grid with sparklines + ATH progress bar
2. **Key Ratios** - Gold/Silver, Gold/Oil, Gold/SPX, Gold/BTC, Gold/Copper with gauge dials + sparklines
3. **Central Bank Tracker** - Heat map table + top 15 bar chart + buying pace
4. **ETF Flows** - GLD/IAU/PHYS/BAR/SGOL overlaid area charts + tonnage cards
5. **COT Positioning** - 52-week stacked bars + percentile gauge
6. **News Feed** - Kitco + BullionVault RSS with sentiment dots
7. **Macro Context** - Real yields, DXY, Fed Funds, CPI, M2, 10Y + dual-axis correlation charts
8. **Mining Snapshot** - AISC bar chart + margin table + miner sparklines
9. **Historical Context** - Annotated timeline chart + decade return bars + event cards

## Data files

| File | Contents |
|------|----------|
| `data/price.json` | Gold spot price, multi-currency, intraday/historical charts |
| `data/ratios.json` | Gold/Silver, Gold/Oil, Gold/SPX, Gold/BTC, Gold/Copper ratios |
| `data/central_banks.json` | Central bank reserves, buying/selling activity |
| `data/etfs.json` | GLD, IAU, PHYS, BAR, SGOL prices and charts |
| `data/macro.json` | Real yields, DXY, CPI, Fed Funds, M2, 10Y yield from FRED |
| `data/miners.json` | GDX, Barrick, Newmont, Agnico Eagle, Alamos Gold |
| `data/news.json` | Latest gold news from RSS feeds |
| `data/cot.json` | CFTC Commitments of Traders positioning data |
| `data/historical.json` | Historical gold events, decade returns, full timeline |
