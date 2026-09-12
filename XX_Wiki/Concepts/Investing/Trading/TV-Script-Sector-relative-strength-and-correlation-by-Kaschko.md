---
title: "TV Script - Sector relative strength and correlation by Kaschko"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Sector relative strength and correlation by Kaschko.md"
source_file_id: "19UuBwvl7W7G4WQBtFQ3LXc59F1hDT_p8"
---

# TV Script - Sector relative strength and correlation by Kaschko

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[03_Tags/JvL-Invest-Futures|Futures]]
[[03_Tags/JvL-Invest-Trading|TradingView]]

Title: Untitled 
Date: 2025-11-13 
Time: 18:12 

Purpose: 
This script provides a quick overview of the relative strength and correlation of the symbols in a sector by showing a line chart of the close prices on a percent scale with all symbols starting at zero at the left side of the chart. It allows a great deal of flexibility in the configuration of the sectors and symbols in it. The standard preset sectors cover the most important futures markets and their symbols.  
  
However, up to ten sectors with up to ten symbols each can be freely configured. Each sector is defined by a single line that has the following format:  
  
Sector name:Symbol suffix:List of comma separated symbols  
  
For example, the first predefined sector is defined as follows.  
  
Energies:1!:CL,HO,NG,RB  
  
1. The name of the sector is "Energies"  
2. The suffix is "1!", i.e., to each symbol in the list "1!" is appended to get the continous future for the given symbol root. When using stock, forex or other symbols, simply leave the suffix empty.  
3. The list of comma separated symbols is "CL,HO,NG,RB", i.e. crude oil, heating oil, natural gas and gasoline. As the suffix is "1!", the actual symbols whose prices are shown are "CL1!","HO1!","NG1!" and "RB1!"  
  
You can choose to use settlement-as-close and back-adjusted contracts. The sector can also be determined automatically ("Auto-select"). In this case, it is determined to which sector the symbol currently displayed in the main chart belongs and the script displays it in the context of the other symbols in the sector.  
  
By selecting a suitable chart time frame and time range, you can quickly determine which symbols in the sector are stronger or weaker and which are more or less strongly correlated.  
  
The following symbols are best suited for a quick trial, as the sectors are preset for these:  
  
CL1!,ES1!,6A1!,6B1!,6c1!,6E1!,6J1!,6M1!,6N1!,6S1!,GC1!,GF1!,HE1!,HG1!,HO1!,LBR1!,LE1!,NG1!,NQ1!,PA1!,PL1!,RB1!,SI1!,YM1!,ZB1!,ZC1!,ZF1!,ZL1!,ZM1!,ZN1!,ZO1!,ZR1!,ZS1!,ZT1!,ZW1!,CC1!,CT1!,DX1!,KC1!,OJ1!,SB1!,RTY1!  
  
You can also use the script to compare any symbols (e.g. different shares) with each other. Preferably use the "Custom" sector for this.
Script:
------------


// This source code is subject to the terms of the Mozilla Public License 2.0 at https://mozilla.org/MPL/2.0/  
// © Kaschko  
  
//@version=5  
indicator("Sector RS/Corr", overlay = false, format = format.percent, max_lines_count = 500)  
  
// A sector is defined as follows. Aliases and the symbol suffix are optional.  
//  
// Sector name:Symbol suffix:Comma separated list of Symbol[Alias]  
//  
// Examples:  
//  
// "Energies:1!:CL,HO,NG,RB"  
// This defines the sector "Energies" using continous futures contracts of crude oil,heating oil,natural gas and gasoline  
//  
// "Currencies::AXY[AUD],BXY[GBP],CXY[CAD],EXY[EUR],JXY[JPY],ZXY[NZD],SXY[CHF],DXY[USD]"  
// This defines the sector "Currencies" using various currency indices, creating a simple currency strength meter  
  
