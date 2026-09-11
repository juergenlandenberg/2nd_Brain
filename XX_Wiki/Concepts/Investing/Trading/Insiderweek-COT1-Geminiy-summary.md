---
title: "Insiderweek COT1 - Geminiy summary"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Insiderweek COT1 - Geminiy summary.md"
source_file_id: "10OnxzkQbowtZhtZgFh9NkKXVgJeHStLt"
---

# Insiderweek COT1 - Geminiy summary

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[insiderweek]] 
[[Futures]]

  



Title: Insiderweek COT1 - Geminiy summary 
Date: 2026-08-25 
Time: 14:13 
Source:


Type: [[Option]], [[Futures]], [[Equity]]
Market: Bullish, Bearisch, Range/Neutral


    

### Executive Summary of the Master Workflow Specification

#### 1. Fundamental & Macro Alignment (Weekly Preparation)

- **COT Report Analysis:**
    
    - **Commercials (Hedgers):** Evaluated against 3–5 year lookback windows to identify extreme net long or short positioning[cite: 1].
        
    - **Large Speculators:** Monitored for trend exhaustion and divergence relative to Commercial positioning[cite: 1].
        
    - **COT Signal:** Commercials at multi-year net long extreme → Bullish Bias; Commercials at multi-year net short extreme → Bearish Bias[cite: 1].
        
    - **Activation Requirement:** A COT signal is a bias and **must** be activated by daily price structure before trading[cite: 1].
        
- **Weekly Trend Analysis (_Markttechnik_):**
    
    - **Uptrend:** Clear sequence of Higher Highs (HH) and Higher Lows (HL)[cite: 1].
        
    - **Downtrend:** Clear sequence of Lower Highs (LH) and Lower Lows (LL)[cite: 1].
        
    - **Hard Boundary Condition:** If the weekly trend is sideways or ambiguous, the market is strictly **excluded** from trading[cite: 1].
        
- **Seasonal Trend Analysis:**
    
    - Evaluated via the **InsiderWeek Seasonality Tool** (30, 15, and 5-year seasonal curves)[cite: 1].
        
    - Active multi-week seasonal window must support the direction of the COT signal and weekly trend[cite: 1].
        
- **Relative Strength & Weakness:**
    
    - Correlated markets are grouped (Energies, Grains, Metals, Softs, Currencies)[cite: 1].
        
    - **Long Setups:** Choose the single strongest leader in the group[cite: 1].
        
    - **Short Setups:** Choose the single weakest lagger in the group[cite: 1].
        

#### 2. Execution & Entry Boundary Conditions (Daily Workflow)

- **Daily Trend Change (_Trendwechsel_):**
    
    - **Long Setup:** Daily Higher Low (HL) forms followed by a structural break above the prior short-term swing high[cite: 1].
        
    - **Short Setup:** Daily Lower High (LH) forms followed by a structural break below the prior short-term swing low[cite: 1].
        
- **Exact Entry Triggers:**
    
    - **Impulswelle (Impulse Entry):** Buy/Sell Stop placed **1 tick above/below** the setup/impulse candle[cite: 1].
        
    - **Korrekturwelle (Pullback Entry):** Buy/Sell Stop placed **1 tick above/below** the reversal candle high/low following a pullback into key support/resistance[cite: 1].
        

#### 3. Risk Management & Position Sizing

- **Stop-Loss (SL) Rules:**
    
    - **Rule #1:** Never execute a trade without a pre-calculated hard Stop-Loss placed in the market[cite: 1].
        
    - **Placement:** 1–2 ticks beyond the setup/reversal candle or structural swing high/low[cite: 1].
        
- **Position Sizing Formula:**
    
    Position Size (Contracts)=⌊Stop Distance (Ticks)×Tick Value ($)Account Equity×Risk %​⌋[cite:1]
    
    - **Risk Parameter:** 0.5% to 2.0% per trade[cite: 1]. Sector exposure capped at 2 open positions per correlated group[cite: 1].
        

#### 4. Trade Management & Exits

- **Break-Even (BE) Management:** Shift SL to Entry Price + 1 tick once price achieves **1R** profit distance (1×Initial Risk) or breaks through the next daily swing structure[cite: 1].
    
- **Trailing Stop Execution:** Trail Stop-Loss strictly behind newly confirmed daily swing lows (Longs) or swing highs (Shorts) after candle closure[cite: 1].
    
