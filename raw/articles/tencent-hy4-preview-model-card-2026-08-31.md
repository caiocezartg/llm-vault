---
source_url: https://huggingface.co/tencent/Hy4-preview
ingested: 2026-08-31
sha256: 945dda7ae94a1af6c3cdf98244f7005f7efa468ceeb73740a8eb2982e2657f67
---
# Tencent Hy4 preview — primary model-card excerpt

Hy4 preview is a Tencent Hy Team Mixture-of-Experts flagship. The published model card states: 770B total parameters, 49B activated per token, 78 layers, 256 routed experts plus one shared expert, top-8 routing, native MTP speculative-decoding layer, and 1M context length.

Tencent distributes Hy4 preview and an FP8 variant under Apache-2.0. The card documents deployment via vLLM or SGLang through an OpenAI-compatible API. The card describes the default reasoning mode as `high`, with an explicit `no_think` option for direct responses.

The publisher claims improved long-horizon software-engineering planning, debugging and verification, and reports internal blind pairwise evaluation by 163 experts across 203 engineering tasks. Those relative scores are vendor evidence, not an independent result.

The model card labels the release as early and lists known issues: it can reason longer than necessary on complex tasks and over-verify work. The stated evaluation/benchmark claims therefore require controlled comparison in a like-for-like harness before routing or self-hosting decisions.

Source: https://huggingface.co/tencent/Hy4-preview
