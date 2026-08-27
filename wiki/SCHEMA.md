# Wiki Schema

## Domain

General research knowledge base — AI/ML, technology, business strategy, personal development, and any topic Jürgen researches deeply.

## Conventions

- File names: lowercase, hyphens, no spaces (e.g., `transformer-architecture.md`)
- Every wiki page starts with YAML frontmatter (see below)
- Use `[[wikilinks]]` to link between pages (minimum 2 outbound links per page)
- When updating a page, always bump the `updated` date
- Every new page must be added to `index.md` under the correct section
- Every action must be appended to `log.md`

## Frontmatter

```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | query | summary
tags: [from taxonomy below]
sources: [raw/articles/source-name.md]
confidence: high | medium | low
---
```

## Tag Taxonomy

- AI/ML: model, architecture, benchmark, training, inference, fine-tuning, alignment
- People/Orgs: person, company, lab, open-source, researcher
- Technology: semiconductor, quantum, robotics, cloud, infrastructure, developer-tools, git
- Business: strategy, investment, market, regulation, compliance
- Finance: trading, pinescript, technical-analysis, fundamental-analysis
- Security: cybersecurity, vulnerability, encryption, privacy
- Meta: comparison, timeline, controversy, prediction, trend

Rule: every tag on a page must appear in this taxonomy. If a new tag is needed, add it here first.

## Page Thresholds

- **Create a page** when an entity/concept appears in 2+ sources OR is central to one source
- **Add to existing page** when a source mentions something already covered
- **DON'T create a page** for passing mentions or minor details
- **Split a page** when it exceeds ~200 lines

## Update Policy

When new information conflicts with existing content:
1. Check the dates — newer sources generally supersede older ones
2. If genuinely contradictory, note both positions with dates and sources
3. Mark the contradiction in frontmatter: `contradictions: [page-name]`
4. Flag for user review in the lint report

## Language

German or English depending on source language. Wiki pages default to German unless the topic is better served in English.
