---
source_url: https://research.meta.ai/blog/introducing-muse-glimmer-open-agentic-model
ingested: 2026-08-11
sha256: 91ec233b52eb0cb731f5645afa9effc935c08f244966084720be420c844dac09
---

# Meta — Muse Glimmer (bounded primary-source excerpt)

On 2026-08-10, Meta announced Muse Glimmer and released its weights under Apache-2.0. Meta describes it as a 30B-parameter model optimized for always-on local agent workflows, including local agents, function calling, local coding and LLM-as-a-judge evaluation.

Meta states that its approximate 4-bit quantized language model is under 20 GB. It positions the full local runtime, including KV cache, perception encoder and speculative-decoding drafter, in a 24 GB or 32 GB memory envelope. Meta reports speculative-decoding speedups on an RTX 5090 and M4/M5 Max hardware, but these are vendor measurements.

The release includes weights on Hugging Face and developer documentation. Meta says optimized integrations for llama.cpp, MLX and ExecuTorch will arrive in the coming days, and mentions future/partner paths through Ollama, LM Studio, Unsloth, vLLM, SGLang, Together AI, Fireworks AI and OpenRouter.

Meta reports evaluations against Gemma4-31B and Qwen3.6-27B across agentic, coding, multimodal, safety and reasoning benchmarks. These performance claims are from Meta and should not be treated as independent evidence for a specific harness, repository workload, cost or safety posture.
