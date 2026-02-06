# Advanced Data Sources for Fund Flow Analysis

This reference provides detailed guidance on seven additional data layers beyond the core ETF/COT/Institution framework. Load this file when users request deeper institutional positioning insights or multi-layer validation.

## When to Use This Reference

- User asks about "hedge fund positioning" or "smart money"
- Need to resolve conflicting signals across core data sources
- User requests "dark pool" or "options flow" analysis
- Investigating unusual market behavior or potential manipulation
- Deep-dive analysis on specific assets showing signal divergence

---

## Layer 1: SEC 13F Institutional Holdings

**What**: Quarterly filings disclosing long equity positions of institutions managing >$100M.

**Key Insight**: Reveals what Berkshire, Bridgewater, Tiger Global, etc. are buying/selling with 45-day lag.

### Data Sources
- **WhaleWisdom**: https://whalewisdom.com - Best aggregation and comparison tools
- **13F Pro**: https://www.13fpro.com - Track specific managers
- **SEC Edgar**: https://www.sec.gov/cgi-bin/browse-edgar?action=getcompany&type=13F - Raw filings

### Workflow
1. Search for target ETF ticker (e.g., "QQQ 13F holdings")
2. Compare quarter-over-quarter changes in shares held by top 10 institutions
3. Calculate net institutional buying: (New Shares - Old Shares) / Old Shares
4. Flag significant moves: >10% change by top holders or major new positions

### Scoring
- Strong Accumulation (>5 major funds increasing >20%): +1
- Moderate Accumulation: +0.5
- No Change: 0
- Distribution (-5 to -10% aggregate): -0.5
- Heavy Distribution (<-10% or major exits): -1

### Limitations
- **Lag**: 45 days after quarter-end
- **Coverage**: Only long positions, no shorts/options/futures
- **ETF caveat**: Most institutions don't file 13F for ETF holdings (track underlying holdings instead)

---

## Layer 2: Dark Pool Trading Data

**What**: Off-exchange block trades executed by institutions to minimize market impact.

**Key Insight**: Large accumulation/distribution that doesn't show up in public order books.

### Data Sources
- **Finra ATS (Alternative Trading System) Data**: https://www.finra.org/finra-data/browse-catalog/alternative-trading-system-data
- **TradingView Dark Pool Indicator**: Built-in indicator showing block trades
- **Bookmap**: https://bookmap.com - Real-time dark pool print visualization

### Workflow
1. Monitor dark pool print volume as % of total daily volume
2. Analyze print sizes: >$1M prints = institutional, >$10M = major positioning
3. Compare dark pool volume trend (5-day MA) vs public volume
4. Check for "sweeps" - multiple dark pool prints in same direction within minutes

### Scoring
- Dark Pool Volume >40% + Large Prints Bullish: +0.5
- Dark Pool Volume 30-40%: 0
- Dark Pool Volume >40% + Large Prints Bearish: -0.5

### Limitations
- **Delayed Reporting**: Dark pool data released next day
- **Direction Ambiguity**: Can't always determine if prints are buys or sells
- **ETF Challenge**: Dark pool data less reliable for ETFs vs individual stocks

---

## Layer 3: Unusual Options Activity (UOA)

**What**: Large, directional options trades indicating informed positioning by institutions or insiders.

**Key Insight**: Options provide leverage and defined risk, often used by sophisticated players before major moves.

### Data Sources
- **Unusual Whales**: https://unusualwhales.com - Premium but comprehensive
- **FlowAlgo**: https://flowalgo.com - Real-time alerts
- **Barchart Unusual Options Activity**: https://www.barchart.com/options/unusual-activity - Free

### What to Track
1. **Large Premium Trades**: >$100K premium, especially in single prints
2. **OTM Calls/Puts**: Out-of-money options suggesting directional bets
3. **Short-Dated Options**: <30 DTE = expecting move soon
4. **Call/Put Ratio**: Sustained shift >1.5 (bullish) or <0.5 (bearish)

### Workflow
1. Search "[Ticker] unusual options activity" daily
2. Flag trades with:
   - Premium >$500K
   - Volume >10x open interest
   - Aggressive "ask side" buying (willing to pay up)
3. Distinguish hedging vs speculation: Hedging often near ATM, speculation far OTM

### Scoring
- Multiple Large OTM Calls (Bullish Bets): +0.5
- Balanced Activity: 0
- Multiple Large OTM Puts (Bearish Bets): -0.5

