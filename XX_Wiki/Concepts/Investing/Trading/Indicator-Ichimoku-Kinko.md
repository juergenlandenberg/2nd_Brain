---
title: "Indicator Ichimoku Kinko"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/Indikatoren&Oszillatoren/Indicator Ichimoku Kinko.md"
source_file_id: "1fCBBT1ICB73KP7ebgEzjMhJhFCdrzx-I"
---

# Indicator Ichimoku Kinko

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

Title: Indicator Ichimoku Kinko 
Date: 2025-12-28 
Time: 12:28 

[[Indikator]]


Blau Basis - Standard Baseline (9D)
Rot - Kiyou Sen - 26T


Wolken

Grün Senkuspan A
Vorauseilende PEriode

Mitte Tot+blau 26 Perioden in Zukunft (26 incl aktueller Tag)

Rot Senku Span B = Mittelwert darlehen 52 Perioden (Hoch/Tief) 26 Wochen in die Zukunft projeziert


Signale

Kurz > Lang - Kauf (Blau über Rot)
Golden Cross : Kurs kreuzt Wolkje
Kumo Break out

--------


# Ichimoku Cloud

**Indicator Type**: Standalone

**Chart Type**: Interactive Chart only

The Ichimoku Cloud is a collection of technical indicators that show support and resistance levels, as well as momentum and trend direction. It does this by taking multiple averages and plotting them on the chart. It also uses these figures to compute a "cloud" which attempts to forecast where the price may find support or resistance in the future.

The Ichimoku cloud was developed by Goichi Hosoda, a Japanese journalist, and published in the late 1960s. It provides more data points than the standard candlestick chart. While it seems complicated at first glance, those familiar with how to read the charts often find it easy to understand with well-defined trading signals.

- The Ichimoku Cloud is composed of five lines or calculations, two of which compose a cloud where the difference between the two lines is shaded in.
- The lines include a nine-period average, 26-period average, an average of those two averages, a 52-period average, and a lagging closing price line.
- The Cloud is a key part of the indicator. When price is below the cloud the trend is down. When price is above the cloud the trend is up.
- The above trend signals are strengthened if the Cloud is moving in the same direction as price. For example, during an uptrend the top of the Cloud is moving up, or during a downtrend the bottom of the cloud is moving down.

![Ichimoku Cloud](https://assets.barchart.com/img/studies/ichimoku.png)

In order to see the pattern of the cloud in the future on the chart, we recommend changing the "Right Margin Free Space" in the chart's Settings to reflect the 'Displacement' value of the study. Our default for 'Displacement' is set at 26 periods; therefore if you click on chart "SETTINGS", select "SCALE" and enter 26 into the "Right Margin Free Space" box and click APPLY, this will adjust the chart accordingly.

![Ichimoku Cloud](https://assets.barchart.com/img/studies/ichimoku-right-margin.png)

### Formula

The following are the five formulas for the lines that compose the Ichimoku cloud indicator.

Conversion Line (tenkan sen) = 9-PH + 9-PL / 2  
Base Line (kijun sen) = 26-PH + 26-PL / 2  
Leading Span A (senkou span A) = CL + Base Line / 2  
Leading Span B (senkou span B) = 52-PH + 52-PL / 2  
Lagging Span (chikou span) = Close plotted 26 periods in the past  
  
where:  
PH = Period high  
PL = Period low  
CL = Conversion line

The highs and lows are the highest and lowest prices seen during the period. For example, the highest and lowest prices seen over the last nine days in the case of the conversion line. Adding the Ichimoku cloud indicator to your chart will do the calculations for you, but if you want to calculate it by hand here are the steps.

1. Calculate the Conversion Line and Base Line.
2. Calculate Leading Span A based on the prior calculations. Once calculated, this data point is plotted 26 periods in the future.
3. Calculate Leading Span B. Plot this data point 26 periods into the future.
4. For the Lagging span, plot the closing price 26 periods in the past on the chart.
5. The difference between Span A and Span B is colored in to create the cloud.
6. When Leading Span A is above Leading Span B color the cloud green. When Leading Span A is below Leading Span B, color the cloud red.
7. The above steps will create one data point. To create the lines, as each period comes to an end go through the steps again to create new data points for that period. Connect the data points to each other to create the lines and cloud appearance.

The technical indicator shows relevant information at a glance using averages.

The overall trend is up when price is above the cloud, down when price is below the cloud, and trendless or transitioning when price is in the cloud.

When Leading Span A is rising and above Leading Span B, this helps confirm the uptrend and space between the lines is typically colored green. When Leading Span A is falling and below Leading Span B, this helps confirm the downtrend. The space between the lines is typically colored red, in this case.

Traders will often use the Cloud as an area of support and resistance depending on the relative location of the price. The Cloud provides support/resistance levels that can be projected into the future. This sets the Ichimoku Cloud apart from many other technical indicators that only provide support and resistance levels for the current date and time.

Traders should use the Ichimoku Cloud in conjunction with other technical indicators to maximize their risk-adjusted returns. For example, the indicator is often paired with the Relative Strength Index (RSI), which can be used to confirm momentum in a certain direction. It's also important to look at the bigger trends to see how the smaller trends fit within them. For example, during a very strong downtrend, the price may push into the cloud or slightly above it, temporarily, before falling again. Only focusing on the indicator would mean missing the bigger picture that the price was under strong longer-term selling pressure.

Crossovers are another way the indicator can be used. Watch for the conversion line to move above the base line, especially when price is above the cloud. This can be a powerful buy signal. One option is to hold the trade until the conversion line drops back below the base line. Any of the other lines could be used as exit points as well.

**The Difference Between the Ichimoku Cloud and Moving Averages**

While the Ichimoku Cloud uses averages, they are different than a typical moving average. Simple moving averages take closing prices, adds them up, and divide that total by how many closing prices there are. In a 10-period moving average, the closing prices for the last 10 periods are added, then divided by 10 to get the average.

Notice how the calculations for the Ichimoku cloud are different? They are based on highs and lows over a period, and then divided by two. Therefore, Ichimoku averages will be different than traditional moving averages, even if the same number of periods are used.

One indicator is not better than another, they just provide information in different ways.

**Limitations of Using the Ichimoku Cloud**

The indicator can make a chart look busy with all the lines. To remedy this, most charting software allows certain lines to be hidden. For example, all the lines can be hidden except for the Leading Span A and B which create the cloud. Each trader needs to focus on which lines provide the most information, and then consider hiding the rest if all the lines are distracting.

Another limitation of the Ichimoku Cloud is that it is based on historical data. While two of these data points are plotted in the future, there is nothing in the formula that is inherently predictive. Averages are simply being plotted in the future.

The cloud can also become irrelevant for long periods of time, as the price remains way above or below it. At times like these, the conversion line, base line, and their crossovers become more important, as they generally stick closer to the price.

Parameters

- PeriodConversionLine: (9) - used in the Conversion Line calculation
- Period BaseLine: (26) - used in the Base Line calculation
- PeriodLaggingSpan2: (52) - used in the Leading Span calculation
- Displacement: (26) - the number of periods in the future to displace the study

Source: [Investopedia.com](https://www.investopedia.com/terms/i/ichimoku-cloud.asp)
