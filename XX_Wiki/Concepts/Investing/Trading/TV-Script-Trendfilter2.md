---
title: "TV Script - Trendfilter2"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Trendfilter2.md"
source_file_id: "1x5B97PGdH5cWSUd4YCPbslm_c9hhQUSL"
---

# TV Script - Trendfilter2

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[03_Tags/JvL-Invest-Futures|Futures]]
[[03_Tags/JvL-Invest-Trading|TradingView]]

Title: TV Script - 
Date: 2025-11-13 
Time: 18:36 

Purpose:  COT2 Tageschart

Script:
------------


// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/  
// © Kaschko  
  
//@version=5  
indicator(title = "TrendFilter2", overlay = false)  
  
_lw = input.int(group = "Histogram", title = "Line width", defval = 5, minval = 1, maxval = 10, display = display.none)  
  
_mac03 = ta.sma(close, 3)  
_mac10 = ta.sma(close,10)  
_cumsum = ta.cum(close - (close > close[1] ? math.min(low,close[1]) : close < close[1] ? math.max(high,close[1]) : close))  
  
var float _lowest = _cumsum  
  
_lowest := _cumsum < _lowest ? _cumsum : _lowest  
  
_macsum = ta.sma(_cumsum + (100 - _lowest), 3)  
_malsum = ta.sma(_cumsum + (100 - _lowest),10)  
  
_tf2 = ((((_mac03-_mac10)/_mac03)*100+((_macsum-_malsum)/_macsum)*100)/2)-ta.sma(((((_mac03-_mac10)/_mac03)*100+((_macsum-_malsum)/_macsum)*100)/2),15)  
_tfp = _tf2 > 0  
_color = _tfp ? color.green : color.red  
  
plot(_tf2,title = "Trendfilter2", style = plot.style_histogram, linewidth = _lw, color = _color)  
  
hline(0, color = color.black, title = "Zero line" , linestyle = hline.style_solid ,linewidth = 1)
