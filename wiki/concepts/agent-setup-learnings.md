---
title: Agent Setup Learnings
created: 2026-08-28
updated: 2026-08-28
type: concept
tags: [hermes-agent, telegram, setup, learnings, pitfalls]
sources: []
confidence: high
---

# Agent Setup Learnings — 28.08.2026

Was heute schiefging und wie wir es vermeiden.

## 1. Telegram-Bot-Tokens

### Problem
- Tokens waren nach Regenerate in @BotFather ungültig
- Script `set-bot-tokens.sh` hatte Quoting-Probleme (Shell vs Python)
- `write_file`-Tool zerschießt Anführungszeichen in Shell-Skripten

### Lösung
- Script nur noch mit `cat > file << 'EOF'` über Terminal erstellen, NICHT über `write_file`
- Tokens immer mit `python3 -c` oder Python-Script setzen, nicht mit Bash-String-Manipulation
- Nach Token-Wechsel: Gateway MUSS neu gestartet werden

### Checkliste
1. @BotFather → `/mybots` → Bot → API Token → Regenerate
2. `bash /opt/data/scripts/set-bot-tokens.sh` (nur betroffene Bots eingeben)
3. `hermes --profile <name> gateway restart`

## 2. Telegram Group Chat

### Problem
- Bots konnten in Gruppe posten, aber keine Nachrichten empfangen
- Privacy Mode war an (Standard bei neuen Bots)
- Telegram cached Privacy-Status beim Beitritt — Änderung wirkt erst nach Remove+Re-add

### Lösung
1. @BotFather → `/mybots` → Bot → **Bot Settings** → **Group Privacy** → **Disable**
2. **WICHTIG:** Bot aus Gruppe entfernen und NEU HINZUFÜGEN (Telegram cached!)
3. In `.env` eintragen:
   ```
   TELEGRAM_ALLOWED_CHATS=-1003727774482
   TELEGRAM_GROUP_ALLOWED_CHATS=-1003727774482
   ```
4. In `config.yaml` eintragen:
   ```yaml
   platforms:
     telegram:
       allowed_chats:
         - "-1003727774482"
       group_allowed_chats:
         - "-1003727774482"
   ```
5. Gateway neu starten

### Reihenfolge (KRITISCH!)
1. Token setzen
2. Privacy Mode deaktivieren
3. Bot aus Gruppe entfernen
4. Bot neu hinzufügen
5. Config eintragen (.env + config.yaml)
6. Gateway neu starten
7. Testen

## 3. Model Configuration

### Problem
- Anthropic-Konto leer → alle Gateways auf Fallback geschaltet
- Gateways liefen mit alter Config (anthropic statt openai-codex)
- Config-Änderung greift erst nach Gateway-Neustart

### Lösung
- Immer `openai-codex/gpt-4.1-mini` als Standard
- `anthropic/claude-sonnet-5` als Heavy
- `anthropic/claude-opus-5` als Maximum
- Nach JEDEM Config-Wechsel: ALLE Gateways neu starten

## 4. Gateway Management

### Problem
- Alte Gateways liefen weiter mit alter Config
- `hermes gateway restart` funktioniert nicht aus dem Gateway selbst
- Mehrere Gateway-Instanzen kollidieren

### Lösung
- Immer erst `process(action='list')` prüfen
- Dann `process(action='kill')` für alte Instanzen
- Dann `terminal(background=true)` für neue Instanzen
- NIEMALS `hermes gateway restart` aus dem Gateway heraus

## 5. Config-Dateien

### Problem
- `.env` und `config.yaml` hatten unterschiedliche Settings
- Einige Bots hatten Gruppen-Config nur in `.env`, andere nur in `config.yaml`

### Lösung
- IMMER beide Dateien prüfen und aktualisieren
- `.env` für Secrets (Tokens, API Keys)
- `config.yaml` für Settings (allowed_chats, model, provider)
- Nach Änderungen: `grep` um sicherzustellen, dass alle Bots gleich konfiguriert sind

## 6. Backup-Repo

### Problem
- Curator-Backups (skills.tar.gz) waren zu groß für GitHub (>2GB)
- Git-History enthielt große Dateien

### Lösung
- `.curator_backups` in `.gitignore` aufnehmen
- `git filter-repo` um große Dateien aus der History zu entfernen
- Regelmäßig `du -sh` prüfen

## 7. Porträt-Generierung

### Learnings
- "Menschlich" vs "Roboter" — klarer definieren was gewünscht ist
- Style-Referenz IMMER zuerst zeigen lassen
- "Röter" war zu vage — besser: "auburn/reddish metallic hair"
- Name-Schilder müssen explizit im Prompt erwähnt werden

## 8. Friday Feedback

### Setup
- Erna: 09:00 UTC
- Ben: 13:00 UTC
- Desiree: 14:00 UTC
- Bruno: 15:00 UTC
- Pawel: 16:00 UTC
- Neue Agenten: nächster Slot nach 16:00 UTC

## 9. 2nd Brain als Shared Context

### Struktur
```
2nd_Brain/wiki/
├── agents/        ← Spezialgebiete jedes Agenten
├── concepts/      ← Shared Knowledge
└── index.md       ← Katalog
```

### Regel
- Bei NEUEN Agenten: IMMER `wiki/agents/<name>/README.md` erstellen
- In `AGENTS.md` dokumentieren

## 10. AGENTS.md

### Muss immer aktuell sein
- Alle Agenten und ihre Rollen
- Telegram-Gruppe mit Chat-ID
- Friday Feedback Zeiten
- Model-Konfiguration
- Obsidian-Vaults
- Shared Knowledge (2nd Brain)

---

## Checkliste für neuen Agenten

1. **Profil erstellen:** `hermes --profile <name> config set ...`
2. **Token setzen:** `bash /opt/data/scripts/set-bot-tokens.sh`
3. **Privacy Mode:** @BotFather → Group Privacy → Disable
4. **Gruppe:** Bot entfernen + neu hinzufügen
5. **Config:** `.env` + `config.yaml` mit allowed_chats
6. **2nd Brain:** `wiki/agents/<name>/README.md` erstellen
7. **Friday Feedback:** Cron-Job erstellen (nächster Slot nach 16:00 UTC)
8. **AGENTS.md:** Neuen Agenten eintragen
9. **Gateway starten:** `hermes --profile <name> gateway run`
10. **Testen:** Nachricht in Gruppe senden, Antwort prüfen

---

*Erstellt nach einem sehr mühsamen Tag. Bitte befolgen!*
