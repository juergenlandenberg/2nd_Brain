---
title: Set Bot Tokens
created: 2026-08-28
updated: 2026-08-28
type: concept
tags: [telegram, developer-tools, hermes-agent]
sources: []
confidence: high
---

# Set Bot Tokens

Telegram-Bot-Tokens für die Hermes-Agenten (Ben, Desiree, Bruno, Pawel) sicher setzen.

## Script

Pfad: `/opt/data/scripts/set-bot-tokens.sh`

```bash
bash /opt/data/scripts/set-bot-tokens.sh
```

Reihenfolge: **ben** → **desiree** → **bruno** → **pawel**

Nach jedem Token blind einfügen + Enter. Tokens werden nicht angezeigt (`read -s`).

## Was das Script macht

1. Fragt nacheinander nach 4 Bot-Tokens
2. Schreibt jeden Token in die `.env` des jeweiligen Profils (`/opt/data/profiles/<name>/.env`)
3. Ersetzt bestehende `TELEGRAM_BOT_TOKEN=` Zeile oder fügt neue hinzu

## Wann nötig

- Tokens von @BotFather erneuert (Regenerate)
- Neue Bots erstellt
- Fehlermeldung: `Provider authentication failed` oder `token rejected by server`

## Danach

Gateways neu starten:

```bash
for p in ben desiree pawel; do
  hermes --profile "$p" gateway restart
done
```

Bruno: Telegram erst aktivieren wenn Token gültig:

```bash
hermes --profile bruno config set platforms.telegram.enabled true
hermes --profile bruno gateway restart
```

## Links

- [[hermes-agent]]
- [[telegram-setup]]
