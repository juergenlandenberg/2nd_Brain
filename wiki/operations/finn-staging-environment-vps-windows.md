# Finn-Staging Environment: VPS und Windows

Die verbindliche Environment-Matrix liegt im Projekt unter:

`/opt/data/shared-workspace/projects/sicheres-dashboard-v1/docs/environment-matrix-vps-windows-finn-staging.md`

Kernbefund: Es gibt derzeit kein verifiziertes Test-Environment. `/docker/sicheres-dashboard-v1-staging` ist nur ein Versuchspfad mit laufenden Compose-Containern. API-intern liefert `/health/live` 200, aber `docker port` ist leer und der VPS-Host verweigert `127.0.0.1:3100`; `docker inspect` zeigt nur eine statische, zur Laufzeit nicht wirksame PortBinding. Pawel priorisiert deshalb Docker-Daemon-/Portproxy-/Hostnetz-Diagnose; Ben verlangt Quelle→Mount→SQLite-Integrität→Read-only→Provenienz. Windows/SSH ist erst danach relevant. Keine Produktionsfreigabe.

Rollen: Ben prüft Quelle/Mount/Read-only/Provenienz; Pawel prüft unabhängig Netzwerk- und Sicherheitsgrenzen; Bruno implementiert; Erna koordiniert; Jürgen gibt fachlich und produktiv frei.

Verbindliche Regel: Jeder Prompt an Jürgen zu VPS, Windows, Docker, SSH, Ports, Tunneln oder Deployment wird vor Ausgabe gegen diese Environment-Doku, den tatsächlichen Runtime-Status, effektive Compose-Konfiguration, Sicherheitswirkung und erwartete Ausgaben geprüft. Bei Widerspruch zuerst Doku/Drift klären; keine spekulativen Befehle weitergeben.