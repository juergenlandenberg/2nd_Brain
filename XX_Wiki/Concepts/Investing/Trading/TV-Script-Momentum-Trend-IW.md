---
title: "TV Script - Momentum Trend_IW"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Momentum Trend_IW.md"
source_file_id: "1EgTb3z9hYHIH0-VHFSUJJcf8w1muxTwp"
---

# TV Script - Momentum Trend_IW

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[03_Tags/JvL-Invest-Futures|Futures]]
[[03_Tags/JvL-Invest-Trading|TradingView]]

Title: TV Script - Momentum Trend_IW 
Date: 2025-11-13 
Time: 18:31 

Purpose: COT1 Tageschart

Script:
------------
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/  
// © Kaschko  
  
//@version=5  
indicator(title = "My Momentum Trend_IW", shorttitle = "Momentum Trend_IW", overlay = false, precision = 2)  
  
PercentR(int _numBars) =>  
    _pctrhh = ta.highest(high,_numBars)  
    _pctrll = ta.lowest (low ,_numBars)  
    _pctr   = 100 * (close - _pctrll) / (_pctrhh - _pctrll)  
  
_iPctRBars            = input.int  (group = "PctR", title = "Number of bars used",  defval =  4, minval =  2, maxval = 100)  
_iOverboughtThreshold = input.float(group = "PctR", title = "Overbought Threshold", defval = 75, minval = 10, maxval = 100)  
_iOversoldThreshold   = input.float(group = "PctR", title = "Oversold Threshold"  , defval = 25, minval =  0, maxval =  90)  
  
// Calculate the PctRs  
_pctr   = PercentR(_iPctRBars)  
_pctr88 = PercentR(88)  
  
/// Calculate the momentum trend  
_mom = ta.ema(_pctr88,21)  
  
plot(_pctr, title = "PercentR"         , color = #000000, linewidth = 2)  
plot(_mom , title = "Momentum Trend_IW", color = #0000ff, linewidth = 2)   
hline(_iOverboughtThreshold            , color = #ff0000, linewidth = 2, linestyle = hline.style_solid)  
hline(_iOversoldThreshold              , color = #00c000, linewidth = 2, linestyle = hline.style_solid)
