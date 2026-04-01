# Gold Situation Room — Full Spec
**Date:** 2026-04-01
**Owner:** Sam Cohen
**Goal:** The most comprehensive, obsessive gold market dashboard on the internet. One page. Everything. No fluff.

---

## Stack
- **Backend:** Python (FastAPI) — pulls & caches all data
- **Frontend:** Single HTML file with vanilla JS + Chart.js + TailwindCSS CDN
- **Hosting:** Deploy to Replit or Vercel (static export option)
- **Refresh:** Auto-refreshes key data every 60s (price), others cached hourly/daily

---

## Sections (top to bottom)

### 1. 🏆 PRICE COMMAND CENTER
- Live gold spot price (USD/oz) — large, prominent
- 24h change $ and %
- YTD change %
- All-time high vs current (% below ATH)
- Gold price in: USD, EUR, GBP, JPY, CNY, AUD, CHF, INR
- Intraday chart (1D, 5D, 1M, 3M, 1Y, 5Y, All toggle)

### 2. 📊 KEY RATIOS (the nerd panel)
- Gold/Silver ratio (current + 1Y chart)
- Gold/Oil ratio (barrels of oil per oz gold)
- Gold/S&P500 ratio
- Gold/Bitcoin ratio
- Gold/Copper ratio
- Gold vs DXY (Dollar Index) — inverse correlation chart
- Gold vs Real Yields (10Y TIPS) — inverse correlation chart
- Gold vs CPI (inflation)

### 3. 🏦 CENTRAL BANK TRACKER
This is the crown jewel. Table showing:
- Country | Total Reserves (tonnes) | Last Month Change | YTD Change | % of Total Reserves | Last Updated
- Sorted by total reserves descending
- Color code: green = buying, red = selling, gray = unchanged
- Key buyers to highlight: China (PBoC), India (RBI), Turkey, Poland, Czech Republic, Kazakhstan, Uzbekistan
- Key sellers to watch: Russia (when selling), Jordan, Qatar
- Net global CB buying pace (tonnes/month trailing 12M)
- Source: World Gold Council IMF IFS data

### 4. 📦 ETF FLOWS
- GLD total holdings (tonnes) — daily change
- IAU total holdings (tonnes) — daily change  
- PHYS, BAR, SGOL holdings
- Combined total ETF holdings chart (1Y)
- Weekly/monthly flow direction (net inflows/outflows)
- Source: World Gold Council ETF tracker, ETF provider sites

### 5. 🔮 FUTURES & POSITIONING
- COMEX open interest (contracts)
- COT Report — Net speculative positioning (Managed Money longs vs shorts)
- COT chart — last 52 weeks
- Backwardation/Contango indicator (spot vs futures spread)
- Source: CFTC weekly COT data

### 6. 📰 GOLD NEWS FEED
- Live news feed: last 20 gold-specific headlines
- Sources: Kitco, BullionVault, WGC blog, Reuters commodities, Bloomberg gold tag
- Each headline: source, timestamp, headline text, link
- Auto-refreshes every 5 min

### 7. 🌍 MACRO CONTEXT
- US 10Y real yield (TIPS) — gold's biggest driver
- DXY — dollar strength
- Fed Funds Rate (current + expectations)
- CPI YoY %
- M2 Money Supply growth
- Global debt-to-GDP
- Source: FRED API (free, no key needed for most)

### 8. ⛏️ MINING SNAPSHOT
- Top gold miners: GDX (ETF price), GOLD (Barrick/B), NEM (Newmont), AEM, AGI
- Each: price, % change, market cap, production oz/year, AISC (all-in sustaining cost)
- GDX/Gold ratio (miners vs metal — shows leverage)
- Source: yfinance

### 9. 🕰️ HISTORICAL CONTEXT
- Gold price adjusted for inflation (real price)
- Gold price at major historical events (Bretton Woods end 1971, Hunt Brothers 1980, 2008 crisis, 2020 COVID, current)
- "Days of global GDP" gold represents
- Average annual return by decade

---

## Data Sources & APIs

| Data | Source | API |
|------|---------|-----|
| Spot price | metals-api.com OR goldapi.io (free tier) | REST |
| Central bank reserves | World Gold Council goldhub | CSV download / scrape |
| ETF holdings | WGC ETF tracker + iShares API | Scrape/CSV |
| COT data | CFTC | CSV (weekly) |
| Macro data | FRED | REST (free, no key) |
| Miner prices | yfinance | Python lib |
| FX rates | exchangerate-api.com | Free tier |
| News | Kitco RSS + BullionVault RSS + WGC RSS | RSS feeds |

---

## Design
- Dark theme (Bloomberg terminal aesthetic — black background, green/gold accents)
- Dense but readable — no wasted whitespace
- Numbers update in real-time with subtle flash animation
- Mobile responsive (but desktop-first)
- No ads, no login, no fluff — pure data

---

## Deliverable
- Single `index.html` + `backend.py` (FastAPI)
- `requirements.txt`
- `README.md` with setup instructions
- Deploy script for Replit
- All data cached in `cache/` folder (JSON) to avoid hammering APIs

---

## Out of Scope (v1)
- User accounts
- Alerts/notifications (v2)
- Platinum/palladium (v2)
- Physical dealer premiums (v2)
