---
title: Bonsai 27B
created: 2026-07-15
updated: 2026-07-15
type: entity
tags: [llm, model, inference, open-weight, multimodal, tool-calling, benchmark]
sources:
  - raw/articles/prismml-bonsai-27b-2026-07-15.md
  - https://huggingface.co/prism-ml/Bonsai-27B-gguf
  - https://news.ycombinator.com/item?id=48910545
confidence: medium
contested: false
contradictions: []
---
# Bonsai 27B

## Overview

**Bonsai 27B** is PrismML's 14 July 2026 low-bit release derived from Qwen3.6-27B. It publishes Apache-2.0 binary and ternary variants intended for local inference: the 1-bit build is documented at about 3.9 GB for language weights and the quality-oriented ternary build at about 7.2 GB deployed. The project provides GGUF/llama.cpp and Apple MLX paths, and documents a 262K context capability with a separately loaded vision component. ^[raw/articles/prismml-bonsai-27b-2026-07-15.md]

## Engineering relevance

The model is a plausible candidate for **bounded, privacy-sensitive local tasks** or for a hybrid routing tier below a cloud frontier model. It changes the feasibility envelope more than it establishes a new coding-agent default: the model card explicitly says long-horizon, multi-file agentic coding is not yet a strong target. Any trial should therefore use a fixed local eval set, constrained tools, a short context first, and repository-native acceptance tests — not vendor aggregate scores alone. This fits the controlled-adoption guidance in [[entities/models/gpt-5-6]] and the gates in [[coding/architecture/kitdev-deterministic-agentic-workflows]].

PrismML's 15-benchmark retention and throughput figures are first-party measurements. The release did receive early public scrutiny on Hacker News, including concrete concerns about comparative tool use, vision quality and agentic reliability; that is useful attention, but not an independent benchmark or production-adoption signal. ^[raw/articles/prismml-bonsai-27b-2026-07-15.md]

## Suggested trial boundary

Test the ternary build before the 1-bit build when quality matters. Record model file, runtime/fork revision, hardware, effective context size, token rate, cost, task success, tool-call correctness and post-test failure rate. Do not infer that a 3.9 GB weight file implies phone viability at a target context: runtime buffers, KV cache and optional vision assets determine peak memory.

## Related

- [[entities/models/gpt-5-6]]
- [[coding/architecture/kitdev-deterministic-agentic-workflows]]
- [[projects/hermes-research-daily-radar]]
