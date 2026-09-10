# Hermes Mirror Policy

## Authorities

1. Google Drive `2nd_Brain` is the authoritative working knowledge base.
2. The local Hermes mirror is a selective read-only cache for agent context and local search.
3. `/opt/data/skills/` remains the operational source for executable skills.
4. Git is used for snapshots, audit, and rollback — not as a second live master.

## Included

- `00_SYSTEM` governance and navigation files;
- Hermes agent and skill summaries;
- Hermes operational procedures;
- `03_Tags/Hermes-Operations.md` and related indexes;
- curated `XX_Wiki/Agents`, `XX_Wiki/Skills`, and Hermes operations notes;
- `AGENTS.md` only where it describes Hermes/Lanvision operating rules.

## Excluded

- Gmail messages and attachments;
- private Calendar content;
- `.env`, OAuth tokens, client secrets, API keys, bot tokens, private keys;
- sessions, logs, caches, `node_modules`, LSP data, `.git`, `.obsidian` state;
- unrelated personal archives and private business material;
- `logseq`, `pages`, and `journals`.

## Write rule

Agents never write to the authoritative Drive vault or local mirror directly. They send a proposal/request to Erna. Erna is the only publisher.
