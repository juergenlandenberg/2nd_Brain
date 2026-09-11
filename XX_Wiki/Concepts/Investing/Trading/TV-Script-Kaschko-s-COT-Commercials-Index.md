---
title: "TV Script - Kaschko's COT Commercials Index"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Kaschko's COT Commercials Index.md"
source_file_id: "1eSe5WNWWrF4VJT9wvZOQYH8QELF4ncse"
---

# TV Script - Kaschko's COT Commercials Index

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[Futures]]
[[TradingView]]

Title: TV Script - Kaschko's COT Commercials Index 
Date: 2025-11-13 
Time: 18:27 

Purpose: 
This script provides an implementation of the COT Commercial Index, which ...  
  
- optionally displays the Small Speculators Index as a sentiment or contra indicator  
- shows correct values on all time units  
- updates the index value on Friday after the close based on the newly available data  
- shows the same values as most other commercial tools do  
  
For information on COT data, please check out the corresponding page at [cftc.gov](https://www.cftc.gov/) («Commitments of Traders»).
Script:
------------
// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/  
// © Kaschko  
  
//@version=5  
indicator("COT Commercials Index", shorttitle = "COT-CI", overlay = false, precision = 2)  
  
import TradingView/LibraryCOT/2 as cotlib  
  
_interval  = input.int  (group = "COT index", title = "Interval in weeks"        , defval =  26, minval =   1)  
_dOff      = input.int  (group = "COT index", title = "COT data offset"          , defval =   0, minval =   0, maxval =  1, display = display.none)  
_offset    = input.int  (group = "COT index", title = "Offset"                   , defval =   0, minval = -10, maxval = 10)  
_bZone     = input.int  (group = "COT index", title = "Buy zone threshold"       , defval =  75, minval =   5, maxval = 95, display = display.data_window)  
_sZone     = input.int  (group = "COT index", title = "Sell zone threshold"      , defval =  25, minval =   5, maxval = 95, display = display.data_window)  
_showZones = input.bool (group = "COT index", title = "Highlight buy/sell zones" , defval = false)  
_sZbgcolor = input.color(group = "COT index", title = "Sell zone backgroun color", defval = #fff0f0)  
_bZbgcolor = input.color(group = "COT index", title = "Buy zone background color", defval = #e7feea)  
_colorCI   = input.color(group = "COT index", title = "COT Index Color"          , defval = #ff0000)  
_colorSI   = input.color(group = "COT index", title = "Sentiment Index Color"    , defval = #0000ff)  
_showSI    = input.bool (group = "COT index", title = "Show sentiment index"     , defval = false)  
  
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
  
var string _t_comm_long = f_COTtickerid(_cftc_code, "Commercial Positions"      , "Long" )  
var string _t_comm_shrt = f_COTtickerid(_cftc_code, "Commercial Positions"      , "Short")  
var string _t_totl_long = f_COTtickerid(_cftc_code, "Total Reportable Positions", "Long" )  
var string _t_totl_shrt = f_COTtickerid(_cftc_code, "Total Reportable Positions", "Short")  
  
_comm_long   = request.security(_t_comm_long, "D", close, barmerge.gaps_off, barmerge.lookahead_off, ignore_invalid_symbol = true)  
_comm_short  = request.security(_t_comm_shrt, "D", close, barmerge.gaps_off, barmerge.lookahead_off, ignore_invalid_symbol = true)  
_totl_long   = request.security(_t_totl_long, "D", close, barmerge.gaps_off, barmerge.lookahead_off, ignore_invalid_symbol = true)  
_totl_short  = request.security(_t_totl_shrt, "D", close, barmerge.gaps_off, barmerge.lookahead_off, ignore_invalid_symbol = true)  
_comm_long0  = request.security(_t_comm_long, "W", close, barmerge.gaps_off, barmerge.lookahead_off, ignore_invalid_symbol = true)  
_comm_short0 = request.security(_t_comm_shrt, "W", close, barmerge.gaps_off, barmerge.lookahead_off, ignore_invalid_symbol = true)  
_totl_long0  = request.security(_t_totl_long, "W", close, barmerge.gaps_off, barmerge.lookahead_off, ignore_invalid_symbol = true)  
_totl_short0 = request.security(_t_totl_shrt, "W", close, barmerge.gaps_off, barmerge.lookahead_off, ignore_invalid_symbol = true)  
  
_comm_net   = _comm_long [_dOff] - _comm_short[_dOff]  
_smsp_net   = _totl_short[_dOff] - _totl_long [_dOff]  
_comm_net0  = _comm_long0        - _comm_short0  
_smsp_net0  = _totl_short0       - _totl_long0  
  
[_comm_index,_smsp_index,_comm_index0,_smsp_index0] = request.security(  
       syminfo.tickerid  
      ,"W"  
      ,[100*(_comm_net -ta.lowest(_comm_net ,_interval))/(ta.highest(_comm_net ,_interval)-ta.lowest(_comm_net ,_interval))  
       ,100*(_smsp_net -ta.lowest(_smsp_net ,_interval))/(ta.highest(_smsp_net ,_interval)-ta.lowest(_smsp_net ,_interval))  
       ,100*(_comm_net0-ta.lowest(_comm_net0,_interval))/(ta.highest(_comm_net0,_interval)-ta.lowest(_comm_net0,_interval))  
       ,100*(_smsp_net0-ta.lowest(_smsp_net0,_interval))/(ta.highest(_smsp_net0,_interval)-ta.lowest(_smsp_net0,_interval))  
       ]  
      ,barmerge.gaps_off  
      ,barmerge.lookahead_on  
      ,ignore_invalid_symbol = true  
      )  
  
_cotx = timeframe.period == "W" ? _comm_index : time_close("W") == time_close ? _comm_index : _comm_index0  
_sspx = timeframe.period == "W" ? _smsp_index : time_close("W") == time_close ? _smsp_index : _smsp_index0  
  
plot(_cotx               , title = "COT Commercial Index", color = _colorCI, linewidth = 2, offset = _offset)  
plot(_showSI ? _sspx : na, title = "Sentiment Index"     , color = _colorSI, linewidth = 2, offset = _offset)  
  
plot(_comm_index0, title="COT CI Ahead", color = _colorCI, display = display.data_window)  
plot(_smsp_index0, title="COT SI Ahead", color = _colorSI, display = display.data_window)  
  
bgcolor(_showZones and _cotx >= _bZone ? _bZbgcolor : _showZones and _cotx <= _sZone ? _sZbgcolor : na)  
  
hline(   102, color = color.new(#ffffff, 100), title = ""         , linestyle = hline.style_solid ,linewidth = 1, editable = false)  
hline(    -2, color = color.new(#ffffff, 100), title = ""         , linestyle = hline.style_solid ,linewidth = 1, editable = false)  
hline(_bZone, color = color.black            , title = "Buy zone" , linestyle = hline.style_solid ,linewidth = 2)  
hline(_sZone, color = color.black            , title = "Sell zone", linestyle = hline.style_solid ,linewidth = 2)
