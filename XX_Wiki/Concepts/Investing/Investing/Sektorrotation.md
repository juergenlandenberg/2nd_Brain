---
title: "Sektorrotation"
type: knowledge-source
status: draft
main_topic: "JvL Invest"
creator: "Erna"
maintainer: "Erna"
content_reviewer: "Jürgen"
section: "Investing"
colorcode: "Blue"
tags:
  - MOC/Investing
sources:
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Equities/Sektorrotation.md"
source_file_id: "1E0Q4aup412VcGaigQLNngiRNqrrgafuE"
---

# Sektorrotation

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[03_Tags/JvL-Invest-Futures|Zyklen und Trends]]


![[40_ATTACHMENTS/JvL_Invest/Clippings/Pasted image 20260224134957.png]]

US Sektoren

|      |                        |
| ---- | ---------------------- |
| XLC  | Communication          |
| XLY  | Consumer Discretionary |
| XLP  | Consumer Staples       |
| XLE  | Energy                 |
| XLF  | Financials             |
| XLV  | Health Care            |
| XLI  | Industrials            |
| XLB  | Materials              |
| XLRE | Real Estate            |
| XLK  | Technology             |
| XLU  | Utilities              |
EU Sektoren



## Methodik ([MSWerkzeug - Sektorrotation](https://msw.flxn.de/tool/sector/))

Die Daten werden mit folgender Methode berechnet:

1. Die Kurse werden geladen und relativ zum ersten Wert des Zeitraums normalisiert
2. Es wird der relative Kurs der Aktie zum Benchmark berechnet
3. Für diesen relativen Kurs wird ein rolling mean und Standardabweichung mit window size von 50 Tagen berechnet
4. Das JdK RS-Ratio berechnet sich dann wie folgt: `100 + ((relative - rolling_mean) / rolling_std)`
5. Für das Momentum wird für jeden Tag der Kurs relativ zum Kurs 10 vor Tagen berechnet
6. Es wird wieder normalisiert mit einem rolling mean von 50 Tagen
7. Das JdK RS-Momentum berechnet ich dann analog mit: `100 + ((momentum - momentum_rolling_mean) / momentum_rolling_std)`
8. Zuletzt werden RS-Ratio und RS-Momentum noch mit einem rolling mean von 10 Tagen geglättet
![[40_ATTACHMENTS/JvL_Invest/Clippings/Pasted image 20260224135222.png]]

![[40_ATTACHMENTS/JvL_Invest/Clippings/Pasted image 20260224135334.png]]



![[40_ATTACHMENTS/JvL_Invest/Clippings/Pasted image 20260224135550.png]]



<!-- Ambiguous image basenames retained for review:
Pasted image 20260224134957.png: Clippings/Pasted image 20260224134957.png, 06_Clippings/Pasted image 20260224134957.png
Pasted image 20260224135222.png: Clippings/Pasted image 20260224135222.png, 06_Clippings/Pasted image 20260224135222.png
Pasted image 20260224135334.png: Clippings/Pasted image 20260224135334.png, 06_Clippings/Pasted image 20260224135334.png
Pasted image 20260224135550.png: Clippings/Pasted image 20260224135550.png, 06_Clippings/Pasted image 20260224135550.png
-->
