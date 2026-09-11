---
title: "TV Script - Kaschko's Open Interest"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Kaschko's Open Interest.md"
source_file_id: "171EGwZQoH7laHNDdf836q_E93kFaA7G7"
---

# TV Script - Kaschko's Open Interest

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[Futures]]
[[TradingView]]

Title: TV Script - Kaschko's Open Interest 
Date: 2025-11-13 
Time: 18:25 

Purpose: 
This script provides an indicator showing the open interest of futures contracts from the COT data (usinng data from Nasdaq data link, formerly known as quandl). Therefore, it works only with futures for which these data are available.
Script:
------------

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/  
// © Kaschko  
  
//@version=5  
indicator("Kaschko's Open Interest", shorttitle = "Open Interest", overlay = true, precision = 0, timeframe = "W", timeframe_gaps = false, scale = scale.none)  
  
import TradingView/LibraryCOT/2 as cotlib  
  
f_Root() =>  
    _ret = syminfo.root  
    if      _ret == "MCL" or _ret == "MES" or _ret == "MGC" or _ret == "MNQ" or _ret == "MYM"  
        _ret := str.substring(_ret,1,3)  
    else if _ret == "QG"  
        _ret := "NG"  
    else if _ret == "QM"  
        _ret := "CL"  
    else if _ret == "QO"  
        _ret := "GC"  
    _ret  
  
var string _root = f_Root()  
var string _cftc_code = cotlib.rootToCFTCCode(_root)  
  
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
  
_open_intr  = request.security(_t_open_intr, "D", close, ignore_invalid_symbol = true)  
  
plot(_open_intr, title = "Open Interest", color = #000000, linewidth = 2, display = display.pane+display.status_line)