- **Exit Conditions:**
    
    - **Technical Exit:** Daily trend structure break[cite: 1].
        
    - **Target Exit:** Reaching TP1 (Weekly Support/Resistance) or TP2 (Seasonal turning window)[cite: 1].
        
    - **Fundamental Exit:** Commercials reversing out of extreme positioning or seasonal window expiration[cite: 1].
        

#### 5. Documentation & Trading Journal

- **Mandatory Attributes Logged:** Market, Direction, COT Rating, Weekly Bias, Seasonal Rating, Entry Pattern, Risk %, Initial SL, TP Target, Fill Price, Management History, Realized R-Multiple, and Execution Quality Score[cite: 1].
    

  

Gemini is AI and can make mistakes, including about people. [Your privacy and GeminiOpens in a new window](https://support.google.com/gemini?p=privacy_notice)

Analysing

# INSIDERWEEK COT1 MASTER WORKFLOW SPECIFICATION
## End-to-End Futures Trading System: From Weekly Analysis to Execution, Management & Journaling

---

## 1. STRATEGY OVERVIEW & SYSTEM ARCHITECTURE

### 1.1 Fundamental Core Principles
* **Institutional Alignment:** The COT1 strategy is built upon tracking institutional market participants—specifically **Commercials** (producers, merchants, and processors who hedge physical commodities) and **Large Speculators** (hedge funds and institutional money managers) [cite: 1].
* **Multi-Filter Framework:** Trade permission is never granted by a single indicator or technical setup [cite: 1]. A trade is only authorized when four independent dimensions align:
  1. **Fundamental Bias:** COT net positioning at multi-year historical extremes [cite: 1].
  2. **Seasonal Window:** High-probability seasonal directional bias (30, 15, and 5-year historical trends) [cite: 1].
  3. **Technical Trend Alignment:** Clear weekly structure via *Markttechnik* (higher highs/higher lows or lower highs/lower lows) [cite: 1].
  4. **Relative Strength/Weakness:** Selecting only the strongest instrument within a sector for longs, or the weakest for shorts [cite: 1].

### 1.2 Multi-Timeframe Integration Hierarchy
* **Weekly Chart (Macro Direction & Gatekeeper):**
  * Establishes overall fundamental and technical bias [cite: 1].
  * Identifies macro support/resistance zones [cite: 1].
  * Evaluates COT positioning and seasonal windows [cite: 1].
  * *Gatekeeper Rule:* If the weekly trend is ambiguous or sideways, the market is strictly excluded regardless of daily signals [cite: 1].
* **Daily Chart (Execution & Activation Layer):**
  * Evaluates daily trend structure (*Markttechnik*) [cite: 1].
  * Monitors for daily trend changes that activate the weekly COT signal [cite: 1].
  * Pinpoints exact entry pattern triggers (Impulse or Correction/Pullback) [cite: 1].
  * Manages active trades (Breakeven shifts, trailing stops, add-on entries) [cite: 1].

---

## 2. PHASE 1: WEEKLY PREPARATION WORKFLOW

### 2.1 Step 1: COT Report Analysis (Data Release: Friday Evening → Applied: Weekly Preparation)
* **Participant Analysis:**
  * **Commercials (Hedgers):** Monitor net positioning relative to historical multi-year lookback windows (3–5 years) [cite: 1]. Identify extreme net long or extreme net short levels [cite: 1].
  * **Large Speculators:** Verify institutional trend continuation or over-extension/exhaustion [cite: 1]. Look for extreme long/short positioning divergence against Commercials [cite: 1].
* **COT Signal Identification & Activation Criteria:**
  * **Bullish COT Signal:** Commercial net position reaches a multi-year high extreme while Large Speculators reach a net short extreme [cite: 1].
  * **Bearish COT Signal:** Commercial net position reaches a multi-year low extreme while Large Speculators reach a net long extreme [cite: 1].
  * **Signal Validity Duration:** A COT signal remains valid for multiple weeks as long as Commercials remain near historical extremes and the weekly structure holds [cite: 1].
  * **Activation Imperative:** A COT signal is a *bias*, not an order [cite: 1]. It must be explicitly activated by daily price action before any order is placed [cite: 1].

### 2.2 Step 2: Weekly Trend Analysis (*Markttechnik*)
* **Uptrend (Wochentrend Long):** Clear sequence of higher highs (HH) and higher lows (HL) on the weekly chart [cite: 1].
* **Downtrend (Wochentrend Short):** Clear sequence of lower highs (LH) and lower lows (LL) on the weekly chart [cite: 1].
* **Sideways / Unclear Market (Seitwärtsmarkt):** Overlapping swing highs and lows with no defined trend structure [cite: 1].
* **Hard Exclusion Boundary:** If a weekly trend cannot be defined cleanly by *Markttechnik*, the market is immediately disqualified from trading [cite: 1].

### 2.3 Step 3: Seasonal Trend Analysis
* **Tooling:** InsiderWeek Seasonality Tool (evaluating 30-year, 15-year, and 5-year seasonal curves) [cite: 1].
* **Window Identification:** Locate multi-week directional windows where historical probability strongly supports the COT bias [cite: 1].
* **Boundary Conditions:**
  * Seasonality must support the direction of both the COT signal and the weekly trend [cite: 1].
  * Do not enter new trades if the seasonal window has less than 5–7 trading days remaining before a major historical inflection point [cite: 1].

### 2.4 Step 4: Relative Strength & Weakness Analysis
* **Sector Grouping:** Group instruments into correlated asset classes (e.g., Grains, Energies, Metals, Softs, Currencies, Indices) [cite: 1].
* **Comparative Evaluation:**
  * For **Long Setups**: Select the single strongest instrument in the group showing the highest momentum and cleanest trend structure [cite: 1].
  * For **Short Setups**: Select the single weakest instrument showing the most vulnerable structure [cite: 1].
* **Rule:** If an instrument is not the relative strength leader (or weakness leader), exclude it in favor of the group leader [cite: 1].

### 2.5 Step 5: Master Watchlist Construction
* Combine alignment across all four dimensions [cite: 1]:
  $$\text{Watchlist Candidate} = \text{COT Signal} \cap \text{Weekly Trend} \cap \text{Seasonal Alignment} \cap \text{Relative Leader} [cite: 1]$$
* Document selected markets, bias (Long/Short), active seasonal window, key weekly support/resistance levels, and current daily activation status [cite: 1].

---

## 3. PHASE 2: DAILY PREPARATION & ENTRY PATTERN SELECTION

### 3.1 Daily Trend Analysis & Activation Trigger
* **Swing Structure:** Map short-term and medium-term swing highs and lows (assisted visually by ZigZag, verified manually) [cite: 1].
* **Trend Change Requirement (Trendwechsel):**
  * *Long Activation:* Formation of a daily higher low (HL) followed by a structural break above the prior short-term high [cite: 1].
  * *Short Activation:* Formation of a daily lower high (LH) followed by a structural break below the prior short-term low [cite: 1].
  * **Mandatory Rule:** Entering before a confirmed daily trend change is strictly prohibited [cite: 1].

### 3.2 Entry Pattern Definitions & Exact Triggers
* **Pattern Type A: Impulswelle (Impulse Entry)**
  * *Setup:* Occurs following a fresh daily trend change where strong directional momentum initiates a new trend leg [cite: 1].
  * *Long Execution:* Place a **Buy Stop** order **1 tick above the high** of the setup/impulse candle [cite: 1].
  * *Short Execution:* Place a **Sell Stop** order **1 tick below the low** of the setup/impulse candle [cite: 1].
* **Pattern Type B: Korrekturwelle (Pullback / Reversal Entry)**
  * *Setup:* Occurs after an established daily trend pulls back into a key structural support/resistance area or moving average zone, displaying a bullish/bearish reversal candle (Pin Bar, Engulfing) [cite: 1].
  * *Long Execution:* Place a **Buy Stop** order **1 tick above the high** of the reversal candle [cite: 1].
  * *Short Execution:* Place a **Sell Stop** order **1 tick below the low** of the reversal candle [cite: 1].

---

## 4. PHASE 3: RISK MANAGEMENT & POSITION SIZING

### 4.1 Stop-Loss (SL) Rules
* **Rule #1:** Never execute a trade without a pre-calculated, hard Stop-Loss order placed in the market [cite: 1].
* **Placement Geometry:**
  * *Long Trade:* Position SL 1–2 ticks below the setup/reversal candle low OR below the recent daily swing low (structural SL) [cite: 1].
  * *Short Trade:* Position SL 1–2 ticks above the setup/reversal candle high OR above the recent daily swing high (structural SL) [cite: 1].

### 4.2 Take-Profit (TP) Rules
* **TP Definition:** Must be established prior to trade execution [cite: 1].
* **Targets:**
  * **TP1:** Next major weekly support/resistance zone [cite: 1].
  * **TP2:** Major seasonal turning point window [cite: 1].
  * **TP3 (Optional):** Commercial positioning exit (when Commercials exit historical extreme levels) [cite: 1].

### 4.3 Position Sizing Formula
$$\text{Position Size (Contracts)} = \left\lfloor \frac{\text{Account Equity} \times \text{Risk \%}}{\text{Stop Distance (Ticks)} \times \text{Tick Value (\$)}} \right\rfloor [cite: 1]$$
* **Standard Account Risk:** 0.5% to 2.0% per trade [cite: 1].
* **Correlation Exposure Limit:** Maximum 2 open positions within the same correlated asset group [cite: 1].

---

## 5. PHASE 4: TRADE MANAGEMENT & EXIT RULES

### 5.1 Break-Even (BE) Management
* Shift Stop-Loss to Breakeven (Entry Price + 1 tick to cover friction) when:
  * Price achieves **1R** profit distance ($1 \times \text{Initial Risk}$), OR
  * Price breaks through the first daily swing level in the trade's direction [cite: 1].

### 5.2 Trailing Stop Execution
* Trail the Stop-Loss behind newly confirmed daily swing lows (Long) or daily swing highs (Short) [cite: 1].
* Only move trailing stops upon candle closure confirming a new swing structure [cite: 1]. Never trail inside intra-day noise or unconfirmed swings [cite: 1].

### 5.3 Add-On Positions (Pyramiding)
* **Conditions for Add-On:**
  1. Initial position is secured at Break-Even or in profit [cite: 1].
  2. Daily trend confirms a clean continuation pattern (new impulse/pullback) [cite: 1].
  3. Total risk across combined positions stays within account safety limits [cite: 1].

### 5.4 Exit Signals
* **Technical Exit:** Structural daily trend break (break of prior swing low for longs, prior swing high for shorts) [cite: 1].
* **Macro Exit:** Weekly trend invalidation [cite: 1].
* **Fundamental/Seasonal Exit:** Expiration of seasonal window or Commercials reversing out of extreme positioning [cite: 1].
* **Operational Exit:** Liquidate positions prior to contract rollover or high-impact unexpected fundamental shocks [cite: 1].

---

## 6. PHASE 5: DOCUMENTATION & TRADING JOURNAL

### 6.1 Essential Journal Attributes
Every executed trade must record [cite: 1]:
* **Context:** Date, Contract, COT Extremes, Weekly Trend Bias, Seasonal Rating, Relative Strength Score [cite: 1].
* **Execution:** Entry Trigger Type (Impulse/Pullback), Planned Entry, Actual Fill, Initial SL, Initial TP, Contract Size [cite: 1].
* **Management Log:** BE Shift Date, Trailing Stop Updates, Add-on details [cite: 1].
* **Exit & Metrics:** Exit Date, Exit Price, Exit Reason, Realized PnL ($ and R-multiple) [cite: 1].
* **Post-Trade Review:** Execution Score (1–5), Emotional State, Mistakes/Deviations, Key Lessons Learned [cite: 1].

### 6.2 Review Cadence
* **Weekly Review:** Assess rule adherence, review watchlist conversion rates, adjust operational process [cite: 1].
* **Monthly/Annual Review:** Analyze system metrics (Win Rate, Profit Factor, Average R-Multiple, Max Drawdown) and refine parameters [cite: 1].

cot1_master_workflow.md

Displaying cot1_master_workflow.md.




# Conversation with Gemini

based on this Document and the analysis you have done in the copilot chat, can you create a workflow document describing the steps to take from weekly analysis to trade entering, manage and exit. please mention exact entry and exit points. keep the summary descriptive in a structured bullet list format with several levels. focus to crystalize out the exact boundary conditions, required market setup and steps for entering and exiting the trade as well interim stoploss management. I like to get one consistent workflow document Please generate a B" master document from the attached file, , please create  a MD file from it. Then secondly a pdf and include a flowchart at the end of the pdf. finally add a checklist to the very end of the pdf
