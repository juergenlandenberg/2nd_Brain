---
title: "TV Script - Primatrend"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Primatrend.md"
source_file_id: "1E54ytQpbrEFTURwcEDOn82XnJ8aGQ1S8"
---

# TV Script - Primatrend

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[Futures]]
[[TradingView]]

Title: TV Script - Primatrend 
Date: 2025-11-13 
Time: 18:32 

Purpose: 
COT Tageschart 

**Primary Trend** is a handy tool if you are used to trading on a clean chart, but sometimes you need to take a look at Primary Trend. The Primary Trend indicator studies price action as a collection of price and time vectors, and uses the average vector to determine the direction and strength of the market. This indicator highlights the short-term direction and strength of the market. The indicator is not redrawn. The indicator implements a breakout strategy. The arrows show the direction of the market. Use the indicator on intervals from M15 and above. Moving averages are not applied.
Script:
------------

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/  
// © Kaschko  
  
//@version=5  
indicator(title = "My Primatrend", shorttitle = "PrimaTrend", overlay = false, precision = 2)  
  
_trueHigh = math.max(high, close[1])  
_trueLow  = math.min(low , close[1])  
  
_prima = ta.cum(close > close[1] ? close - _trueLow : close < close[1] ? close - _trueHigh : 0)  
_ma57  = ta.sma(_prima,57)  
  
plot(_prima, title = "PrimaTrend IW", color = _prima < _ma57 ? #ff0000 : _prima > _ma57 ? #008000 : #0000ff, linewidth = 2)  
plot(_ma57 , title = "MovingAvg(57)", color = #0000ff, linewidth = 2)
