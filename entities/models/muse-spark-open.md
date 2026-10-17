---
title: Muse Spark Open
created: 2026-10-17
updated: 2026-10-17
type: entity
tags: [llm, model, inference, agent, coding, open-weight]
sources:
  - raw/articles/meta-muse-spark-open-2026-10-15.md
  - https://machinelearning.apple.com/research/mlx-distributed-inference
  - https://huggingface.co/meta-models/Muse-Spark-Open-816B-A42B
confidence: medium
contested: false
contradictions: []
---

# Muse Spark Open

## What it is

Meta released this natively multimodal MoE model on 2026-10-15 with 816B total parameters, 42B active per token and a claimed 1M-token context. The released weights target coding and long-horizon agent workflows; this makes it a candidate for a controlled routing or self-hosted-inference trial, not a default model route. ^[raw/articles/meta-muse-spark-open-2026-10-15.md]

## Deployment boundary

“Open weight” does not mean lightweight or unrestricted. Apple reports that the NVFP4 version needs about 493GB for the model and does not fit on one 512GB Mac Studio once intermediate inference memory is included; its MLX measurement reaches 15.74 tokens/s on two M5 Ultras or 36.73 tokens/s on four at an 8,192-token context. That is a specific Apple/MLX configuration, not a general performance claim or ordinary-desktop requirement. The Muse Model License also has attribution and Model-as-a-Service conditions; review it before building a hosted offering. ^[raw/articles/meta-muse-spark-open-2026-10-15.md]

## Evaluation and adoption boundary

Meta's task benchmarks and local coding demos are vendor evidence. The release has broad initial discussion and day-zero serving support, but no independent accepted-task comparison for Caio's workflow was found at ingestion. Test a hosted endpoint before procuring hardware: pin model/checkpoint, reasoning effort, harness, context and tool policy; then measure accepted changes, CI/review outcome, latency, total cost and failure/retry behavior.

## Related

- [[entities/models/kolibri]] is a materially smaller open-weight route with its own hardware envelope.
- [[comparisons/model-routing-hermes-opencode-pi]] defines the controlled-routing and accepted-task measurement boundary for any new model.
