---
title: Production LLM serving: memory optimization and cache integrity
created: 2026-08-04
updated: 2026-08-04
type: concept
tags: [llm, inference, evaluation, architecture]
sources: [raw/articles/cloudflare-smaller-faster-safer-2026-08-03.md]
confidence: medium
contested: false
contradictions: []
---
# Production LLM serving: memory optimization and cache integrity

## Overview

For long-context or high-concurrency LLM services, the deployment decision should be separated by phase: **prefill** is often compute-bound, while **decode** can be memory-bandwidth- and KV-cache-bound. A production report from Cloudflare on Kimi and GLM serving uses that split to retain FP8 weights/cache only where it is beneficial and introduces a cache-integrity check for shared physical pages. The pattern is relevant to any eventual serving evaluation of large MoE models such as [[entities/models/kimi-k3]] or [[entities/models/qwen3-8-max]], not a claim that their behavior is identical. ^[raw/articles/cloudflare-smaller-faster-safer-2026-08-03.md]

## Durable operating pattern

- Measure TTFT/prefill, inter-token latency/decode, throughput, GPU memory, cache capacity and task quality separately; aggregate tokens/s can conceal a prefill regression.
- Treat FP8 KV cache as a conditional capacity/latency optimization. Validate the exact model, attention backend, GPU, context distribution and tool/coding workload. vLLM's public testing found both fixed long-context accuracy defects and paths needing calibration or BF16 exclusions.
- Weight compression can improve decode bandwidth while slowing prefill. A split deployment must be benchmarked end-to-end, including routing and handoff overhead, not only with kernel microbenchmarks.
- A shared KV cache is also a trust boundary: page ownership/version tags and fail-closed checks before decode illustrate a defense-in-depth option for multi-tenant serving. It does not replace identity, authorization, isolation, auditability or independent security review.

## Evidence boundary

Cloudflare's throughput, cost and quality results are first-party measurements on its own SGLang/H200 deployment. The vLLM work independently corroborates that FP8 KV quantization can be useful but supplies material caveats: it recorded a 128K long-context failure before a kernel fix, model-specific degradation for Kimi-K2.5 without calibration, and configurations where BF16 remains faster. Thus, the reusable conclusion is a **measurement protocol**, not a universal recommendation to quantize.

## Evaluation checklist

1. Establish BF16 or equivalent baseline on fresh, repository-native coding/tool tasks plus representative long-context prompts.
2. Compare prefill and decode separately at the intended concurrency, then run mixed traffic; record TTFT, ITL, total latency, capacity, cost and error/retry rate.
3. Include long-context retrieval, structured outputs and multi-step tool loops. Benchmark-only quality parity is insufficient for agent routing.
4. For shared infrastructure, test cache ownership/mapping mismatch handling and retain action telemetry; follow the wider containment controls in [[coding/architecture/merge-gated-dag-coding-workflow]].

## Sources

- [[raw/articles/cloudflare-smaller-faster-safer-2026-08-03]]
- [Cloudflare production-serving report, 3 August 2026](https://blog.cloudflare.com/smaller-faster-safer-models/)
- [vLLM: FP8 KV-cache and attention quantization](https://vllm-project.github.io/2026/04/22/fp8-kvcache.html)
- [Hacker News technical discussion](https://news.ycombinator.com/item?id=49158581)
