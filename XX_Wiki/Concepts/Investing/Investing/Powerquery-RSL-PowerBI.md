---
title: "Powerquery RSL PowerBI"
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
  - "Google Drive / 10_RAW / Archive Imports / JvL_Invest / Investing/TOOLS/Powerquery RSL PowerBI.md"
source_file_id: "1qJHI8U7CvdatBa4GO6KLCcoAJKbgJwfg"
---

# Powerquery RSL PowerBI

Navigation: [[JvL-Invest]] · [[JvL-Invest-Investing]] · [[JvL-Invest-Futures-Options]] · [[JvL-Invest-Tax]]

> Imported from immutable RAW material. This is a review draft; source claims are not recommendations.

let
    // 1. Load all files from folder
    Source = Folder.Files("D:\YourFolderPathHere"),

    // 2. Keep only CSV files
    #"Filtered CSV" = Table.SelectRows(Source, each Text.EndsWith([Name], ".csv")),

    // 3. Extract date from filename: RSL_S&P500_2026-01-18.csv
    #"Added FileDate" = Table.AddColumn(#"Filtered CSV", "FileDate", each 
        Date.FromText(Text.BetweenDelimiters([Name], "_", ".csv")), type date),

    // 4. Add WorkWeek number
    #"Added WorkWeek" = Table.AddColumn(#"Added FileDate", "WorkWeek", each 
        Date.WeekOfYear([FileDate], Day.Monday), Int64.Type),

    // 5. Combine files
    #"Imported CSV" = Table.AddColumn(#"Added WorkWeek", "Data", each Csv.Document([Content], [Delimiter=",", Encoding=65001, QuoteStyle=QuoteStyle.Csv])),

    // 6. Promote headers inside each CSV
    #"Promoted Headers" = Table.TransformColumns(#"Imported CSV", {"Data", each Table.PromoteHeaders(_, [PromoteAllScalars=true])}),

    // 7. Expand the CSV content
    #"Expanded Data" = Table.ExpandTableColumn(#"Promoted Headers", "Data",
        Table.ColumnNames(#"Promoted Headers"{0}[Data])),

    // 8. Convert numeric columns (fixes your "Record" error)
    #"Changed Types" = Table.TransformColumnTypes(#"Expanded Data", {
        {"Price", type number},
        {"Simple Moving Average (26) 1 week", type number},
        {"Simple Moving Average (3) 1 month", type number}
    }),

    // 9. Add RSL26 = Price / SMA26
    #"Added RSL26" = Table.AddColumn(#"Changed Types", "RSL26", each 
        [Price] / [Simple Moving Average (26) 1 week], type number),

    // 10. Add RSL13 = Price / SMA13
    #"Added RSL13" = Table.AddColumn(#"Added RSL26", "RSL13", each 
        [Price] / [Simple Moving Average (3) 1 month], type number)

in
    #"Added RSL13"
