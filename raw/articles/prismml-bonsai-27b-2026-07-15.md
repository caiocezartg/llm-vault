---
source_url: https://prismml.com/news/bonsai-27b
ingested: 2026-07-15
sha256: fddf10e6bfb93dfd28c74a78708007dc5b7ea8a3152f73058e1c423e735b5d93
---
# Capture: PrismML announcement — Bonsai 27B

Source URL: https://prismml.com/news/bonsai-27b
Captured: 2026-07-15

# Announcing Bonsai 27B: The First 27B-Class Model to Run on a Phone

PrismML announced Bonsai 27B on 14 July 2026. The release is derived from Qwen3.6 27B and publishes two Apache-2.0 variants: a binary 1-bit build and a ternary build. PrismML describes the 1-bit model as a 3.9 GB deployed language-model footprint and the ternary variant as a quality-oriented option. It claims 262K context and multimodal support, with device backends based on its own low-bit forks of llama.cpp, MLX, and MLX Swift.

The publisher reports 15 thinking-mode benchmarks against the full-precision baseline. Those results are vendor measurements, not an independent performance evaluation. The official Hugging Face model card documents an important scope limit: long-horizon, multi-file agentic coding is not yet a strong target of this release; an agentic-coding-tuned variant is on the roadmap.

Primary announcement: https://prismml.com/news/bonsai-27b
Model card: https://huggingface.co/prism-ml/Bonsai-27B-gguf
Ternary model card: https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf
Whitepaper: https://github.com/PrismML-Eng/Bonsai-demo/blob/main/bonsai-27b-whitepaper.pdf
