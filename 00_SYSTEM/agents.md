# Lanvision 2nd Brain — Agent Rules

## Purpose
This vault is the authoritative working knowledge base for Lanvision.

## Source layers
- `10_RAW/` contains original source material. Never rewrite or silently delete RAW.
- `XX_Wiki/` contains curated, linked knowledge derived from sources.
- `30_SOURCES/` contains provenance, bibliographic records and source indexes.
- `40_ATTACHMENTS/` contains binary source files and media.

## Required behavior
1. Read `00_SYSTEM/context-rules.md` before answering knowledge questions.
2. Use `00_SYSTEM/router.md` to select the smallest relevant scope.
3. Prefer `INDEX.md` and curated WIKI pages before broad searching.
4. Cite source paths and dates for material claims.
5. Never present an unsupported inference as a fact.
6. Do not overwrite competing claims; record the conflict and its sources.
7. Treat RAW as immutable evidence.
8. One active writer per file; check the Drive revision before updating.
9. Every curated note must use an informative filename; `README.md` is not an accepted content-note name.
10. Every curated note must link to its main topic or cluster; cross-links between related notes are encouraged.
11. Erna is creator and maintainer of all Hermes notes. For imported personal vaults, Jürgen is the final content reviewer; topic roles are assigned before publication.
12. Keep secrets, tokens, passwords and private keys out of this vault.
13. Do not copy `.git/`, `.obsidian/workspace*.json`, caches or runtime state.

## Ingest workflow
New material enters `10_RAW/` first. Resi may prepare a proposal. A curated WIKI update must preserve source links and be logged in `CHANGELOG.md`.

## Answer workflow
Source-first, targeted retrieval, explicit uncertainty, then answer. If the vault has no reliable evidence, say so and use external research only when requested.
