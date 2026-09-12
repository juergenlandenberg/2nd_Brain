---
title: "TV Script - Kaschko's COT Net Pos"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Kaschko's COT Net Pos.md"
source_file_id: "1L5hYE0rylbIaCJK9l3oveQExkKcC_Zxx"
---

# TV Script - Kaschko's COT Net Pos

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[03_Tags/JvL-Invest-Futures|Futures]]
[[03_Tags/JvL-Invest-Trading|TradingView]]

Title: Kaschko's COT Net Pos 
Date: 2025-11-13 
Time: 18:19 

Purpose: 
This script provides an indicator that shows the net positioning of Commercials, Large Speculators and Small Speculators in futures contracts for which the CFTC ([cftc.gov](https://www.cftc.gov/)) is publishing COT reports. Optionally, the open interest can also be displayed. Data source are the COT data, which are provided via the Nasdaq data link (formerly known as quandl). For COT data, see [cftc.gov](https://www.cftc.gov/) («Commitment of Traders»).
Script:
------------

// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/  
// © Kaschko  
  
//@version=5  
indicator("Kaschko's COT Net Pos", shorttitle = "COT Net Pos", overlay = false, precision = 0)  
  
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
  
var string _t_comm_long = f_COTtickerid(_cftc_code, "Commercial Positions"   , "Long" )  
var string _t_comm_shrt = f_COTtickerid(_cftc_code, "Commercial Positions"   , "Short")  
var string _t_lrsp_long = f_COTtickerid(_cftc_code, "Noncommercial Positions", "Long" )  
var string _t_lrsp_shrt = f_COTtickerid(_cftc_code, "Noncommercial Positions", "Short")   
var string _t_smsp_long = f_COTtickerid(_cftc_code, "Nonreportable Positions", "Long" )    
var string _t_smsp_shrt = f_COTtickerid(_cftc_code, "Nonreportable Positions", "Short")   
var string _t_open_intr = f_COTtickerid(_cftc_code, "Open Interest", "No direction")    
  
_comm_long  = request.security(_t_comm_long, "D", close, ignore_invalid_symbol = true)  
_comm_short = request.security(_t_comm_shrt, "D", close, ignore_invalid_symbol = true)  
_lrsp_long  = request.security(_t_lrsp_long, "D", close, ignore_invalid_symbol = true)  
_lrsp_short = request.security(_t_lrsp_shrt, "D", close, ignore_invalid_symbol = true)  
_smsp_long  = request.security(_t_smsp_long, "D", close, ignore_invalid_symbol = true)  
_smsp_short = request.security(_t_smsp_shrt, "D", close, ignore_invalid_symbol = true)  
_open_intr  = request.security(_t_open_intr, "D", close, ignore_invalid_symbol = true)  
  
_comm_net   = _comm_long-_comm_short  
_lrsp_net   = _lrsp_long-_lrsp_short  
_smsp_net   = _smsp_long-_smsp_short  
  
float _comm_high = ta.highest(_comm_net ,100)  
float _comm_low  = ta.lowest (_comm_net ,100)  
float _lrsp_high = ta.highest(_lrsp_net ,100)  
float _lrsp_low  = ta.lowest (_lrsp_net ,100)  
float _smsp_high = ta.highest(_smsp_net ,100)  
float _smsp_low  = ta.lowest (_smsp_net ,100)  
float _opin_high = ta.highest(_open_intr,100)  
float _opin_low  = ta.lowest (_open_intr,100)  
  
_highest   = math.max(_comm_high,_lrsp_high,_smsp_high)  
_lowest    = math.min(_comm_low ,_lrsp_low ,_smsp_low )  
_height    = _highest-_lowest  
_oirange   = _opin_high-_opin_low  
_factor    = _height/_oirange  
  
plot(_comm_net , title = "COT Commercials"  , color = #ff0000, linewidth = 2)  
plot(_lrsp_net , title = "COT Large Spec"   , color = #00c000, linewidth = 2)  
plot(_smsp_net , title = "COT Small Spec"   , color = #e0e0e0, linewidth = 2)  
plot(_open_intr, title = "Open Interest Val", color = #000000, linewidth = 2, display = display.status_line)  
plot(_lowest+(_open_intr-_opin_low)*_factor, title = "Open Interest"  , color = #000000, linewidth = 2, display = display.pane)  
  
hline(0, color = color.black, title = "Zero line" , linestyle = hline.style_dotted ,linewidth = 1)
