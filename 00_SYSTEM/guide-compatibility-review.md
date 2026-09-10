# Compatibility Review — Hermes Second-Brain Guide

## Decision

The supplied Hermes Operations & Maintenance Guide is accepted as a **conceptual operating reference**, not as a replacement for the authoritative 2ndB folder structure or current governance.

## Adopted rules

- RAW intake remains separate from curated WIKI output.
- RAW/source material is read-only for Hermes and must retain provenance.
- Curated notes use descriptive filenames; `README.md` is not a published content-note name.
- Every curated note links to its main topic or cluster.
- Meaningful cross-links between related notes are encouraged.
- Curated notes carry source paths, dates, status, and relationship metadata where applicable.
- Conflicting claims are recorded explicitly rather than silently overwritten.
- Indexes/MOCs are maintained as navigation and backlink hubs.
- Vault-first retrieval is used before external research.
- Import, linting, deduplication, and archiving are controlled maintenance operations, not blind automation.

## Mapped to current 2ndB structure

| Guide concept | Authoritative 2ndB location |
|---|---|
| RAW intake | `10_RAW/` plus source-specific subfolders |
| Curated WIKI | `XX_Wiki/` |
| Tag/taxonomy hubs | `03_Tags/` as structured backlink/MOC hubs, not classic tags |
| Indexes and MOCs | `50_INDEXES/` and `03_Tags/` |
| Templates | `60_TEMPLATES/` |
| Sources and excerpts | `30_SOURCES/` |
| Attachments | `40_ATTACHMENTS/` |
| Archives | `90_ARCHIVE/` |
| Operations/system rules | `00_SYSTEM/` |

The guide's `01_Rough Notes` through `08_Quotes` and `xx_Main` are therefore treated as a **source-vault mapping model**, not as a second physical hierarchy.

## Not adopted as written

### Classical tags

The guide's `#domain/subdomain` taxonomy conflicts with the established 2ndB decision. `03_Tags` organizes backlinks through topic and cluster pages; it is not a tag registry with tag proliferation.

### Automatic broken-link stubs

Broken links are reported and routed for review. Hermes must not create placeholder knowledge notes automatically. This prevents fabricated nodes and preserves the content-review gate.

### Automatic semantic merging at 85%

Similarity may identify duplicate candidates, but it does not authorize an automatic merge. Erna prepares a proposal, preserves provenance and conflicts, and publishes only after validation.

### Two bidirectional links as a hard universal minimum

The quality target is: one main-topic link plus meaningful related links where applicable. Tiny source, index, or boundary notes may not have two honest neighbours. Artificial links are worse than sparse links.

### Co-owned indexes

Operationally, Erna remains the sole writer of the authoritative 2ndB. Agents may propose index changes; Erna publishes them.

### Unverified cron and command suite

The supplied `hermes run --task ...` and `qmd index ...` commands are not installed/validated as the current production workflow. They remain proposals until each command, path, schedule, and output contract is tested. Existing Hermes cronjobs are not replaced by this guide.

### Graph-RAG/HyDE as a current dependency

QMD, embeddings, Graphify output, and vector search are optional future layers. The current baseline remains INDEX/MOC routing, targeted Markdown retrieval, and provenance-first reading.

## Roles

- Hermes notes: Erna is creator, maintainer, publisher, and link-integrity owner.
- Imported personal vaults: Erna performs structural import and link mapping; Jürgen is final content reviewer; topic-specific creator/maintainer roles are assigned per main topic.

## Import gate

The main-topic list must be defined before final curation of personal vault imports. Each imported cluster needs a main topic, role assignment, source/legacy path, exclusions, and expected backlink neighbourhood.
