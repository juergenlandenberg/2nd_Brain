---
title: "Indicator ADX"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Indikatoren&Oszillatoren/Indicator ADX.md"
source_file_id: "1BYfTOc9ZTdT2fCzM7or7NEbA6oelOI_8"
---

# Indicator ADX

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

[[03_Tags/JvL-Invest-Trading|Indikator]]


ADX (Green>red UND ADX >25) Rise ADX - Strong Trend
	ADX<25 UND red>gree - Seitwärtstrend


# Average Directional Index (ADX)

**Indicator Type**: Standalone

Average Directional Index Technical Indicator (ADX) helps to determine if there is a price trend. It was developed and described in detail by Welles Wilder in his book "New concepts in technical trading systems".

The simplest trading method based on the system of directional movement implies comparison of two direction indicators: the 14-period +DI, and the 14-period -DI. To do this, one either puts the charts of indicators one on top of the other, or +DI is subtracted from -DI. W. Wilder recommends buying when +DI is higher than -DI, and selling when +DI sinks lower than -DI.

To these simple commercial rules Wells Wilder added "a rule of points of extremum". It is used to eliminate false signals and decrease the number of deals. According to the principle of points of extremum, the "point of extremum" is the point when +DI and -DI cross each other. If +DI raises higher than -DI, this point will be the maximum price of the day when they cross. If +DI is lower than -DI, this point will be the minimum price of the day they cross.

The point of extremum is used then as the market entry level. Thus, after the signal to buy (+DI is higher than -DI) one must wait till the price has exceeded the point of extremum, and only then buy. However, if the price fails to exceed the level of the point of extremum, one should retain the short position.

**Sample Chart**:

![Average Directional Index](https://assets.barchart.com/img/studies/adx.png)

**Calculation**

Calculating the DMI can actually be broken down into two parts. First, calculating the +DI and -DI, and second, calculating the ADX.

To calculate the +DI and -DI you need to find the +DM and -DM (Directional Movement).  
+DM and -DM are calculated using the High, Low and Close for each period. You can then calculate the following:

Current High - Previous High = UpMove  
Previous Low - Current Low = DownMove

If UpMove > DownMove and UpMove > 0, then +DM = UpMove, else +DM = 0  
If DownMove > Upmove and Downmove > 0, then -DM = DownMove, else -DM = 0

Once you have the current +DM and -DM calculated, the +DM and -DM lines can be calculated and plotted based on the number of user defined periods.

+DI = 100 times Exponential Moving Average of (+DM / Average True Range)  
-DI = 100 times Exponential Moving Average of (-DM / Average True Range)

Now that -+DX and -DX have been calculated, the last step is calculating the ADX.

ADX = 100 times the Exponential Moving Average of the Absolute Value of (+DI - -DI) / (+DI + -DI)

**Parameters:**

- ADX Smoothing (_Interactive Charts only_) - Default of 14. The time period to be used in calculating the ADX which has a smoothing component.
- DI Length (_Period_) - Default of 14. The time period to be used in calculating the DI.
- LEVELS (_Interactive Charts only_): These are used to help determine if the market is trending or not. Above 25 typically indicates the market is trending, whereas below 20 indicates the market is not trending.
