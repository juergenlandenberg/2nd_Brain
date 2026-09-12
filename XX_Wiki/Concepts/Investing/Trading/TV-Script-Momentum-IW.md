---
title: "TV Script - Momentum_IW"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Momentum_IW.md"
source_file_id: "1LuYkGKgT3zb1GULGx3HUlrKkh7KiMGEN"
---

# TV Script - Momentum_IW

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[03_Tags/JvL-Invest-Futures|Futures]]
[[03_Tags/JvL-Invest-Trading|TradingView]]

Title: TV Script - Momentum_IW 
Date: 2025-11-13 
Time: 18:35 

Purpose: COT1 Tageschart

Script:
------------



// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/  
// © Kaschko  
  
//@version=5  
indicator(title = "My Momentum_IW", shorttitle = "Momentum_IW", overlay = false, precision = 4, explicit_plot_zorder = true, max_boxes_count = 500)  
  
float _mom = ta.mom(close,28)  
bool  _divMomBuy  = low  == ta.lowest (low ,60) and ta.mom(close,28) > ta.lowest (ta.mom(close,28),54)[6]  
bool  _divMomSell = high == ta.highest(high,60) and ta.mom(close,28) < ta.highest(ta.mom(close,28),54)[6]  
  
_bsDMB = ta.barssince(not _divMomBuy )  
_bsDMS = ta.barssince(not _divMomSell)  
  
var box _box = na  
  
_BColor = input.color(color.new(#1ab31a, 0), title = "DivMomBuy Color")  
_SColor = input.color(color.new(#ff0000, 0), title = "DivMomSell Color")  
  
hline(0,title = "Horizontal Line", color = #808080  , linewidth = 2, linestyle = hline.style_solid)  
  
if _divMomBuy  
    _box  := box.new(bar_index-_bsDMB,math.max(_mom[_bsDMB],_mom),bar_index,math.min(_mom[_bsDMB],_mom), border_width = 2, border_color = _BColor, bgcolor = _BColor)  
  
if _divMomSell  
    _box  := box.new(bar_index-_bsDMS,math.max(_mom[_bsDMS],_mom),bar_index,math.min(_mom[_bsDMS],_mom), border_width = 2, border_color = _SColor, bgcolor = _SColor)  
  
plot(_mom, title = "Momentum", color = #0000ff, linewidth = 2)
