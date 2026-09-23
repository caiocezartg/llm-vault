---
title: GPT-6 Sol and Luna
created: 2026-09-23
updated: 2026-09-23
type: entity
tags: [llm, model, reasoning, coding, agent, inference, evaluation]
sources: [raw/articles/openai-gpt-6-sol-luna-2026-09-22.md]
confidence: medium
contested: false
contradictions: []
---

# GPT-6 Sol and Luna

## Overview

OpenAI released GPT-6 Sol and GPT-6 Luna on 22 September 2026 as lower-cost members of the GPT-6 family. The documented API prices are US$2/M input and US$10/M output for Sol, and US$0.10/M input and US$0.50/M output for Luna—each a stated 50% reduction from its GPT-5.6 predecessor. They are available as `gpt-6-sol` and `gpt-6-luna` in the API and on supported Codex/ChatGPT routes. ^[raw/articles/openai-gpt-6-sol-luna-2026-09-22.md]

## Routing implications

- Treat the release primarily as a cost/routing change, not proof of a uniform capability increase over [[entities/models/gpt-5-6]]. In early independent measurements reported by Artificial Analysis, Sol modestly improved its Coding Agent Index while Luna modestly declined; other results were mixed. ^[raw/articles/openai-gpt-6-sol-luna-2026-09-22.md]
- Codex CLI 0.156.1 exposes both models in the picker and recommends Luna when switching after a rate limit. That is availability guidance, not an automatically valid task-allocation policy. ^[raw/articles/openai-gpt-6-sol-luna-2026-09-22.md]
- [[entities/models/gpt-6-astra]] remains OpenAI's higher-capability route. Sol and Luna should be compared against Astra and a fixed baseline only under the same harness, context policy, effort, tools and acceptance tests.

## Controlled-trial guidance

Use Luna first for bounded high-volume work where failure is cheap and deterministic verification exists; use Sol as a candidate for implementation, review or longer tool loops where its accepted-task economics beat the existing route. Measure accepted-task rate, retries, context growth, latency, tool errors and total cost—not token price alone. Preserve explicit model receipts, least-privilege tools and external gates as in [[comparisons/model-routing-hermes-opencode-pi]] and [[coding/architecture/merge-gated-dag-coding-workflow]].

## Sources

- [OpenAI announcement and API pricing](https://openai.com/index/introducing-gpt-6-sol-and-luna/)
- [Codex CLI 0.156.1 release](https://github.com/openai/codex/releases/tag/rust-v0.156.1)
- [Independent analysis of cost/performance trade-offs](https://the-decoder.com/openais-gpt-6-sol-and-luna-cut-prices-in-half-but-barely-move-the-needle-on-performance/)
- [Hacker News discussion](https://news.ycombinator.com/item?id=49805509)
