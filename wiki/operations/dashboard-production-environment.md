# Lanvision Dashboard – Produktions-Deployment-Environment

**Stand:** 2026-09-07 13:10 UTC  
**Status:** produktiv verifiziert

Navigation: [[Hermes-Operations]] · [[Finn-Agent-Profile]] · [[finn-staging-environment-vps-windows]]

## Zielzugang

- Domain: `https://dashboard.lanvision.cloud`
- Finn-Bereich: `/investmentanalysen`
- mTLS: aktiv; Clientzertifikat erforderlich
- Interne Dienste sind nicht öffentlich exponiert
- Öffentliche Zusatzports `3100` und `5173`: nicht zulässig und nicht veröffentlicht

## Runtime auf dem VPS

- Host: `srv1873162`
- Produktionspfad des kontrollierten Releases: `/var/lib/sicheres-dashboard/current`
- Release-Archiv: `/var/lib/sicheres-dashboard/releases/`
- Deploy-Benutzer: `dashboard-deploy`
- SSH-Kanal: ForcedCommand, `restrict`, kein TTY, kein Agent-/X11-/Port-Forwarding
- Erlaubtes Protokoll: Compose über stdin plus immutable GHCR-Digests und kurzlebiger GHCR-Token
- Produktions-Compose verwendet ausschließlich immutable API-/Web-Images; kein `build:` im Release-Compose
- Read-only-Bind-Mount der autoritativen Buchhaltungsdatenbank bleibt aktiv

## Aktive Container

- `current-dashboard-api-1`: intern Port `3100`, Healthcheck aktiv
- `current-caddy-1`: einziger produktiver Web-Einstieg im Docker-Netzwerk
- Traefik terminiert externes TLS/mTLS und routet die Domain zum aktuellen Caddy
- Der alte konkurrierende Stack `sicheres-dashboard-v1-*` wurde entfernt, weil er dieselbe Host-Regel beanspruchte und veraltete HTML-/Asset-Inhalte ausliefern konnte
- Staging-Container bleiben vom produktiven Router getrennt und sind kein Benutzerzugang

## Reverse-Proxy-Routing

Caddy routet:

- `/api/*` → `dashboard-api:3100`
- `/auth/*` → `dashboard-api:3100`
- `/health` und `/health/*` → `dashboard-api:3100`
- `/assets/*` ausschließlich als statische Dateien
- `/favicon*` ausschließlich als statische Dateien
- übrige SPA-Routen → `/index.html`

Wichtig: Asset-Pfade dürfen niemals auf den SPA-HTML-Fallback fallen. Fehlende JavaScript-/CSS-Dateien müssen `404` liefern, nicht `index.html`.

## CI/CD-Kette

```text
Git push / workflow_dispatch
  → GitHub Actions
  → Tests, Lint, Typecheck, Build
  → immutable API-/Web-Images in GHCR
  → Provenance/SBOM
  → ForcedCommand-SSH zum VPS
  → kurzlebiger GHCR-Login nur während des Pulls
  → atomarer Release-Symlink
  → Compose-Healthcheck
  → externer mTLS-/Asset-/Port-Test aus GitHub Actions
  → Erfolg oder Rollback
```

Der GHCR-Token wird nur über den geschützten stdin-Kanal übertragen, nicht dauerhaft auf dem VPS gespeichert. Nach dem Image-Pull erfolgt Docker-Logout.

## GitHub-Secrets und Environment

Repository-Secrets, ohne Werte zu dokumentieren:

- `DEPLOY_HOST`
- `DEPLOY_KNOWN_HOSTS`
- `DEPLOY_SSH_KEY`

Environment `production`, ohne Werte zu dokumentieren:

- `BASE_URL`
- `MTLS_CLIENT_PFX_B64`
- `MTLS_CLIENT_PFX_PASSWORD`

Keine privaten Schlüssel, Passwörter, Tokens, PFX-Dateien oder Secret-Werte in dieses Wiki übernehmen.

## mTLS-Trust

- Bestehende Client-CA bleibt aktiv.
- Zusätzliche CI-CA: `Lanvision Dashboard CI CA 2026`
- Die öffentliche CI-CA ist im Traefik-Trust-Bundle `/docker/traefik/dynamic/dashboard-client-ca.crt` ergänzt.
- Der CA-Private-Key bleibt ausschließlich lokal beim Aussteller.
- Das CI-Clientzertifikat wird nur als geschütztes GitHub-Environment-Secret verwendet.
- Das persönliche `Juergen-Desktop`-Zertifikat wird nicht exportiert und nicht für CI verwendet.

## Verifikation

Letzter erfolgreicher Deployment-Lauf:

- GitHub Actions Run: `34125699292`
- Verifizierter Build-/Deploy-Stand: Commit `4b3a6ccac39867019283146c5f9684c9b6ca5317`
- Build: PASS
- API-/Caddy-Health: PASS
- mTLS mit CI-Zertifikat: PASS
- öffentlicher Frontend-Asset-Test: PASS
- Zugriff ohne Clientzertifikat: erwartungsgemäß abgewiesen
- Post-Deploy-Gate: PASS

## Sicherheitsregeln

- Keine privaten Schlüssel in Chat, Git, Kanban, Wiki oder VPS.
- Keine Auth-Bypasses.
- Keine direkten Browserzugriffe auf SQLite.
- Keine synthetischen Finanz- oder Marktdaten im produktiven Pfad.
- Produktionsfreigabe nur mit grünem CI, kontrolliertem Deploy-Kanal und externer mTLS-Verifikation.
- Bei konkurrierenden Docker-Routern für dieselbe Domain zuerst den alten Router stoppen/entfernen; nicht mit Cache-Theorien herumdoktern.

## Zugehörige Dokumente

- Projekt: `/opt/data/shared-workspace/projects/sicheres-dashboard-v1`
- Datenvertrag: `investmentanalysen-data.v1`
- Environment-Matrix: `/opt/data/shared-workspace/projects/sicheres-dashboard-v1/docs/environment-matrix-vps-windows-finn-staging.md`
- Deployment-Kanal: `/opt/data/shared-workspace/projects/sicheres-dashboard-v1/docs/deploy-channel.md`
- Finn-Datenvertrag: `/opt/data/kanban/boards/projekte/attachments/t_d3554c86/investmentanalysen-data-contract-v1.md`