// Display  
_sector     = input.string(group = "Display", title = "Sector", options = ["Auto-select","Sector #1","Sector #2","Sector #3","Sector #4","Sector #5","Sector #6","Sector #7","Sector #8","Sector #9","Sector #10"], defval = "Auto-select", display = display.none)  
_width      = input.int   (group = "Display", title = "Line width", defval = 3, minval = 1, maxval = 10, display = display.none)  
_showZL     = input.bool  (group = "Display", title = "Display zero line", defval = true, display = display.none)  
// Futures  
_usac       = input.bool  (group = "Futures", title = "Use settlement as close", defval = false, display = display.none)  
_ubac       = input.bool  (group = "Futures", title = "Use back-adjusted contracts", defval = false, display = display.none)  
// Sectors  
_sector01   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #1" , defval = "Energies:1!:CL,HO,NG,RB", display = display.none)  
_sector02   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #2" , defval = "Currencies:1!:6A,6B,6C,6E,6J,6M,6N,6S", display = display.none)  
_sector03   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #3" , defval = "Metals:1!:GC,HG,PA,PL,SI", display = display.none)  
_sector04   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #4" , defval = "Meats:1!:GF,HE,LE", display = display.none)  
_sector05   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #5" , defval = "Softs:1!:LBR,CC,CT,KC,OJ,SB", display = display.none)  
_sector06   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #6" , defval = "Indices:1!:ES,NQ,YM,RTY", display = display.none)  
_sector07   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #7" , defval = "Interest:1!:ZB,ZN,ZF,ZT", display = display.none)  
_sector08   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #8" , defval = "Grains:1!:ZC,ZL,ZM,ZO,ZR,ZS,ZW", display = display.none)  
_sector09   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #9" , defval = "Crypto:1!:BTC,ETH", display = display.none)  
_sector10   = input.string(group = "Sector:Suffix:Symbols(comma separated)", title = "Sector #10", defval = "Custom::AAPL,GOOG,META,MSFT", display = display.none)  
// Legend  
_lgndX      = input.string(group = "Legend" , title = "Horizontal position", options = ["left","center","right"], defval = "right", display = display.none)  
_lgndY      = input.string(group = "Legend" , title = "Vertical position", options = ["top","middle","bottom"], defval = "top", display = display.none)  
_tsize      = input.string(group = "Legend" , title = "Font size", options = ["auto","tiny","small", "normal", "large", "huge"], defval = "auto", display = display.none)  
  
var bool _auto = _sector == "Auto-select"  
  
