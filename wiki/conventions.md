# 2nd Brain — Conventions

## Architecture

Three layers:

1. **raw/** — Immutable source documents (articles, papers, notes, PDFs). Erna reads but never modifies.
2. **wiki/** — LLM-generated and maintained knowledge base. Erna owns this layer entirely.
3. **This file** — Schema and conventions governing how the wiki works.

## Directory Structure

```
2nd_Brain/
├── raw/                    # Source documents (immutable)
│   ├── assets/             # Images and attachments
│   └── *.md / *.pdf        # Source files
└── wiki/                   # LLM-generated knowledge base
    ├── index.md            # Content catalog
    ├── log.md              # Chronological operations log
    ├── overview.md         # High-level synthesis
    ├── conventions.md      # This file
    ├── sources/            # Source summary pages
    ├── entities/           # Entity pages (people, orgs, tools)
    ├── concepts/           # Concept pages (theories, methods, patterns)
    └── analyses/           # Analysis pages (comparisons, syntheses)
```

## Page Format

Every wiki page uses this frontmatter:

```yaml
---
title: "Page Title"
type: source | entity | concept | analysis
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [tag1, tag2]
sources: [source-filename.md]  # for entity/concept pages
---
```

## Workflows

### Ingest
1. Source lands in `raw/`
2. Erna reads the source
3. Creates a summary page in `wiki/sources/`
4. Updates/creates relevant entity and concept pages
5. Updates `index.md`
6. Appends entry to `log.md`

### Query
1. Erna reads `index.md` to find relevant pages
2. Reads the pages, synthesizes an answer
3. Good answers get filed as new analysis pages

### Lint
Periodic health check:
- Contradictions between pages
- Stale claims superseded by newer sources
- Orphan pages with no inbound links
- Missing cross-references
- Concepts mentioned but lacking their own page

## Naming Conventions

- **Sources:** `source-slug.md` (kebab-case, derived from title)
- **Entities:** `entity-name.md` (the entity's name in kebab-case)
- **Concepts:** `concept-name.md` (the concept in kebab-case)
- **Analyses:** `analysis-topic.md` (descriptive kebab-case)

## Cross-References

Use `[[wikilinks]]` for all internal links. Every page should link to related pages.

## Language

Sources may be in any language. Wiki pages are written in the language of the source, or German/English as Jürgen prefers.
