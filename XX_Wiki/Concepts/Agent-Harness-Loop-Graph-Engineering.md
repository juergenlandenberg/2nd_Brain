---
title: "Agent Harness, Loop and Graph Engineering"
type: concept
status: draft
main_topic: "JvL AI"
creator: "Erna"
maintainer: "Erna"
content_reviewer: "Jürgen"
source_path: "Google Drive / Obsidian / JvL_AI / Hermes - Agent Harness, Loop & Graph Engineering.md"
colorcode: "Unassigned"
tags:
  - Colorcode/Unassigned
sources:
  - "https://www.youtube.com/watch?v=4NqKZerJpk8"
---

# Agent Harness, Loop and Graph Engineering

- [[JvL-AI]]
- [[hermes-agent]]
- [[wikilinks]]

## Preserved diagrams

![[40_ATTACHMENTS/JvL_AI/Pasted image 20260822095931.png]]
![[40_ATTACHMENTS/JvL_AI/Pasted image 20260822100113.png]]
![[40_ATTACHMENTS/JvL_AI/Pasted image 20260822095511.png]]

## Source model

The source describes four engineering layers around an AI model:

1. **Prompt Engineering** — instructions and task framing.
2. **Context Engineering** — supplying domain knowledge and governing context.
3. **Skill Engineering** — repeatable procedures and workflows.
4. **Tool Engineering** — external systems, connectors and MCP/tool access.

The diagrams place these four layers around the model inside an **Agent Harness**. A Loop adds repeated execution, with the source naming `/goal`, `/loop`, `/hooks` and multi-model operation.

## Graph pattern

The source graph shows three cooperating loops:

- product research and further development;
- building from ticket information;
- review loop.

This is conceptually compatible with the 2ndB pipeline, but not an authorization to enable autonomous writes. Current 2ndB governance remains authoritative: Erna is the writer, RAW remains read-only, and review gates remain mandatory.

## Review status

`draft` — architecture concept imported; operational adoption requires explicit governance and testing.
