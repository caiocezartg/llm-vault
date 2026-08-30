---
source_url: https://blog.cloudflare.com/smaller-faster-safer-models/
ingested: 2026-08-04
sha256: e8bffd8542049ee484dd9bcec6adf3c83835c5ebdfad5a7a60b2d2229e7a8ac6
---

# Captured primary-source excerpt — Cloudflare: Smaller, faster, safer: running Kimi and GLM at scale

Source date: 2026-08-03
Original URL: https://blog.cloudflare.com/smaller-faster-safer-models/

Cloudflare reports serving Kimi and GLM MoE models with SGLang and describes three production techniques: FP8 KV-cache quantization, INT4 weight compression for GLM 5.2 decode, and integrity checking for shared KV-cache pages. This capture preserves the technical claims material to the accompanying wiki synthesis; the original article remains the authoritative source.

For Kimi K2.6 on a disaggregated H200 deployment, Cloudflare says replacing BF16 KV cache with FP8 approximately doubles resident context from 686,000 to 1.37 million tokens. The reported throughput at concurrency 64 was 2,192 tok/s for FP8 while BF16 had exhausted memory at 32 concurrent requests; Cloudflare reports about 41% greater peak throughput and 30% lower cost per token. It preserves BF16 during prefill because the phase is compute-bound and FP8 has a per-token conversion cost.

For GLM 5.2, Cloudflare reports converting weights from FP8 to INT4 shrinks the checkpoint from 705 GB to 421 GB and lowers per-GPU memory in an 8-way tensor-parallel deployment from about 88 GB to 52 GB. Reported decode throughput gains range from 16% to 55% depending on concurrency, while prefill declines from roughly 10,160 to 8,660 tok/s. The stated production policy is therefore INT4 for memory-bound decode and FP8 for compute-bound prefill.

Cloudflare also describes a KV-cache integrity mechanism: each physical page has a tag that changes on reallocation, and a request's expected page/tag mappings are checked before supported decode operations. A mismatch aborts the request rather than risk returning another request's cache data. The vendor reports under 1% throughput and p95-latency overhead in its measured setup. This is a deployment-specific defense, not a proof of generic multi-tenant safety.

The article claims no meaningful benchmark-accuracy change in its evaluation suites. Independent vLLM technical work, however, documents FP8 KV-cache failure modes: a long-context Hopper accuracy regression that required a two-level accumulation fix; lower prefill performance for some large-head-dimension paths; and a consistent accuracy decrease for Kimi-K2.5 with uncalibrated FP8 cache/attention. Therefore, FP8 is not a default to apply without model-, kernel-, hardware-, context- and workload-specific evaluation.