### Limitations
- **Noise**: Many trades are hedges or spreads, not directional
- **Market Maker Hedging**: Can create feedback loops (gamma squeeze)
- **Requires Context**: Must combine with price action and volume

---

## Layer 4: Gamma Exposure (GEX)

**What**: Net options market maker exposure driving hedging flows that amplify or dampen market moves.

**Key Insight**: Positive GEX = market makers hedge by selling into rallies (dampens volatility). Negative GEX = buy rallies, sell dips (amplifies volatility).

### Data Sources
- **SpotGamma**: https://spotgamma.com - Institutional-grade GEX analytics (paid)
- **SqueezeMetrics**: https://squeezemetrics.com - DIX/GEX combo analysis
- **Zero Gamma Level**: Calculated from options OI across strikes

### Key Metrics
- **Absolute GEX**: Total gamma exposure (higher = more hedging activity)
- **GEX by Strike**: Identify support (call walls) and resistance (put walls)
- **Zero Gamma Level**: Price where GEX flips positive to negative

### Workflow
1. Check daily aggregate GEX for market (SPX, QQQ, IWM)
2. If GEX > +$3B: Expect range-bound, muted volatility
3. If GEX < -$1B: Expect volatility expansion, potential squeeze
4. Cross-reference with VIX futures term structure (see Layer 5)

### Scoring
- High Positive GEX (>$5B) + Calls OTM = Resistance Above: 0 (neutral, trapped)
- Negative GEX (<-$1B) + Price Above Zero Gamma = Squeeze Potential: +0.5
- Negative GEX + Price Below Zero Gamma = Crash Risk: -0.5

### Limitations
- **Complex Calculation**: Requires options chain data and delta/gamma modeling
- **Intraday Changes**: GEX shifts throughout the day as options expire
- **Better for Indices**: Individual ETFs have less options activity

---

## Layer 5: VIX Futures Term Structure

**What**: Shape of VIX futures curve indicating market stress expectations.

**Key Insight**: Contango (normal) = calm market. Backwardation (inverted) = fear/hedging demand.

### Data Sources
- **CBOE VIX Futures**: https://www.cboe.com/tradable_products/vix/vix_futures/
- **VIX Central**: https://vixcentral.com - Visual term structure tracker
- **TradingView VIX Futures Chart**: Compare M1 vs M2 vs M3 contracts

### Key Patterns
- **Steep Contango** (M1 < M2 by >10%): Market complacent, good entry for vol shorts
- **Flat Curve** (M1 ≈ M2): Neutral, watching
- **Backwardation** (M1 > M2): Near-term fear, defensive positioning rising

### Workflow
1. Calculate VIX M1-M2 spread daily
2. Track changes over 5 days (trend more important than absolute level)
3. Combine with CBOE Put/Call Ratio for sentiment confirmation

### Scoring
- Backwardation Increasing (Fear Rising): -0.5 (risk-off signal)
- Contango Stable: 0
- Steep Contango (Complacency): +0.5 (risk-on signal)

### Limitations
- **VIX ≠ Market Direction**: VIX can spike in both crashes and melt-ups (gamma squeeze)
- **Timing**: Early warnings but can stay "wrong" for weeks

---

## Layer 6: Fed Z.1 Financial Accounts (Flow of Funds)

**What**: Quarterly report tracking capital flows across all sectors of US economy.

**Key Insight**: Shows which sectors (households, corporates, foreigners, Fed) are buying/selling financial assets.

### Data Sources
- **Fed Z.1 Release**: https://www.federalreserve.gov/releases/z1/
- **FRED Database**: https://fred.stlouisfed.org/release?rid=52 - Interactive data
- **Key Tables**:
  - L.223: Corporate Equities
  - L.209: Bonds and Credit Market Instruments
  - L.229: Mutual Funds and ETFs

### Workflow
1. Download quarterly Z.1 release (published ~10 weeks after quarter-end)
2. Focus on "Net Acquisition of Financial Assets" by sector
3. Track year-over-year changes in:
   - Household equity purchases (direct + funds)
   - Foreign holdings of US securities (TIC data)
   - Fed balance sheet changes (QE/QT)

### Scoring
- Household Equity Buying Accelerating (>20% YoY): +0.5
- Stable: 0
- Household Equity Selling or Foreign Outflows: -0.5

