---
title: Shared Task Board
created: 2026-08-28
updated: 2026-08-28
type: concept
tags: [project-management, kanban, multi-agent, workflow]
sources: []
confidence: high
---

# Shared Task Board

Asynchrones Projekt-Management-System für das Lanvision-Agenten-Team.

## Standort

```
/opt/data/shared/
├── board/              # Projekt-JSON-Dateien
│   ├── schema.json     # Schema-Definition
│   ├── index.json      # Index aller Projekte
│   └── PROJ-001.json   # Einzelne Projekte
├── inbox/              # Posteingang pro Agent
│   ├── bruno/
│   ├── ben/
│   ├── desiree/
│   ├── pawel/
│   └── erna/
├── handoff/            # Deliverables zwischen Agents
├── scripts/
│   └── board-cli.sh    # CLI-Tool
└── docs/
    └── README.md       # Doku
```

## CLI-Befehle

```bash
bash /opt/data/shared/scripts/board-cli.sh <command>
```

| Command | Description |
|---------|-------------|
| `create <title> <desc>` | Neues Projekt erstellen (Erna) |
| `list` | Alle Projekte auflisten |
| `show <PROJ-ID>` | Projekt-Details anzeigen |
| `assign <PROJ-ID> <task-id> <agent>` | Task zuweisen |
| `status <PROJ-ID> <task-id> <new-status>` | Task-Status ändern |
| `notify <PROJ-ID> <agent> <message>` | Inbox-Nachricht senden |
| `handoff <PROJ-ID> <task-id>` | Deliverable markieren |
| `check-inbox <agent>` | Inbox eines Agenten prüfen |
| `clear-inbox <agent>` | Inbox leeren nach Bearbeitung |

## Workflow

1. **Jürgen → Erna:** "Projekt X, Bruno baut, Ben liefert Daten"
2. **Erna:** erstellt Projekt, weist Tasks zu
3. **Ben:** liefert Daten → handoff/
4. **Bruno:** kriegt automatisch Bescheid → baut Backend
5. **Desiree:** arbeitet parallel am Design
6. **Pawel:** kriegt Bescheid wenn alles ready → Security Review
7. **Erna:** kriegt Abschluss-Meldung

## Cronjobs

Alle 30 Min prüfen alle Agenten ihre Inbox:
- Bruno: 85eabd5fb326
- Ben: 4baf45266979
- Desiree: 92c5bca6e0a3
- Pawel: 5d6bcb2fdfe1
- Erna: 61fca69c999a

## Task-Status

- `pending` — wartet auf Abhängigkeit
- `in_progress` — wird bearbeitet
- `done` — abgeschlossen
- `blocked` — nicht startbar

## Beispiel

PROJ-001 "Lanvision Dashboard":
1. Ben → Finanzdaten bereitstellen (done)
2. Bruno → Dashboard-Backend (pending, blocked by 1)
3. Desiree → UI Design (in_progress)
4. Pawel → Security Review (pending, blocked by 2+3)

## Links

- [[ai-model-overview]]
- [[hermes-agent]]
- [[agent-setup-learnings]]
