---
source_url: https://aleph-alpha.com/en/blog/kolibri-has-landed-a-sovereign-open-weight-model/
ingested: 2026-10-04
sha256: fa18e56fc29b45267a6f161d4dbd071784ebfad643fb26e6edd5dccececba4c7
---
# Kolibri — bounded primary-source record

**Source title:** Kolibri Has Landed: A Sovereign Open-Weight Model  
**Published by source:** 2026-10-03  
**Captured:** 2026-10-04

Aleph Alpha announced Kolibri as an English-German Mixture-of-Experts transformer with 78B total parameters and 3B active parameters (the model card specifies 3.46B active). The weights are available on Hugging Face under Apache 2.0. The stated context window is up to 1,048,576 tokens; the model card recommends contexts no larger than 262,144 tokens for serving efficiency and complex work.

The official model card lists explicit reasoning mode and tool calling, and says the intended use includes multi-step reasoning, coding, retrieval-augmented generation, long-document processing and agentic workflows in German and English. It documents an FP8 model footprint of about 78 GB and minimum serving hardware of 2× A100 80 GB, 2× H100 SXM5, 1× H200, 1× B200 or 1× B300. It provides an Aleph Alpha vLLM plugin and documents a `vllm serve` path with Kolibri-specific reasoning and tool-call parsers.

The announcement and card report benchmark comparisons, but these are vendor-produced results; they do not establish success, latency, cost, safety or reliability in a separate coding harness. The model card explicitly frames agentic use around human review and says a calling system should validate results before actions are taken.

Primary URLs:
- https://aleph-alpha.com/en/blog/kolibri-has-landed-a-sovereign-open-weight-model/
- https://huggingface.co/Aleph-Alpha/Kolibri-1
- https://aleph-alpha.com/downloads/tech-report.pdf
