---
title: Muse Glimmer
created: 2026-08-11
updated: 2026-08-11
type: entity
tags: [llm, model, open-weight, inference, agent, evaluation]
sources: [raw/articles/meta-muse-glimmer-2026-08-11.md]
confidence: medium
contested: false
contradictions: []
---

# Muse Glimmer

## Overview

Muse Glimmer is Meta's Apache-2.0, 30B open-weight model released on 2026-08-10 for local agent workflows, tool use, coding and evaluation. Meta supplies quantized variants intended to make the language model fit below 20 GB, with a stated 24–32 GB envelope after working memory and auxiliary components. It is a candidate for controlled local-inference trials, not an established replacement for a production coding model. ^[raw/articles/meta-muse-glimmer-2026-08-11.md]

## Integration and evaluation boundary

The vendor has published weights and documentation; it says optimized llama.cpp, MLX and ExecuTorch integrations are imminent and lists serving/packaging routes such as vLLM, SGLang and Ollama. Its benchmark and speed results are vendor evidence. They do not establish performance, cost, reliability, prompt-injection resistance or recovery behavior in a Hermes/OpenCode/Pi task packet. ^[raw/articles/meta-muse-glimmer-2026-08-11.md]

The useful comparison point is [[entities/models/lfm25-26b]]: LFM2.5 is a tiny bounded-loop candidate whose own card excludes agentic coding, whereas Muse Glimmer has a much larger local footprint and is explicitly positioned for coding and agentic tasks. Both require workload-specific trials rather than model-card extrapolation. The routing and authority boundaries in [[comparisons/model-routing-hermes-opencode-pi]] still apply: local/open weights improve portability and data locality but do not grant a model tool, network, credential or merge authority.

## Controlled-trial guidance

Use a disposable local endpoint and fresh, fixed tasks. Measure end-to-end verified task success, tool-call schema correctness, recovery after controlled failures, elapsed time, token/energy cost, peak memory, and behavior outside task scope. Keep repository gates, sandbox/egress policy and scoped credentials outside the model. Compare the same tasks with the incumbent API route before changing any routing policy.

## Related

- [[entities/models/lfm25-26b]]
- [[comparisons/model-routing-hermes-opencode-pi]]
- [[entities/tools/hermes-agent]]
