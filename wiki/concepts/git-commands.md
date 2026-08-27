---
title: Git Commands
created: 2026-08-27
updated: 2026-08-27
type: concept
tags: [git, developer-tools]
sources: []
confidence: high
---

# Git Commands

Kurzer Spickzettel für die Git-Befehle, die Jürgen aktuell braucht — vor allem zum Klonen, Aktualisieren und Reparieren von lokalen Repositories.

## Repository frisch klonen

### Hermes Backup

```bash
git clone https://github.com/juergenlandenberg/Hermes.git
```

### 2nd Brain

```bash
git clone https://github.com/juergenlandenberg/2nd_Brain.git
```

HTTPS ist auf Windows oft einfacher als SSH, wenn noch kein GitHub-SSH-Key eingerichtet ist.

## In ein bestehendes Repository wechseln

```bash
cd C:\Users\<DEIN_WINDOWS_USER>\Documents\Hermes
git status
```

Oder für den 2nd Brain:

```bash
cd C:\Users\<DEIN_WINDOWS_USER>\Documents\2nd_Brain
git status
```

Wenn `fatal: not a git repository` erscheint, bist du entweder im falschen Ordner oder der Ordner wurde nicht mit `git clone` erstellt.

## Lokales Repository hart auf GitHub-Stand setzen

Nur ausführen, wenn lokale Änderungen egal sind:

```bash
git fetch origin
git reset --hard origin/main
git clean -fd
```

Bedeutung:

- `git fetch origin` — lädt den aktuellen Stand von GitHub
- `git reset --hard origin/main` — setzt lokale Dateien exakt auf GitHub-Stand
- `git clean -fd` — löscht unversionierte Dateien/Ordner

Das ist der digitale Kärcher. Nützlich, aber nicht liebevoll.

## Remote von SSH auf HTTPS umstellen

Wenn diese Fehlermeldung kommt:

```text
could not read publickey
```

Dann nutzt Git SSH, aber Windows hat keinen passenden GitHub-Key. Auf HTTPS umstellen:

```bash
git remote set-url origin https://github.com/juergenlandenberg/Hermes.git
```

Für 2nd Brain:

```bash
git remote set-url origin https://github.com/juergenlandenberg/2nd_Brain.git
```

Danach:

```bash
git fetch origin
git reset --hard origin/main
git clean -fd
```

## Prüfen, welches Remote gesetzt ist

```bash
git remote -v
```

Beispiele:

```text
origin  https://github.com/juergenlandenberg/Hermes.git (fetch)
origin  https://github.com/juergenlandenberg/Hermes.git (push)
```

oder SSH:

```text
origin  git@github.com:juergenlandenberg/Hermes.git (fetch)
origin  git@github.com:juergenlandenberg/Hermes.git (push)
```

## GitHub Login bei HTTPS

Wenn GitHub nach Login fragt:

- Username: `juergenlandenberg`
- Password: **nicht** GitHub-Passwort, sondern Personal Access Token

GitHub erlaubt keine normalen Passwörter mehr für Git-Zugriff.

## Verwandte Seiten

- [[github]]
- [[obsidian]]
- [[2nd-brain]]
