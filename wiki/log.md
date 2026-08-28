# Wiki Log

> Chronological record of all wiki actions. Append-only.
> Format: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete
> When this file exceeds 500 entries, rotate: rename to log-YYYY.md, start fresh.

## [2026-08-27] create | Wiki initialized
- Domain: General research (AI/ML, tech, business, personal development)
- Structure created with SCHEMA.md, index.md, log.md, overview.md
- Path: /opt/data/2nd_Brain/

## [2026-08-27] create | Git Commands entry
- Created: wiki/concepts/git-commands.md
- Created support pages: wiki/concepts/github.md, wiki/concepts/obsidian.md, wiki/concepts/2nd-brain.md
- Updated: wiki/index.md, wiki/SCHEMA.md
- Key takeaways: Windows-friendly Git commands for cloning, fetching, resetting, SSH-to-HTTPS remote switching, and common errors.

## [2026-08-28] create | Set Bot Tokens entry
- Created: wiki/concepts/set-bot-tokens.md
- Updated: wiki/index.md
- Key takeaways: Secure script for setting Telegram bot tokens via @BotFather renewal. Script at /opt/data/scripts/set-bot-tokens.sh.

## [2026-08-28] create | AI Model Overview entry
- Created: wiki/concepts/ai-model-overview.md
- Updated: wiki/index.md
- Key takeaways: Comprehensive model comparison for Lanvision team. Standard=GPT-4.1 Mini, Heavy=Sonnet 5, Max=Opus 5. Coding: DeepSeek V4 Flash. Images: FLUX 2 Klein (free via Nous).

## [2026-08-28] create | Agent knowledge base
- Created: wiki/agents/erna/README.md, wiki/agents/ben/README.md, wiki/agents/desiree/README.md, wiki/agents/bruno/README.md, wiki/agents/pawel/README.md
- Updated: wiki/index.md, AGENTS.md
- Key takeaways: 2nd Brain wiki is now shared context for all agents. Each agent has specialty area in wiki/agents/. New agents get README.md at creation time.

## [2026-08-28] create | Shared Task Board + Learnings
- Created: wiki/concepts/shared-task-board.md, wiki/concepts/agent-setup-learnings.md
- Updated: wiki/index.md, AGENTS.md
- Key takeaways: Bruno built async project management system at /opt/data/shared/. Board CLI for all operations. Cronjobs every 30 min for inbox checking. Learnings documented for future agent setup.