_color00 = input.color(group = "Colors", title = "Symbol #1" , defval = #9B05AF)  
_color01 = input.color(group = "Colors", title = "Symbol #2" , defval = #098EE3)  
_color02 = input.color(group = "Colors", title = "Symbol #3" , defval = #F01F9E)  
_color03 = input.color(group = "Colors", title = "Symbol #4" , defval = #8CDD53)  
_color04 = input.color(group = "Colors", title = "Symbol #5" , defval = #F3D721)  
_color05 = input.color(group = "Colors", title = "Symbol #6" , defval = #258DAB)  
_color06 = input.color(group = "Colors", title = "Symbol #7" , defval = #FF9500)  
_color07 = input.color(group = "Colors", title = "Symbol #8" , defval = #C22106)  
_color08 = input.color(group = "Colors", title = "Symbol #9" , defval = #FB8667)  
_color09 = input.color(group = "Colors", title = "Symbol #10", defval = #47F090)  
  
var _fsize  = switch _tsize  
    "auto"   => size.auto  
    "tiny"   => size.tiny  
    "small"  => size.small  
    "normal" => size.normal  
    "large"  => size.large  
    "huge"   => size.huge  
  
var _a_color = array.from(_color00,_color01,_color02,_color03,_color04,_color05,_color06,_color07,_color08,_color09)  
  
// get comma separated list of symbols  
get_symbols(simple string _sect) =>  
    string _symbols = na  
    i = str.length(_sect)-1  
    while i >= 0  
        if str.substring(_sect,i,i+1) == ":"  
            _symbols := str.substring(_sect,i+1)  
            break  
        i := i - 1  
    // remove aliases, if any  
    while str.contains(_symbols,"]")  
        _p1 = str.pos(_symbols,"[")  
        _p2 = str.pos(_symbols,"]")  
        _symbols := str.substring(_symbols,0,_p1) + str.substring(_symbols,_p2+1)  
    "," + _symbols + ","  
  
// get comma separated list of aliases  
get_aliases(simple string _sect) =>  
    string _symbols = na  
    string _aliases = ","  
    i = str.length(_sect)-1  
    while i >= 0  
        if str.substring(_sect,i,i+1) == ":"  
            _symbols := str.substring(_sect,i+1)  
            break  
        i := i - 1  
    // extract aliases, if any  
    while str.contains(_symbols,"]")  
        _p1 = str.pos(_symbols,"[")  
        _p2 = str.pos(_symbols,"]")  
        _aliases := _aliases + str.substring(_symbols,_p1+1,_p2) + ","  
        _symbols := str.substring(_symbols,_p2+1)  
    if _aliases == ","  
        _aliases := na  
    _aliases  
  
simple string _s_sector01  = get_symbols(_sector01)  
simple string _s_sector02  = get_symbols(_sector02)  
simple string _s_sector03  = get_symbols(_sector03)  
simple string _s_sector04  = get_symbols(_sector04)  
simple string _s_sector05  = get_symbols(_sector05)  
simple string _s_sector06  = get_symbols(_sector06)  
simple string _s_sector07  = get_symbols(_sector07)  
simple string _s_sector08  = get_symbols(_sector08)  
simple string _s_sector09  = get_symbols(_sector09)  
simple string _s_sector10  = get_symbols(_sector10)  
  
simple string _s_aliases01 = get_aliases(_sector01)  
simple string _s_aliases02 = get_aliases(_sector02)  
simple string _s_aliases03 = get_aliases(_sector03)  
simple string _s_aliases04 = get_aliases(_sector04)  
simple string _s_aliases05 = get_aliases(_sector05)  
simple string _s_aliases06 = get_aliases(_sector06)  
simple string _s_aliases07 = get_aliases(_sector07)  
simple string _s_aliases08 = get_aliases(_sector08)  
simple string _s_aliases09 = get_aliases(_sector09)  
simple string _s_aliases10 = get_aliases(_sector10)  
  
// get nth symbol root from sector string (indexing starts with 0)  
get_root(simple string _symstr,simple int _idx) =>  
    int    _nth = -1  
    int    _len = str.length(_symstr)  
    string _ret = na  
    i = 0  
    // cannot use for loop and/or if statements due to their side effects  
    while i < _len  
        _chr = str.substring(_symstr,i,i+1)  
        while _chr != "," and _nth == _idx  
            _ret := _ret + _chr  
            break  
        while _chr == ","  
            _nth := _nth + 1  
            break  
        i := i + 1  
    _ret  
  
// get nth alias from sector string (indexing starts with 0)  
get_alias(simple string _aliasstr,simple int _idx) =>  
    int    _nth = -1  
    int    _len = str.length(_aliasstr)  
    string _ret = na  
    i = 0  
    // cannot use for loop and/or if statements due to their side effects  
    while i < _len  
        _chr = str.substring(_aliasstr,i,i+1)  
        while _chr != "," and _nth == _idx  
            _ret := _ret + _chr  
            break  
        while _chr == ","  
            _nth := _nth + 1  
            break  
        i := i + 1  
    _ret  
  
// get suffix of symbols in selected sector  
get_suffix(simple string _sect) =>  
    _sectstr = switch _sect  
        "Sector #1"   => _sector01  
        "Sector #2"   => _sector02  
        "Sector #3"   => _sector03  
        "Sector #4"   => _sector04  
        "Sector #5"   => _sector05  
        "Sector #6"   => _sector06  
        "Sector #7"   => _sector07  
        "Sector #8"   => _sector08  
        "Sector #9"   => _sector09  
        "Sector #10"  => _sector10  
    _p1 = str.pos(_sectstr,":") + 1  
    _p2 = str.pos(str.substring(_sectstr,_p1),":")  
    str.substring(_sectstr,_p1,_p1+_p2)  
  
// get symbol string for selected sector  
get_symstr(simple string _sect) =>  
    _symbols = switch _sect  
        "Sector #1"   => _s_sector01  
        "Sector #2"   => _s_sector02  
        "Sector #3"   => _s_sector03  
        "Sector #4"   => _s_sector04  
        "Sector #5"   => _s_sector05  
        "Sector #6"   => _s_sector06  
        "Sector #7"   => _s_sector07  
        "Sector #8"   => _s_sector08  
        "Sector #9"   => _s_sector09  
        "Sector #10"  => _s_sector10  
  
// get alias string for selected sector  
get_aliasstr(simple string _sect) =>  
    _symbols = switch _sect  
        "Sector #1"   => _s_aliases01  
        "Sector #2"   => _s_aliases02  
        "Sector #3"   => _s_aliases03  
        "Sector #4"   => _s_aliases04  
        "Sector #5"   => _s_aliases05  
        "Sector #6"   => _s_aliases06  
        "Sector #7"   => _s_aliases07  
        "Sector #8"   => _s_aliases08  
        "Sector #9"   => _s_aliases09  
        "Sector #10"  => _s_aliases10  
  
// get series  
get_series(int _no,string _sect) =>  
    _symbols = get_symstr(_sect)  
    _root    = get_root(_symbols,_no)  
    _tpfix   = '={"settlement-as-close":' + (_usac ? "true" : "false") + (_ubac ? ',"backadjustment":"default"' : '') + ',"symbol":"'  
    _tsfix   = get_suffix(_sect) + '"}'  
    _ticker  = _tpfix + _root + _tsfix  
    // return series  
    request.security(_ticker, timeframe.period, close, gaps = barmerge.gaps_on, ignore_invalid_symbol = true)  
  
// get sector of symbol  
get_sector(simple string _symbol) =>  
    _smbl = "," + _symbol + ","  
    str.contains(_s_sector01     ,_smbl) ? "Sector #1"  :   
         str.contains(_s_sector02,_smbl) ? "Sector #2"  :  
         str.contains(_s_sector03,_smbl) ? "Sector #3"  :  
         str.contains(_s_sector04,_smbl) ? "Sector #4"  :  
         str.contains(_s_sector05,_smbl) ? "Sector #5"  :  
         str.contains(_s_sector06,_smbl) ? "Sector #6"  :  
         str.contains(_s_sector07,_smbl) ? "Sector #7"  :  
         str.contains(_s_sector08,_smbl) ? "Sector #8"  :  
         str.contains(_s_sector09,_smbl) ? "Sector #9"  :  
         str.contains(_s_sector10,_smbl) ? "Sector #10" : na  
  
// get name of sector  
get_sectname(simple string _sect) =>  
    _name = switch _sect  
        "Sector #1"   => str.substring(_sector01,0,str.pos(_sector01,":"))  
        "Sector #2"   => str.substring(_sector02,0,str.pos(_sector02,":"))  
        "Sector #3"   => str.substring(_sector03,0,str.pos(_sector03,":"))  
        "Sector #4"   => str.substring(_sector04,0,str.pos(_sector04,":"))  
        "Sector #5"   => str.substring(_sector05,0,str.pos(_sector05,":"))  
        "Sector #6"   => str.substring(_sector06,0,str.pos(_sector06,":"))  
        "Sector #7"   => str.substring(_sector07,0,str.pos(_sector07,":"))  
        "Sector #8"   => str.substring(_sector08,0,str.pos(_sector08,":"))  
        "Sector #9"   => str.substring(_sector09,0,str.pos(_sector09,":"))  
        "Sector #10"  => str.substring(_sector10,0,str.pos(_sector10,":"))  
  
var string _sect = _auto ? get_sector(syminfo.root) : _sector  
  
_sym00 = get_series(0,_sect)  
_sym01 = get_series(1,_sect)  
_sym02 = get_series(2,_sect)  
_sym03 = get_series(3,_sect)  
_sym04 = get_series(4,_sect)  
_sym05 = get_series(5,_sect)  
_sym06 = get_series(6,_sect)  
_sym07 = get_series(7,_sect)  
_sym08 = get_series(8,_sect)  
_sym09 = get_series(9,_sect)  
  
var _a_series  = array.new<string>(0)  
var _a_aliases = array.new<string>(0)  
  
// close of left visible bar for all symbols in sector  
var float _start00 = na  
var float _start01 = na  
var float _start02 = na  
var float _start03 = na  
var float _start04 = na  
var float _start05 = na  
var float _start06 = na  
var float _start07 = na  
var float _start08 = na  
var float _start09 = na  
  
if time == chart.left_visible_bar_time  
    _start00 := _sym00  
    _start01 := _sym01  
    _start02 := _sym02  
    _start03 := _sym03  
    _start04 := _sym04  
    _start05 := _sym05  
    _start06 := _sym06  
    _start07 := _sym07  
    _start08 := _sym08  
    _start09 := _sym09  
    _symbols = get_symstr  (_sect)  
    _aliases = get_aliasstr(_sect)  
    if not na(_start00)  
        array.push(_a_series ,get_root (_symbols,0))  
        array.push(_a_aliases,get_alias(_aliases,0))  
    if not na(_start01)  
        array.push(_a_series ,get_root (_symbols,1))  
        array.push(_a_aliases,get_alias(_aliases,1))  
    if not na(_start02)  
        array.push(_a_series ,get_root (_symbols,2))  
        array.push(_a_aliases,get_alias(_aliases,2))  
    if not na(_start03)  
        array.push(_a_series ,get_root (_symbols,3))  
        array.push(_a_aliases,get_alias(_aliases,3))  
    if not na(_start04)  
        array.push(_a_series ,get_root (_symbols,4))  
        array.push(_a_aliases,get_alias(_aliases,4))  
    if not na(_start05)  
        array.push(_a_series ,get_root (_symbols,5))  
        array.push(_a_aliases,get_alias(_aliases,5))  
    if not na(_start06)  
        array.push(_a_series ,get_root (_symbols,6))  
        array.push(_a_aliases,get_alias(_aliases,6))  
    if not na(_start07)  
        array.push(_a_series ,get_root (_symbols,7))  
        array.push(_a_aliases,get_alias(_aliases,7))  
    if not na(_start08)  
        array.push(_a_series ,get_root (_symbols,8))  
        array.push(_a_aliases,get_alias(_aliases,8))  
    if not na(_start09)  
        array.push(_a_series ,get_root (_symbols,9))  
        array.push(_a_aliases,get_alias(_aliases,9))  
  
plot(((_sym00/_start00)-1)*100, title = "Symbol #1" , color = _color00, linewidth = _width)  
plot(((_sym01/_start01)-1)*100, title = "Symbol #2" , color = _color01, linewidth = _width)  
plot(((_sym02/_start02)-1)*100, title = "Symbol #3" , color = _color02, linewidth = _width)  
plot(((_sym03/_start03)-1)*100, title = "Symbol #4" , color = _color03, linewidth = _width)  
plot(((_sym04/_start04)-1)*100, title = "Symbol #5" , color = _color04, linewidth = _width)  
plot(((_sym05/_start05)-1)*100, title = "Symbol #6" , color = _color05, linewidth = _width)  
plot(((_sym06/_start06)-1)*100, title = "Symbol #7" , color = _color06, linewidth = _width)  
plot(((_sym07/_start07)-1)*100, title = "Symbol #8" , color = _color07, linewidth = _width)  
plot(((_sym08/_start08)-1)*100, title = "Symbol #9" , color = _color08, linewidth = _width)  
plot(((_sym09/_start09)-1)*100, title = "Symbol #10", color = _color09, linewidth = _width)  
  
if barstate.islastconfirmedhistory  
    // table  
    var table _table = table.new(_lgndY + "_" + _lgndX, 1, array.size(_a_series)+1)  
    table.cell(_table, 0, 0, get_sectname(_auto ? get_sector(syminfo.root) : _sector), text_size = _fsize, text_color = #ffffff, bgcolor = #868686)  
    for i = 0 to array.size(_a_series)-1  
        _text = array.get(_a_aliases,i)  
        if na(_text)  
            _text := array.get(_a_series,i)  
        table.cell(_table, 0, i+1, _text, text_size = _fsize, text_color = #ffffff, bgcolor = array.get(_a_color,i))  
  
hline(_showZL ? 0 : na, title = "Zero", color = #868686, linewidth = 1)
