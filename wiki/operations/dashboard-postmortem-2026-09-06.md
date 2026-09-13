# Dashboard-Postmortem: Externer Zugang und Live-Daten

**Datum:** 2026-09-06  
**Projekt:** Lanvision-EK-Dashboard  
**Status:** Fehlerursachen behoben; Learnings verbindlich für künftige Deployments.

## Kurzfassung

Der externe Zugang war zeitweise erreichbar, aber Login und Datenanzeige scheiterten durch mehrere voneinander unabhängige Fehler. Der entscheidende Datenfehler war ein falscher `AUTHORITATIVE_DB_HOST_PATH`: Der VPS verwendete eine synthetische SQLite-Fixture statt Bens autoritativer Datenbank.

## Festgestellte Ursachen

1. **Deployment-Drift:** Das Dockerfile kopiert ein vorgebautes `dist-server`. Lokale Source- und Test-Gates bewiesen nicht, dass der laufende Container denselben Build enthielt.
2. **scrypt-Fehler:** Python erzeugte Produktions-Hashes mit `N=32768, r=8`; Node verwendete ein zu knappes `maxmem`. Der abgefangene Fehler erschien als generisches `401 Ungültige Zugangsdaten`. Korrektur: mindestens 64 MB `maxmem` und Regressionstest mit Produktionsparametern.
3. **Falsche Datenquelle:** `AUTHORITATIVE_DB_HOST_PATH` zeigte auf `test-data/synthetic-buchhaltung.db`. Ein technischer Preflight prüfte Existenz und SQLite-Integrität, aber nicht fachliche Inhalte.
4. **Routing-Lücke:** Caddy leitete `/api/*`, aber zunächst nicht `/auth/*` an den API-Dienst weiter.
5. **UI-Warnungsrauschen:** Fehlende optionale Tabellen wurden als sichtbare Fehler dargestellt, obwohl der Datenvertrag leere optionale Bereiche erlaubt.
6. **Diagnose-Schalter:** `AUTH_REQUIRE_TOTP` war als temporärer Testschalter operativ fehleranfällig; Chat-Maskierung führte zusätzlich dazu, dass `***` literal in `.env` übernommen wurde.

## Verbindliche Gates vor künftigen Abnahmen

- Artefakt-Hash vor Upload prüfen.
- Hash von `dist-server/auth.js` und `dist-server/server.js` lokal und im laufenden Container vergleichen.
- Effektive Container-Umgebung prüfen, nicht nur die Host-`.env`.
- Host-Mountquelle und Container-Ziel prüfen; Datenbank muss Bens read-only SQLite sein.
- Live-Snapshot authentifiziert prüfen: Provenienz, Zählungen, Synthetic-Markierungen und repräsentative Felder.
- Quelle → Mount → Container → API → UI → Export als eine Kette testen.
- Technische Integrität (`integrity_check`) reicht nicht; fachliche Plausibilität ist Pflicht.
- Optionale Schemawarnungen operatorseitig dokumentieren, aber nicht als Benutzerfehler anzeigen.
- Temporäre Auth-Bypasses nur explizit, zeitlich begrenzt, auditierbar und nach dem Test wieder aktivieren.
- Pawel bleibt unabhängiger Reviewer und verändert keinen Anwendungscode; Bruno implementiert eng begrenzte Korrekturen.

## Ergebnis

Die autoritative Datenbank ist read-only einzubinden. Synthetische Fixtures dürfen nur in isolierten Tests/Preflights vorkommen und niemals als produktive Mountquelle oder Live-Snapshot dienen.

Verknüpfte Themen: [[dashboard-production-environment]] [[Hermes-Operations]] [[deployment-reliability]] [[kanban-coordination]]

## Navigation

- [[INDEX]] — authoritative 2nd-Brain index
- [[03_Tags/Tags]] — central tag and MOC navigation
