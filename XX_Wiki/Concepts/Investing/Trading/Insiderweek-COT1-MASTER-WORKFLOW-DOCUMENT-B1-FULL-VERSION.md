---
title: "Insiderweek - COT‑1 MASTER WORKFLOW DOCUMENT (B1 FULL VERSION)"
type: knowledge-source
status: draft
main_topic: "JvL Invest"
creator: "Erna"
maintainer: "Erna"
content_reviewer: "Jürgen"
section: "Trading"
colorcode: "Blue"
tags:
  - MOC/Trading
sources:
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Insiderweek - COT‑1 MASTER WORKFLOW DOCUMENT (B1 FULL VERSION).md"
source_file_id: "1f6ImRvUZYcObr3toHzngic5etisBzsIh"
---

# Insiderweek - COT‑1 MASTER WORKFLOW DOCUMENT (B1 FULL VERSION)

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

#
[[insiderweek]] 
[[Futures]]
 

### _Weekly → Daily → Entry → Management → Exit — Full InsiderWeek Workflow_

### _Markdown Edition_

## # **1. WEEKLY ANALYSIS WORKFLOW**

## ## **1.1 COT Analysis — Institutional Positioning**

- Identify **Commercials** extreme net positions
    
- Identify **Large Speculators** confirming or contradicting direction
    
- Mark **COT signals** (Buy / Sell)
    
- Confirm multi‑week alignment
    
- Exclude markets with unclear COT structure
    

**Boundary Condition:**

- **No COT signal → Market excluded**
    

## ## **1.2 Weekly Trend Analysis — Structural Direction**

- Uptrend: **Higher Highs + Higher Lows**
    
- Downtrend: **Lower Highs + Lower Lows**
    
- Sideways: overlapping swings → exclude
    

**Boundary Condition:**

- **Weekly trend must match COT direction**
    

## ## **1.3 Seasonality — Time Window Confirmation**

- Identify seasonal windows (5y, 15y, 30y)
    
- Confirm seasonal direction matches COT + weekly trend
    
- Avoid trades near seasonal turning points
    
- Avoid weak seasonal windows
    

**Boundary Condition:**

- **Seasonality must support direction**
    

## ## **1.4 Relative Strength / Weakness — Market Selection**

- For long trades → strongest market
    
- For short trades → weakest market
    
- Exclude markets with unclear strength
    
- Confirm strength aligns with weekly trend
    

**Boundary Condition:**

- **Only strongest/weakest markets allowed**
    

## ## **1.5 Weekly Watchlist Creation**

A market enters the watchlist only if:

- COT signal
    
- Weekly trend
    
- Seasonality
    
- Relative strength
    

**ALL align in the same direction.**

**Boundary Condition:**

- **If one fails → market excluded**
    

# **2. DAILY ANALYSIS WORKFLOW**

## ## **2.1 Daily Trend Structure — Swing Logic**

- Identify short‑term highs/lows
    
- Identify medium‑term highs/lows
    
- Confirm daily trend direction
    
- Daily trend must be readable (no overlapping swings)
    

**Boundary Condition:**

- **Daily trend must be clean**
    

## ## **2.2 Daily Trend Change — Activation Trigger**

### **Long Trend Change**

- Formation of **Higher Low (HL)**
    
- Break of previous **short‑term high**
    

### **Short Trend Change**

- Formation of **Lower High (LH)**
    
- Break of previous **short‑term low**
    

**Boundary Condition:**

- **No trend change → NO trade**
    

## ## **2.3 Market Phase Identification**

- **Impulse phase** → impulse entry
    
- **Correction phase** → pullback entry
    

## ## **2.4 Entry Pattern Identification**

### **Impulse Entry**

- Enter with momentum
    
- Break of impulse candle high/low
    
- SL below/above impulse candle
    

### **Pullback Entry**

- Reversal candle required (Pin bar, Engulfing)
    
- Break of reversal candle high/low
    
- SL below/above reversal candle
    

**Boundary Condition:**

- **No entry pattern → NO trade**
    

# **3. ENTRY WORKFLOW**

## ## **3.1 Required Market Setup (ALL must be true)**

### **Directional Alignment**

- COT direction
    
- Weekly trend direction
    
- Seasonality direction
    
- Daily trend direction
    
- Relative strength direction
    

### **Technical Alignment**

- Daily trend change confirmed
    
- Entry pattern visible
    
- Market at key level (support/resistance)
    

### **Risk Alignment**

- SL defined
    
- TP defined
    
- Position size calculated
    
- Correlation check passed
    

**Boundary Condition:**

- **ALL conditions must align before entry**
    

## ## **3.2 Exact Entry Trigger**

### **Long Entry**

- **Buy Stop** placed **1 tick above**:
    
    - Reversal candle high (pullback entry)
        
    - OR impulse candle high (impulse entry)
        

### **Short Entry**

- **Sell Stop** placed **1 tick below**:
    
    - Reversal candle low
        
    - OR impulse candle low
        

