---
title: AI Model Overview
created: 2026-08-28
updated: 2026-08-28
type: concept
tags: [ai, models, pricing, openai, anthropic, deepseek, image-generation]
sources: []
confidence: high
---

# AI Model Overview

Übersicht über aktuelle KI-Modelle (Stand August 2026), Preise, Spezialisierungen und Empfehlungen für das Lanvision-Agenten-Team.

## Text-Modelle — Proprietär

### OpenAI

| Modell | Input/1M | Output/1M | Context | Spezialisierung |
|---|---|---|---|---|
| GPT-5.6 Sol | — | — | — | Frontier, SWE-bench 96.2% |
| GPT-5.6 Luna | — | — | — | Frontier, SWE-bench 93% |
| GPT-5.5 | $5 | $30 | — | Allround |
| GPT-5.2 | $1.75 | $14 | 400K | Stark, aber teuer für Alltag |
| GPT-4.1 | $2 | $8 | — | Solide Allround |
| **GPT-4.1 Mini** | **$0.40** | **$1.60** | 1M | ✅ **Standard für Lanvision** |

### Anthropic (Claude)

| Modell | Input/1M | Output/1M | Context | Spezialisierung |
|---|---|---|---|---|
| Fable 5 | $10 | $50 | 1M | Frontier Intelligence, lange Agenten |
| Opus 5 | $5 | $25 | 1M | Komplexes Coding, Enterprise |
| **Sonnet 5** | **$2** | **$10** | 1M | ✅ **Heavy-Modell für Lanvision** |
| Haiku 4.5 | $1 | $5 | 200K | Schnell, günstig |
| Opus 4.6 | $5 | $25 | 1M | Legacy, SWE-bench 80.8% |

### Google (Gemini)

| Modell | Input/1M | Output/1M | Context | Spezialisierung |
|---|---|---|---|---|
| Gemini 3.1 Pro | $2 | $12 | — | Wissenschaft, Multimodal, GPQA 94.3% |
| Gemini 3.6 Flash | $1.50 | $7.50 | 1M | Schnell, günstig |

## Text-Modelle — Open Source / Selbst-Hosted

| Modell | Params | SWE-bench | LiveCodeBench | Kosten | Empfehlung |
|---|---|---|---|---|---|
| DeepSeek V4 Pro | 1.6T | 80.6% | 93.5% | API günstig | Stärkster Open-Source-Coder |
| **DeepSeek V4 Flash** | 284B | 79% | 91.6% | API günstig | ✅ **Coding-Empfehlung für Bruno** |
| Kimi K3 | 2.8T | 76.8% | — | API | Allround-Stärke |
| GLM-5.2 | 744B | 62.1%* | — | Kostenlos (lokal) | Coding, braucht GPU |
| Qwen3.6-27B | 27B | 77.2% | 83.9% | **Kostenlos (lokal)** | ✅ Lokal auf Server |
| MiMo-V2-Flash | 309B | 73.4% | 80.6% | API | Xiaomi, guter Allrounder |
| Mistral Small 4 | 119B | — | — | API | Leichtgewichtig |

*GLM auf SWE-bench Pro, nicht direkt vergleichbar

## Bildgenerierung

| Tool | Qualität | Kosten | Status |
|---|---|---|---|
| **FLUX 2 Klein 9B** | Sehr gut | **Kostenlos** (Nous Abo) | ✅ Aktiv für Lanvision |
| FLUX 2 Pro | State-of-the-art | FAL API | Über Nous Abo |
| Stable Diffusion XL | Gut | Kostenlos (lokal) | Braucht GPU |
| DALL-E 3 | Gut | OpenAI API | Teuer |

## Aktuelle Lanvision-Konfiguration

| Zweck | Modell | Provider | Kosten |
|---|---|---|---|
| **Standard** | GPT-4.1 Mini | openai-codex | $0.40/$1.60 |
| **Heavy** | Sonnet 5 | anthropic | $2/$10 |
| **Maximum** | Opus 5 | anthropic | $5/$25 |
| **Fallback 1** | xiaomi/mimo-v2.5-pro | nous | über Abo |
| **Fallback 2** | qwen3:8b | custom (lokal) | kostenlos |
| **Bilder** | FLUX 2 Klein | nous | über Abo |

## Agenten-Zuordnung (geplant)

| Agent | Standard | Heavy | Spezial |
|---|---|---|---|
| Erna | GPT-4.1 Mini | Sonnet 5 | — |
| Ben | GPT-4.1 Mini | Sonnet 5 | — |
| Desiree | GPT-4.1 Mini | Sonnet 5 | FLUX 2 (Bilder) |
| Bruno | GPT-4.1 Mini | Sonnet 5 | DeepSeek V4 Flash (Coding) |
| Pawel | GPT-4.1 Mini | Sonnet 5 | — |

## Coding-Benchmarks (SWE-bench Verified, August 2026)

| Modell | Score | Typ |
|---|---|---|
| GPT-5.6 Sol | 96.2% | Proprietär |
| Claude Fable 5 | 95% | Proprietär |
| Claude Mythos 5 | 95.5% | Proprietär |
| Claude Opus 5 | — | Proprietär |
| Claude Sonnet 5 | 85.2% | Proprietär |
| DeepSeek V4 Pro | 80.6% | Open Source |
| Claude Opus 4.6 | 80.8% | Proprietär |
| DeepSeek V4 Flash | 79% | Open Source |
| Qwen3.6-27B | 77.2% | Open Source (lokal) |
| GPT-4.1 Mini | 23.6% | Proprietär (günstig) |

## Links

- [[set-bot-tokens]]
- [[hermes-agent]]
- [[git-commands]]
