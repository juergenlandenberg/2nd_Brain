# Finn – Investmentanalysen: RSL

**Status:** fachlich festgelegt, technische Umsetzung noch nicht freigegeben  
**Stand:** 2026-09-07

## Navigation

- [[JvL-Invest]]
- [[JvL-Invest-Investing]]
- [[JvL-Invest-Futures-Options]]
- [[Finn-Agent-Profile]]

Im Dashboard gibt es links den Hauptbereich **Strategien** mit zunächst zwei eigenen Seiten:

- **COT1**
- **RSL**

Der Finn-Bereich bleibt fachlich vom Lanvision-EK-Bereich getrennt.

## RSL-Seite

Finn liefert regelmäßig die fünf aktuell betrachteten Markt-Bundles. Für jedes Bundle führt Finn die Top-10-Liste fortlaufend je Kalenderwoche weiter.

Die RSL-Seite zeigt:

- fünf Markt-Bundles;
- pro Bundle eine eigene Kachel;
- pro Kachel die Top 10 des ausgewählten Wochenstands;
- Standardsicht: aktuelle Woche;
- Standardsortierung: **RSL 26W absteigend**.

## Tabelle pro Kachel

Die Top-10-Tabelle enthält sieben Spalten:

1. Symbol
2. Description
3. RSL 26W
4. RSL 3M
5. Price to Earnings
6. Free Cash Flow
7. Market Cap

## Zeitsteuerung

Oben auf der RSL-Seite befindet sich ein Schieberegler für die letzten **26 Wochen**.

- Der Regler wählt eine Kalenderwoche bzw. einen historischen Wochenstand.
- Die Wochenzahl wird sichtbar angezeigt.
- Die Skala bzw. Beschriftung erfolgt in **5-Wochen-Schritten**.
- Wird der Regler in die Vergangenheit bewegt, wechseln alle fünf Kacheln auf den Datenstand der ausgewählten Woche.
- Der einzige fachliche Filter ist **Market Cap**.
- Es gibt keine zusätzlichen Filter für RSL 26W, RSL 3M, P/E, Free Cash Flow, Symbol oder Description.

## Daten- und Historienmodell

- Finn ist Eigentümer und Pfleger der fachlichen Wochenwerte.
- Die Quelle wird fortlaufend um neue Wochen ergänzt.
- Für die aktuelle Woche werden zunächst die von Finn gelieferten fünf Bundles und Top-10-Werte angezeigt.
- Historische Auswahl ist erst vollständig möglich, sobald Finn die Historie liefert.
- Fehlende Wochen müssen eindeutig als „keine Daten vorhanden“ angezeigt werden; es darf nicht stillschweigend die aktuelle Woche dargestellt werden.
- Keine synthetischen oder erfundenen Historienwerte.

## Noch zu definieren

- Namen und fachliche Definition der fünf Markt-Bundles.
- Eindeutiger Wochenbezug: Kalenderwoche/Jahr oder ISO-Woche.
- Einheit und Währung von Price to Earnings, Free Cash Flow und Market Cap.
- Exakte Market-Cap-Filterbedienung und Wertebereich.
- Datenformat bzw. API-Vertrag zwischen Finn und dem Dashboard.
- Verhalten bei unvollständigen Daten innerhalb einer Woche.

## Detailansicht je Markt-Bundle — Variante 1 beschlossen

Unter jeder Bundle-Kachel führt ein Link auf eine eigene Detailansicht des Markt-Bundles.

Die Detailansicht zeigt für die **aktuelle Top 10** rückwirkend den Verlauf über zunächst **12 Wochen**:

- **RSL 3M:** Liniendiagramm mit X-Achse = Kalenderwochen und Y-Achse = RSL 3M;
- **RSL 26W:** analoges Liniendiagramm mit Y-Achse = RSL 26W;
- zehn Linien je Diagramm, eine Linie pro Symbol;
- identische Symbolauswahl für beide Diagramme;
- Auswahl/Mouseover hebt das Symbol in beiden Diagrammen hervor, die übrigen Linien werden gedämpft;
- Tooltip zeigt Woche, Symbol und exakten RSL-Wert;
- fehlende historische Werte werden nicht als `0` interpretiert und nicht als künstlicher Datenpunkt ergänzt;
- bei einzelnen fehlenden Wochen verbindet die Linie den letzten vorhandenen mit dem nächsten vorhandenen Datenpunkt direkt (visuelle lineare Verbindung über die Lücke);
- bei längeren oder am Rand liegenden Lücken bleibt die Linie entsprechend unterbrochen;
- die Datentabelle kennzeichnet fehlende Wochen ausdrücklich als nicht vorhanden;
- eine kompakte Datentabelle unter dem jeweiligen Diagramm ergänzt die grafische Darstellung.

Die Top-10-Mitglieder stammen aus dem ausgewählten aktuellen Wochenstand und werden historisch verfolgt. Es wird nicht für jede historische Woche eine neue Top 10 eingesetzt.

**Entscheidung:** Variante 1 (zwei klassische Liniendiagramme mit interaktiver Symbol-Hervorhebung). Heatmap und Small Multiples werden nicht Bestandteil des ersten Umfangs.

Die Darstellung verwendet ausschließlich Finns historische Wochenwerte. Bis Finn die Historie liefert, werden fehlende Wochen sichtbar als nicht verfügbar angezeigt.
