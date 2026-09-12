---
title: "Optionscreener"
type: knowledge-source
status: draft
main_topic: "JvL Invest"
creator: "Erna"
maintainer: "Erna"
content_reviewer: "Jürgen"
section: "Options"
colorcode: "Blue"
tags:
  - MOC/Options
sources:
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Optionscreener.md"
source_file_id: "1AheAeV3MISdn9_PYi1oihjrJhqSBdvPh"
---

# Optionscreener

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

Title: Optionscreener 
Date: 2026-07-18 
Time: 08:11 
Source: Barchart


Type: [[03_Tags/JvL-Invest-Options|Option]], 
Market: Bullish, Bearisch, Range/Neutral

## Abstract:


### Barchart Default Screener Columns & Metrics to select options

When using the Barchart options screener (found under "Naked Put"), the speaker evaluates several default columns to gauge liquidity and trade viability:

- **Moneyness:** Negative moneyness indicates the trade is out-of-the-money (the strike price is lower than the current stock price).
    
- **Bid:** The amount buyers are willing to pay for the put option (the premium collected by the seller).
    
- **Break-Even Price:** Calculated as the strike price minus the bid premium received.
    
- **Liquidity Indicators:**
    
    - **Volume:** The number of contracts traded in the last session. High volume ensure quick order fills.
        
    - **Open Interest:** The total number of active, outstanding contracts. Strong open interest indicates an active market of participants to trade with.
        

### Custom Screener Filters ("The Ultimate Screener")

To narrow down options from roughly 800 results to a highly curated list, the speaker applies specific criteria across five main categories:

|**Filter Category**|**Specific Setting**|**Purpose / Rationale**|
|---|---|---|
|**Market Cap**|**Above $3 Billion**|Avoids highly volatile small-cap and micro-cap companies.|
|**Implied Volatility (IV)**|**Between 30% and 60%**|Balances the need for premium size against the risk of massive, adverse price swings.|
|**IV Rank**|**30% and Above**|Ensures option premiums are relatively high and expensive compared to the stock's historical pricing over the past year.|
|**Days to Expiration (DTE)**|**30 to 45 Days** (including weekly options)|Strikes a sweet spot for capturing fast time decay (theta) while leaving enough breathing room for the stock to recover if it moves.|
|**Security Type**|Add **ETFs**|Expands the search parameters beyond individual equities.|

### Technical Analysis Overlay

The speaker integrates Barchart's stock screener filters directly into the options tool to find high-quality, growth-oriented companies:

- **Barchart Technical Opinion:** Set to **"Buy" ratings for both short and medium-term timeframes**. This filters for underlying stocks with strong upward momentum based on a proprietary blend of 13 technical indicators (such as RSI, Bollinger Bands, and MACD).
    

### Key Execution Rules mentioned in the text:

- **Delta Range:** Target a **20 to 30 delta**. A 24 delta, for example, translates roughly to a 76% chance of the option expiring out-of-the-money (worthless), which is the primary goal.
    
- **Expected Move:** Look at the "Expected Move" tab (derived from at-the-money straddles). Ideally, the put strike price should be set **below the lower expected range bound** to minimize assignment risk.