**Boundary Condition:**

- **Entry only on break of signal candle**
    

## ## **3.3 Stop‑Loss Placement**

### **Long Trades**

- SL below reversal candle low
    
- OR below swing low
    
- OR below daily trend swing low
    

### **Short Trades**

- SL above reversal candle high
    
- OR above swing high
    
- OR above daily trend swing high
    

**Boundary Condition:**

- **SL must be placed BEFORE entry**
    

## ## **3.4 Position Size Calculation**

Code

```
Position Size = Risk per Trade / (SL Distance × Tick Value)
```

- Risk per trade: **0.5–2%**
    
- SL distance: entry → SL
    
- Tick value: contract specification
    

**Boundary Condition:**

- **Position size must match SL distance**
    

## ## **3.5 Correlation Check**

- Avoid trading correlated markets simultaneously
    
- Avoid over‑exposure
    

**Boundary Condition:**

- **No correlated trades allowed**
    

# **4. TRADE MANAGEMENT WORKFLOW**

## ## **4.1 Break‑Even Management**

Move SL to BE when:

- Price reaches **1R**
    
- OR next daily swing breaks
    
- OR minor weekly level is reached
    

**Boundary Condition:**

- **Never move SL to BE too early**
    

## ## **4.2 Trailing Stop Management**

Trail SL behind:

### **Long Trades**

- Daily swing lows
    

### **Short Trades**

- Daily swing highs
    

**Rules:**

- Trail only after confirmed swing
    
- Do not trail inside noise
    
- Trail only in trend continuation
    

## ## **4.3 Add‑On Positions (Pyramiding)**

Allowed only when:

- First position is in profit
    
- SL is at BE
    
- Trend continues cleanly
    
- Seasonality still supports
    
- Market remains strongest/weakest
    

Entry pattern rules apply again.

**Boundary Condition:**

- **Add‑ons only in strong trend continuation**
    

## ## **4.4 Exit Rules**

Exit when:

### **Trend Break**

- Long: break of swing low
    
- Short: break of swing high
    

### **Weekly Trend Break**

- Immediate exit
    

### **Seasonal Change**

- Seasonal window ends
    
- Seasonal turning point arrives
    

### **COT Change**

- Commercials leave extreme
    
- Large Specs reverse strongly
    
- COT contradicts direction
    

**Boundary Condition:**

- **Exit immediately on structural or fundamental contradiction**
    

# **5. DOCUMENTATION WORKFLOW**

## ## **5.1 Trade Log**

Record:

- Market
    
- Direction
    
- Weekly trend
    
- COT signal
    
- Seasonality
    
- Relative strength
    
- Entry pattern
    
- Entry price
    
- SL/TP
    
- Position size
    
- Management actions
    
- Exit reason
    
- Exit price
    
- R‑multiple
    

## ## **5.2 Weekly Review**

- Mistakes
    
- Wins
    
- Losses
    
- Rule adherence
    
- Improvements
    

## ## **5.3 Monthly Review**

- Win rate
    
- Average R
    
- Drawdown
    
- Emotional stability
    
- System stability
    

## ## **5.4 Annual Review**

- Total R
    
- Total trades
    
- Strategic improvements
    
- Personal development
    

# **6. FLOWCHART (ASCII)**

Code

```
Weekly Analysis
   ↓
COT → Weekly Trend → Seasonality → Strength
   ↓ (all must align)
Watchlist
   ↓
Daily Trend Structure
   ↓
Trend Change (HL/LH + break)
   ↓
Entry Pattern (Impulse / Pullback)
   ↓
Entry Trigger (Break of signal candle)
   ↓
Stop-Loss + Position Size + Correlation
   ↓
Trade Active
   ↓
Management:
   - BE Shift
   - Trailing Stop
   - Add-ons
   ↓
Exit:
   - Trend Break
   - Weekly Trend Break
   - Seasonal Turn
   - COT Contradiction
   ↓
Documentation
```

# **7. CHECKLIST (Printable)**

### **Weekly**

- [ ] COT direction
    
- [ ] Weekly trend
    
- [ ] Seasonality
    
- [ ] Relative strength
    
- [ ] Watchlist created
    

### **Daily**

- [ ] Daily trend clean
    
- [ ] Trend change confirmed
    
- [ ] Entry pattern visible
    
- [ ] SL defined
    
- [ ] TP defined
    
- [ ] Position size calculated
    
- [ ] Correlation check passed
    

### **Entry**

- [ ] Break of signal candle
    
- [ ] SL placed
    
- [ ] TP placed
    
- [ ] Position size correct
    

### **Management**

- [ ] SL moved to BE
    
- [ ] Trailing behind swings
    
- [ ] Add-ons only in trend continuation
    

### **Exit**

- [ ] Trend break
    
- [ ] Weekly trend break
    
- [ ] Seasonal turning point
    
- [ ] COT contradiction
