---
title: GPT-6 Sol, Luna, and 6.1 Sol
created: 2026-09-23
updated: 2026-09-30
type: entity
tags: [llm, model, reasoning, coding, agent, inference, evaluation]
sources: [raw/articles/openai-gpt-6-sol-luna-2026-09-22.md, raw/articles/openai-gpt-6-1-sol-2026-09-29.md]
confidence: medium
contested: false
contradictions: []
---

# GPT-6 Sol, Luna, and 6.1 Sol

## Overview

OpenAI released GPT-6 Sol and GPT-6 Luna on 22 September 2026 as lower-cost members of the GPT-6 family. The documented API prices are US$2/M input and US$10/M output for Sol, and US$0.10/M input and US$0.50/M output for Luna—each a stated 50% reduction from its GPT-5.6 predecessor. They are available as `gpt-6-sol` and `gpt-6-luna` in the API and on supported Codex/ChatGPT routes. ^[raw/articles/openai-gpt-6-sol-luna-2026-09-22.md]

On 29 September, OpenAI added `gpt-6.1-sol`: US$2/M input, US$0.10/M cached input and US$10/M output, 1M context, API access, and availability in ChatGPT Work/Codex (not Chat). The cache price is half that of GPT-6 Sol, so its value proposition is especially sensitive to real cache-hit behavior. OpenAI’s capability, safety and cost claims are vendor evidence, not a routing conclusion. ^[raw/articles/openai-gpt-6-1-sol-2026-09-29.md]

## Routing implications

- Treat the original release primarily as a cost/routing change, not proof of a uniform capability increase over [[entities/models/gpt-5-6]]. In early independent measurements reported by Artificial Analysis, Sol modestly improved its Coding Agent Index while Luna modestly declined; other results were mixed. ^[raw/articles/openai-gpt-6-sol-luna-2026-09-22.md]
- GPT-6.1 Sol is a materially different trial candidate: Artificial Analysis reports an Intelligence Index of 52 at `max` versus 48 for the highest GPT-6 Sol variant, with measured cost per Index task ranging from US$0.13 at `low` to US$0.72 at `max`. Those aggregate measurements do not prove coding-task acceptance or cache behavior in a specific harness. ^[raw/articles/openai-gpt-6-1-sol-2026-09-29.md]
- Codex CLI 0.156.1 exposes the original Sol/Luna models in the picker and recommends Luna when switching after a rate limit. That is availability guidance, not an automatically valid task-allocation policy. ^[raw/articles/openai-gpt-6-sol-luna-2026-09-22.md]
- [[entities/models/gpt-6-astra]] remains OpenAI's higher-capability route. Sol-family variants should be compared against Astra and a fixed baseline only under the same harness, context policy, effort, tools and acceptance tests.

## Controlled-trial guidance

Use Luna first for bounded high-volume work where failure is cheap and deterministic verification exists. Test GPT-6.1 Sol against the existing Sol route and [[entities/models/claude-sonnet-5-5]] on retained implementation, review and tool-loop tasks; fix effort, provider, tools, context/cache policy and budget. Measure accepted-task rate, retries, context growth, cache-hit rate, latency, tool/schema errors and total cost—not token price alone. Preserve explicit model receipts, least-privilege tools and external gates as in [[comparisons/model-routing-hermes-opencode-pi]] and [[coding/architecture/merge-gated-dag-coding-workflow]].

## Sources

- [OpenAI: GPT-6 Sol and Luna announcement](https://openai.com/index/introducing-gpt-6-sol-and-luna/)
- [OpenAI: GPT-6.1 Sol announcement, API pricing and stated evaluations](https://openai.com/index/introducing-gpt-6-1-sol/)
- [Artificial Analysis: independent model, cost and speed measurements](https://artificialanalysis.ai/models/releases/gpt-6-1-sol)
- [Codex CLI 0.156.1 release](https://github.com/openai/codex/releases/tag/rust-v0.156.1)
- [Prior independent analysis of GPT-6 Sol/Luna trade-offs](https://the-decoder.com/openais-gpt-6-sol-and-luna-cut-prices-in-half-but-barely-move-the-needle-on-performance/)
- [Hacker News discussion of GPT-6.1 Sol](https://news.ycombinator.com/item?id=49896586)
