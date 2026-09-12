---
title: "TV Script - Spread (front-back contract in future markets)"
type: knowledge-source
status: draft
main_topic: "JvL Invest"
creator: "Erna"
maintainer: "Erna"
content_reviewer: "Jürgen"
section: "Futures"
colorcode: "Blue"
tags:
  - MOC/Futures
sources:
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Technische Analyse/TradingView-Scripts/TV Script - Spread (front-back contract in future markets).md"
source_file_id: "1Vs1siB8XjdX7uZ0lJlbYhov3OiGromYP"
---

# TV Script - Spread (front-back contract in future markets)

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[03_Tags/JvL-Invest-Futures|Futures]]
[[03_Tags/JvL-Invest-Trading|TradingView]]

Title: TV Script - Spread (front-back contract in future markets) 
Date: 2025-11-13 
Time: 18:29 

Purpose: 
This script can be used in three different modes.  
  
In «price» mode, it displays a line chart of the front contract and one or more back contracts.  
In «absolute» mode, it shows the absolute spread(s) between front and one or more back contracts.  
In «relative» mode, it shows the spreads between front and back contracts relative to each other.  
  
Up to 12 spreads can be displayed on the same chart. You can select the front contract by volume or by calendar. The number of spreads actually displayed depends on the existing contracts and whether they have sufficient volume to calculate a spread.  
  
Optionally, you can display the volume in the legend. This is always the volume of the last bar.
Script: (protected)
------------
