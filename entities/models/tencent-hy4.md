---
title: Tencent Hy4 preview
created: 2026-08-31
updated: 2026-08-31
type: entity
tags: [llm, model, open-weight, inference, agent, evaluation]
sources: [raw/articles/tencent-hy4-preview-model-card-2026-08-31.md]
confidence: medium
contested: false
contradictions: []
---
# Tencent Hy4 preview

## Overview

Tencent released **Hy4 preview** on 30 August 2026 as an Apache-2.0, FP8 Mixture-of-Experts model with 770B total parameters, 49B active per token, a 1M-token context window and documented vLLM/SGLang serving. It is a substantial open-weight candidate for long-context coding and agent trials, but its total size and preview status make it an evaluation target rather than a default routing choice. ^[raw/articles/tencent-hy4-preview-model-card-2026-08-31.md]

## Evidence boundary

The model card positions Hy4 for planning, debugging, verification and multi-step software engineering, and reports internal expert comparison over 203 engineering tasks. Those numbers are vendor evidence, not an independent measure of task completion, tool correctness, recovery, serving cost or operational safety. The card itself notes excessive reasoning/verification on some complex requests. ^[raw/articles/tencent-hy4-preview-model-card-2026-08-31.md]

Hy4 belongs beside [[entities/models/glm-5-3]] and [[entities/models/muse-glimmer]] in a controlled open-model evaluation pool. Their advertised context lengths, benchmark families, sparsity and hardware envelopes differ; none establishes a like-for-like winner without a fixed harness.

## Controlled-trial boundary

1. Verify the deployed weights, license, serving version, quantization and endpoint behavior before scoring a task.
2. Run fresh retained repository tasks with fixed context, tools, budgets, acceptance gates and failure injections; record verified completion, wall time, effective cost, peak memory, retries and out-of-scope edits.
3. Preserve scoped credentials, allowlisted egress, isolated execution and external repository gates. A local/open route changes portability and data locality, not execution authority; follow [[comparisons/model-routing-hermes-opencode-pi]].

## Sources

- [[raw/articles/tencent-hy4-preview-model-card-2026-08-31]]
- [Tencent Hy4 preview model card](https://huggingface.co/tencent/Hy4-preview)
- [Tencent launch announcement](https://www.tencent.com/tencent-releases-and-open-sources-tencent-hy4-preview/)
- [Hacker News launch discussion](https://news.ycombinator.com/item?id=49492632)