### Limitations
- **Extreme Lag**: 10 weeks old when released
- **Macro Level**: Doesn't specify which assets within categories
- **Use for Context**: Trend validation, not timing signals

---

## Layer 7: Repo Market & Money Market Funds

**What**: Short-term funding markets indicating liquidity stress or abundance.

**Key Insight**: Repo rate spikes = liquidity crunch (risk-off). Money market outflows = capital moving to risk assets.

### Data Sources
- **Fed Repo Operations**: https://www.newyorkfed.org/markets/desk-operations/reverse-repo
- **SOFR (Secured Overnight Financing Rate)**: Real-time repo benchmark
- **SEC Money Market Fund Flows**: https://www.sec.gov/data-research/statistics-data-visualizations/money-market-fund-statistics

### Key Metrics
- **Repo Rate Spread** (SOFR - Fed Funds): >20 bps = stress
- **Fed Reverse Repo Usage**: >$1.5T = excess liquidity (Fed draining)
- **Money Market Fund Assets**: Rising = flight to safety, Falling = risk-on

### Workflow
1. Check weekly Fed repo facility usage
2. Track money market fund 4-week rolling flows
3. Flag stress: Repo spreads >30 bps or MMF inflows >$100B/month

### Scoring
- MMF Outflows + Low Repo Rates = Risk-On: +0.5
- Neutral: 0
- MMF Inflows + Repo Stress = Risk-Off: -0.5

### Limitations
- **Systemic Indicator**: Better for market-wide risk, not individual assets
- **Fed Intervention**: Fed can suppress signals via emergency facilities

---

## Integration Strategy

When multiple advanced sources available, apply layered weighting:

**Enhanced Score Formula**:
```
Final Score = (Core Score × 0.70) + (Advanced Score × 0.30)

Where:
Core Score = ETF(0.35) + Price(0.25) + Institution(0.25) + COT(0.15)
Advanced Score = [13F(0.2) + Dark Pool(0.15) + Options(0.15) + GEX(0.1) + VIX(0.1) + Z.1(0.15) + Repo(0.15)]
```

**Reliability Boost**:
- 5+ sources align (same direction): ⭐⭐⭐⭐⭐
- 4 sources align: ⭐⭐⭐⭐
- 3 sources align: ⭐⭐⭐
- Major conflicts: Flag as "High Uncertainty - Avoid"

---

## Example: Multi-Layer Analysis

**Asset**: QQQ (Nasdaq-100 ETF)

| Layer | Signal | Score | Weight |
|---|---|---|---|
| ETF Flow | -$1.8B outflow | -2 | 0.35 |
| Price | -1.2% (1W) | -1 | 0.25 |
| Institution | Neutral | 0 | 0.25 |
| COT | -12K contracts | -0.5 | 0.15 |
| **Core Score** | | **-1.1** | **0.70** |
| 13F | Top 5 reduced 8% | -0.5 | 0.06 |
| Dark Pool | 45% of volume, bearish | -0.5 | 0.045 |
| Options | Heavy put buying | -0.5 | 0.045 |
| GEX | Negative GEX, below zero gamma | -0.5 | 0.03 |
| VIX | Backwardation forming | -0.5 | 0.03 |
| Z.1 | N/A (too lagged) | 0 | 0 |
| Repo | Neutral | 0 | 0.045 |
| **Advanced Score** | | **-0.5** | **0.30** |

**Final Score**: (-1.1 × 0.70) + (-0.5 × 0.30) = -0.77 - 0.15 = **-0.92 ≈ -1.0**

**Reliability**: ⭐⭐⭐⭐⭐ (9/10 sources bearish, only Institution neutral)

**Action**: Strong sell signal with very high confidence.

---

## Practical Limitations

1. **Data Overload**: Use advanced sources only when core signals conflict or user requests
2. **Diminishing Returns**: Beyond 5-6 sources, additional data rarely changes conclusion
3. **Cost**: Many premium sources (Unusual Whales, SpotGamma) require subscriptions
4. **Expertise Required**: Options/GEX analysis needs understanding of Greeks and hedging

**Recommendation**: Start with core 3-layer system. Add advanced sources when:
- User explicitly requests (e.g., "check dark pools")
- Core signals show major conflict (need tiebreaker)
- Asset showing extreme unusual behavior
- Deep-dive analysis for high-conviction positioning
