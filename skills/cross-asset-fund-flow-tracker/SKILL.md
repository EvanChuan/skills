---
name: cross-asset-fund-flow-tracker
description: Automate cross-asset fund flow analysis by tracking ETF flows, CFTC COT positioning, institutional views, and price momentum across 16 asset classes. Use when analyzing: (1) Where capital is flowing across markets, (2) Multi-asset investment strategies, (3) Risk-on vs risk-off sentiment, (4) Sector rotation signals, or (5) Validation of market trends through triple-confirmation (ETF flows + COT positioning + institutional ratings).
---

# Cross-Asset Fund Flow Tracker

Automated system tracking capital flows across 16 asset classes using triple-confirmation: ETF flows (現貨), CFTC COT positioning (期貨), and institutional views (戰略配置).

## Core Workflow

### Step 1: Confirm Parameters

Establish tracking period with user:
- 1 week: Past 5-7 trading days
- 1 month: Past 20-30 trading days  
- 3 months: Past 60-90 trading days

Default: Track all 16 asset classes unless user specifies subset.

### Step 2: Query Data Sources

For each asset, gather four data points in parallel:

**2.1 ETF Fund Flows**
- **Sources**: ETFdb.com → Morningstar → Issuer websites (iShares/Vanguard/State Street)
- **Search**: `[ticker] fund flows` (e.g., "QQQ fund flows")
- **Extract**: 1-week, 1-month, 3-month net flows
- **Score**: +2 (>$1B inflow), +1 ($0-1B), 0 (neutral), -1 ($0-1B outflow), -2 (<-$1B)

**2.2 Price Momentum**
- **Sources**: Yahoo Finance / TradingView
- **Extract**: 1-week, 1-month, 3-month % changes
- **Score**: +2 (strong uptrend), +1 (uptrend), 0 (sideways), -1 (downtrend), -2 (strong downtrend)

**2.3 CFTC COT Positioning** (for assets with futures contracts)
- **Sources**: Barchart COT → COT Base → CFTC official
- **Focus**: Non-Commercial (large speculators) net long changes over 2-3 weeks
- **Score**: +0.5 (consecutive increases), 0 (neutral), -0.5 (consecutive decreases)
- **Contrarian Check**: Compare Non-Commercial vs Non-Reportable (retail) positioning

**2.4 Institutional Views**
- **Sources**: PIMCO/JP Morgan/BlackRock quarterly outlooks
- **Search**: `[Institution] Asset Allocation Outlook 2026`
- **Extract**: OW/N/UW ratings, convert to +1/0/-1, average across 3 institutions
- **Score**: Range from +2 (all OW) to -2 (all UW)

### Step 3: Calculate Fund Temperature Score

Apply weighted formula:
```
Score = (ETF Flow × 0.35) + (Price Momentum × 0.25) + (Institutional View × 0.25) + (COT Signal × 0.15)
```

Round to: -2, -1.5, -1, -0.5, 0, +0.5, +1, +1.5, +2

**Reliability Assessment**:
- ⭐⭐⭐⭐⭐ High: All 3-4 sources align
- ⭐⭐⭐⭐ Medium-High: 2-3 sources align  
- ⭐⭐⭐ Medium: Conflicting signals
- Flag contradictions (e.g., ETF inflow + COT outflow + Institution UW)

### Step 4: Generate Report

Output structured markdown with these sections:

1. **Asset Flow Summary Table** - All 16 assets with scores in single table
2. **Top 5 Hot Assets** (Score ≥ +1.5) - With driving factors
3. **Top 5 Cold Assets** (Score ≤ -0.5) - With risk factors
4. **COT Sentiment Dashboard** - Large speculator extremes
5. **Institutional Consensus** - Cross-institution agreement/divergence
6. **Market Implications** - Taiwan/Asia investment insights (5 points)

## Default Asset Universe

| Asset Class | ETF | COT Contract | Characteristics |
|---|---|---|---|
| US Tech | QQQ | NQ | Growth, AI, mega-cap |
| US Value | VTV | - | Defensive, dividends |
| US Small Cap | IWM | RTY | Domestic, cyclical |
| Global Ex-US | ACWX | - | International diversification |
| Investment Grade Bonds | AGG | - | High-quality fixed income |
| High Yield Bonds | HYG | - | Credit risk premium |
| 10Y Treasury | IEF | TY | Risk-free benchmark |
| Cash | SHV | - | Opportunity cost gauge |
| Gold | GLD | GC | Safe haven, inflation hedge |
| Silver | SLV | SI | Industrial + precious metal |
| Crude Oil | USO | CL | Energy, inflation |
| Copper | COPX | HG | Industrial demand leading indicator |
| Bitcoin | IBIT | BTC | Digital asset, risk-on |
| REITs | VNQ | - | Real estate, rate-sensitive |
| US Dollar | DXY | DX | Reserve currency |
| Japanese Yen | FXY | JPY | Safe haven currency |

**Asset Adjustment**: Users may add (e.g., EMB, VGK) or focus on subsets (e.g., "only commodities and safe havens").

## Advanced Features

**Week-over-Week Tracking**: Compare current vs previous scores, flag fastest movers (temperature change > ±1).

**Contradiction Alerts**: Auto-flag when:
- ETF inflow + COT outflow + Institution UW (potential false breakout)
- Retail buying + Smart money selling (possible top)
- All sources neutral but high volatility (uncertainty regime)

**Custom Asset Lists**: Flexibly add/remove assets or filter to COT-only assets.

## Enhanced Analysis (When Needed)

For deeper institutional positioning insights or signal validation, see:
- **references/advanced-data-sources.md** - 7 additional data layers including:
  - SEC 13F institutional holdings tracking
  - Dark pool trading analysis
  - Unusual options activity (UOA)
  - Gamma Exposure (GEX) and options market maker positioning
  - VIX futures term structure
  - Fed Z.1 Flow of Funds report
  - Repo market and money market fund flows

**When to Load**: User requests "hedge fund positions", "dark pools", "options flow", or when core signals show major conflicts requiring tiebreakers.

**Integration**: Advanced sources add 30% weight to final score (Core 70% + Advanced 30%), significantly boosting reliability ratings when all layers align.

## Data Source Quick Reference

- **ETF Flows**: etfdb.com, morningstar.com/fund-flows, issuer websites
- **CFTC COT**: cftc.gov/CommitmentsofTraders, barchart.com/futures/commitment-of-traders, cotbase.com
- **Institutions**: pimco.com/insights, am.jpmorgan.com, ishares.com/us/insights
- **Prices**: finance.yahoo.com, tradingview.com

## Limitations

1. **Data Lag**: ETF flows (1-2 days), COT (3 days), Institution views (quarterly)
2. **Coverage**: Not all assets have COT futures (e.g., VTV, AGG, HYG)
3. **Black Swans**: Even high-reliability signals can fail during sudden events
4. **Not Investment Advice**: Framework only; combine with risk management

**Report Frequency**: Weekly updates recommended (aligned with COT release schedule).
