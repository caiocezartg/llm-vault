---
title: GPT-6 Astra
created: 2026-09-05
updated: 2026-09-05
type: entity
tags: [llm, model, evaluation, coding, agent, inference]
sources: [raw/articles/gpt-6-astra-2026-09-05.md]
confidence: medium
contested: true
contradictions: []
---

# GPT-6 Astra

## Overview

OpenAI released GPT-6 Astra on 2026-09-03 as a frontier model for long-horizon computer use, coding and other professional tool-using work. It is rolling out through the OpenAI API, Azure, AWS Bedrock and selected ChatGPT plans; GitHub added gradual Copilot availability on 2026-09-04. The standard API list price is US$10/M input and US$50/M output tokens. ^[raw/articles/gpt-6-astra-2026-09-05.md]

## Evaluation boundary

OpenAI reports large gains on its selected coding, computer-use, scientific and cyber evaluations, but those comparisons are first-party and include configuration-specific harnesses. Artificial Analysis independently measured a modest Coding Agent Index increase over [[entities/models/gpt-5-6]] Sol (67.0 versus 65.1) in the Codex harness alongside substantially lower token use; it also found a 61 tie with Sol in its broader Intelligence Index and a higher max-effort cost per task because Astra's list price is 2.5× Sol's. The evidence supports a controlled candidate route, not a default-model conclusion. ^[raw/articles/gpt-6-astra-2026-09-05.md]

## Controlled adoption guidance

Compare Astra with Sol and [[entities/models/claude-fable-5-1]] using the same retained coding/review tasks, context policy, tool permissions, time/token budget and independent acceptance tests. Record success, retries, tool failures, wall-clock time, cache behavior and total cost per accepted task; do not infer task economics from token price or a vendor benchmark. Preserve the independent receipts, isolation and merge gates described in [[coding/architecture/merge-gated-dag-coding-workflow]] and [[comparisons/model-routing-hermes-opencode-pi]].

## Related

- [[entities/models/gpt-5-6]]
- [[entities/models/claude-fable-5-1]]
- [[comparisons/model-routing-hermes-opencode-pi]]
- [[coding/architecture/merge-gated-dag-coding-workflow]]
