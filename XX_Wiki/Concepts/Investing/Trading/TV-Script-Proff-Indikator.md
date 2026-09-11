---
title: "TV Script - Proff-Indikator"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Proff-Indikator.md"
source_file_id: "1FfIfsI9Lig6XBdMcp8MWkCIBRCqTR1bu"
---

# TV Script - Proff-Indikator

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[Futures]]
[[TradingView]]

Title: TV Script - Proff-Indikator 
Date: 2025-11-13 
Time: 18:39 

Purpose: 

Script:
------------






|                                                                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| //@version=5indicator(title = "My Proff Indicator", shorttitle = "Proff", overlay = true, precision = 4, scale = scale.none)plot(ta.sma(close-open,14), color = #00c000, linewidth = 2) |
