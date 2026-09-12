---
title: "TV Script - POIV"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - POIV.md"
source_file_id: "1E_IjE1vxdKcTY994ggD8CtpVl340hEtj"
---

# TV Script - POIV

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[03_Tags/JvL-Invest-Futures|Futures]]
[[03_Tags/JvL-Invest-Trading|TradingView]]

Title: TV Script - POIV 
Date: 2025-11-13 
Time: 18:37 

Purpose: 

Script:
------------

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/  
// © Kaschko  
  
//@version=5  
indicator(title = "My POIV", shorttitle = "POIV", overlay = true, precision = 0, scale = scale.none)  
  
import TradingView/LibraryCOT/2 as cotlib  
  
_root = syminfo.root  
if      _root == "MCL" or _root == "MES" or _root == "MGC" or _root == "MNQ" or _root == "MYM"  
    _root := str.substring(_root,1,3)  
else if _root == "QC"  
    _root := "HG"  
else if _root == "QG"  
    _root := "NG"  
else if _root == "QM"  
    _root := "CL"  
else if _root == "QO"  
    _root := "GC"  
_cftc_code   = cotlib.rootToCFTCCode(_root)  
if _root == "HG"  
    _cftc_code := "085692" // missing in LibraryCOT  
else if _root == "LBR"  
    _cftc_code := "058644" // missing in LibraryCOT  
  
f_COTtickerid(string i_cftc_code, string i_metric, string i_dir) =>  
    cotlib.COTTickerid(  
          COTType         = "Legacy"  
         ,CFTCCode        = i_cftc_code  
         ,includeOptions  = false  
         ,metricName      = i_metric  
         ,metricDirection = i_dir  
         ,metricType      = "All"  
         )  
  
var string _t_open_intr = f_COTtickerid(_cftc_code, "Open Interest", "No direction")   
  
_oi = request.security(_t_open_intr, "D", close, ignore_invalid_symbol = true)  
  
// OBV  
_obv  = ta.cum(math.sign(close-close[1])*volume)  
// POIV  
_trueHigh = math.max(high, close[1])  
_trueLow  = math.min(low , close[1])  
_poiv     = ta.cum(_oi*(close-close[1])/(_trueHigh-_trueLow))+_obv  
  
plot(_poiv, title = "POIV", color = #ff00ff, linewidth = 2)
