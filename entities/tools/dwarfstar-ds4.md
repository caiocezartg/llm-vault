---
title: DwarfStar 4 (ds4)
created: 2026-10-03
updated: 2026-10-03
type: entity
tags: [llm, model, inference, open-weight, tool, cli, coding, agent]
sources: [raw/articles/antirez-ds4-current-state-2026-10-03.md]
confidence: medium
contested: false
contradictions: []
---
# DwarfStar 4 (ds4)

## Overview

DwarfStar 4 (`ds4`) is an MIT-licensed local inference engine in C for selected large open-weight models on Metal, CUDA and ROCm. Its documented stack exposes a CLI, OpenAI- and Anthropic-compatible local APIs, and integration guidance for [[entities/tools/hermes-agent]], OpenCode, Codex CLI, Claude Code and Pi. It currently targets particular DeepSeek V4/V4.1 Flash, GLM 5.x and Qwen 3.8 GGUF layouts rather than acting as a general model-serving layer. ^[raw/articles/antirez-ds4-current-state-2026-10-03.md]

## Why it is notable

The current design combines asymmetric low-bit quantization, disk-resident KV cache, SSD streaming and tensor parallelism to make selected routed-MoE models viable on high-memory Apple Silicon or GPU systems. The project publishes reproducible commands and baseline throughput tables, but those are its own measurements—not a like-for-like independent comparison with [[concepts/production-llm-serving-memory-integrity]], llama.cpp, vLLM, MLX or other runtimes. ^[raw/articles/antirez-ds4-current-state-2026-10-03.md]

A 3 October 2026 Hacker News thread had 221 points and 56 comments, with examples of bindings/integrations as well as requests for broader Intel/AMD support. That is current developer attention and early ecosystem activity, not proof of portability, quality or agentic-coding performance. The repository snapshot recorded 23,024 stars, 2,218 forks and no tagged releases; pin a reviewed commit rather than treating its current branch as a stable production contract. ^[raw/articles/antirez-ds4-current-state-2026-10-03.md]

## Controlled evaluation boundary

1. Start only on hardware in the documented memory/backend matrix, with an exact model build and commit pinned.
2. Compare the same model, quantization, context length, cache state and concurrency against an existing runtime; separately measure prefill, decode, cold/warm restart and task-level correctness.
3. Treat the local OpenAI/Anthropic-compatible endpoint as an inference boundary, not a security boundary. Keep task-scoped files, egress, credentials, review and repository-native gates outside the model server as defined in [[coding/architecture/merge-gated-dag-coding-workflow]].

## Sources

- [ds4 repository and documented benchmark conditions](https://github.com/antirez/ds4)
- [DwarfStar documentation](https://dwarfstar.sh/)
- [Hacker News discussion](https://news.ycombinator.com/item?id=49936575)
