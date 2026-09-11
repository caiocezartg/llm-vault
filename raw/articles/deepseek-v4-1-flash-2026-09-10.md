---
source_url: https://deepseek.com/en/news/deepseek-v4-1-flash/
ingested: 2026-09-11
sha256: e9695ac72ee62d607789ea5f7f648e28228acadd86cf568dae889e2314f4ef7c
---
# DeepSeek-V4.1-Flash — bounded primary capture

DeepSeek released V4.1-Flash on 2026-09-10. The native multimodal CED MoE has 552B backbone parameters, up to 1M tokens of context, and activates 8B parameters during prefill and 16B during decode. DeepSeek lists MIT-licensed weights on Hugging Face.

The API model identifier is `deepseek-flash`. Legacy V4 Flash/Vision identifiers temporarily route to V4.1-Flash; `deepseek-v4-pro` will route to it from 2026-09-14 until V4.1 Pro ships. This is a compatibility and reproducibility change as well as a release.

DeepSeek benchmark and cost claims are first-party. Artificial Analysis independently lists the released model, measures 198 output tokens per second in its configuration, and identifies high output verbosity. Results remain configuration-dependent.

Sources:
- https://deepseek.com/en/news/deepseek-v4-1-flash/
- https://huggingface.co/deepseek-ai/DeepSeek-V4.1-Flash
- https://artificialanalysis.ai/models/deepseek-v4-1-flash