# 2ndB Note- und Graph-Governance

Diese Regeln gelten für alle Notes, die in den konsolidierten 2ndB-Bestand aufgenommen oder dort neu erstellt werden.

## 1. Aussagekräftige Dateinamen

- `README.md` ist als fachlicher Note-Name nicht zulässig.
- Jeder Dateiname beschreibt den Inhalt eindeutig und stabil.
- Der Name soll ohne Ordnerkontext verständlich sein.
- Für Übersichten werden fachliche Namen verwendet, zum Beispiel `Hermes-Operations.md`, `Agents-Index.md` oder `Investment-Cluster.md`.
- Technische Legacy-Dateien mit generischen Namen werden beim Import umbenannt; der ursprüngliche Pfad bleibt in den Metadaten bzw. Quellen erhalten.
- Keine unnötigen Kopien desselben Inhalts unter verschiedenen Namen.

## 2. Keine Inselnoten

- Jede kuratierte Note muss mindestens ein Wikilink zum zuständigen Haupttopic oder Cluster enthalten.
- Eine Note ohne Haupttopic-Link wird nicht als fertig importiert bzw. veröffentlicht markiert.
- Zusätzlich sind sinnvolle Querverbindungen zwischen Notes ausdrücklich erwünscht.
- Links müssen fachlich begründet sein; kein künstliches Link-Spam-Netz.
- `03_Tags` enthält strukturierte Topic-/Cluster-Hubs für Backlinks. Es ist kein klassisches Tag-Verzeichnis.

### Mindestanforderung für eine fertige Note

```markdown
## Haupttopic
- [[Haupttopic]]

## Verknüpfte Notes
- [[Verwandte Note 1]]
- [[Verwandte Note 2]]
```

Bei sehr kleinen Notes reicht mindestens der Haupttopic-Link plus eine Quelle oder ein sinnvoller Nachbarlink.

## 3. Rollen und Freigabe

### Hermes-Notes

- **Creator:** Erna
- **Maintainer:** Erna
- **Content-Prüfung:** Erna nach fachlichem Bedarf; unabhängige Reviews bleiben getrennt dokumentiert.
- Andere Agenten dürfen Vorschläge, Korrekturen und Quellen liefern, aber nicht direkt veröffentlichen.

### Importierte persönliche Vaults

- **Quelle/Import:** Erna bereitet Struktur, Umbenennung, Linkmapping und Konsolidierung vor.
- **Letzter Content-Prüfer:** Jürgen.
- **Fachliche Rollen:** Werden pro Haupttopic festgelegt, bevor der Topic-Import veröffentlicht wird.
- Eine technische Strukturprüfung durch Erna ersetzt nicht Jürgens letzte inhaltliche Freigabe.

## 4. Topic-first Import

Vor jedem größeren Vault-Import müssen feststehen:

1. Haupttopic bzw. Cluster;
2. zulässige Untertopics;
3. Creator und Maintainer;
4. letzter Content-Prüfer;
5. Quellen- und Legacy-Pfad;
6. erwartete Backlinks und Querverbindungen;
7. Ausschlüsse und sensible Inhalte.

Die von Jürgen gelieferte Haupttopic-Liste ist die maßgebliche Routing-Grundlage. Bis sie vorliegt, werden persönliche Vaults nicht endgültig kuratiert oder veröffentlicht.

## 5. Qualitätsgate vor Veröffentlichung

Eine importierte Note darf erst als `active` veröffentlicht werden, wenn:

- der Dateiname aussagekräftig ist;
- mindestens ein Haupttopic-Link vorhanden ist;
- Quellen und Legacy-Pfad nachvollziehbar sind;
- keine Secrets oder privaten Fremdinhalte enthalten sind;
- Rollen und Prüfer für das Topic bekannt sind;
- Querverbindungen geprüft wurden;
- bei persönlichen Vaults Jürgens Content-Freigabe vorliegt.

Unvollständige Notes bleiben als `draft` oder im Import-/Prüfbereich.
