---
title: DeepSeek V4.1 Flash
created: 2026-09-11
updated: 2026-09-11
type: entity
tags: [llm, model, multimodal, open-weight, inference, coding, evaluation]
sources:
  - raw/articles/deepseek-v4-1-flash-2026-09-10.md
confidence: medium
contested: false
contradictions: []
---

# DeepSeek V4.1 Flash

## What changed

DeepSeek released its MIT-licensed, open-weight V4.1 Flash model on 2026-09-10. It is a native multimodal MoE with a one-million-token context window; the documented Causal Encoder-Decoder architecture activates 8B parameters during prefill and 16B during decoding from a 552B backbone. The claimed KV-cache compression is relevant to long-context agent economics, but it does not reduce the total deployment footprint to a routine local setup. ^[raw/articles/deepseek-v4-1-flash-2026-09-10.md]

## API and migration boundary

`deepseek-flash` selects the new version. DeepSeek temporarily routes legacy V4 Flash/Vision names to V4.1 Flash, and will route V4 Pro requests from 2026-09-14 until V4.1 Pro is released. Treat that as an implicit production-model change: pin model IDs where possible, preserve run receipts, and rerun retained acceptance tasks before relying on former V4-Pro/V4-Flash behavior. ^[raw/articles/deepseek-v4-1-flash-2026-09-10.md]

## Evidence and trial guidance

DeepSeek's coding/agent benchmark figures are vendor results. Artificial Analysis independently reports 198 output tokens/s in its configuration and notes unusually high verbosity; neither result establishes accepted-task cost for another harness. Evaluate against [[entities/models/gpt-6-astra]] and [[entities/models/gemini-3-6-flash]] with the same repository fixtures, tool permissions, reasoning setting, context/retry budget, and independent acceptance gates. Measure accepted change, retries, latency, total cost, and output/trace volume—not a headline cache price or benchmark alone.

## Related

- [[comparisons/model-routing-hermes-opencode-pi]]
- [[entities/models/gpt-6-astra]]
- [[entities/models/gemini-3-6-flash]]