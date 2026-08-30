---
title: Kimi K3
created: 2026-07-19
updated: 2026-07-28
type: entity
tags: [llm, model, reasoning, tool-calling, context-window, open-weight, inference]
sources: [raw/articles/moonshot-kimi-k3-2026-07-19.md]
confidence: medium
contested: false
contradictions: []
---
# Kimi K3

## Overview

Kimi K3 is Moonshot AI's 2.8T-parameter Mixture-of-Experts flagship, announced in July 2026 for long-horizon coding, tool use, reasoning, knowledge work and vision. It is API-available with a stated 1M-token context and was a candidate for controlled routing experiments alongside [[entities/models/gpt-5-6]].^[raw/articles/moonshot-kimi-k3-2026-07-19.md]

## Material update — weights and report published (27 July 2026)

Moonshot published the full MXFP4 model weights on the verified `moonshotai/Kimi-K3` Hugging Face repository, alongside a technical report and the Kimi K3 License. The published architecture specifies 2.8T total / 104B activated parameters, 93 layers, 16 selected experts from 896, native text-and-image input, and a 1,048,576-token context. This changes the model from an API-only routing candidate into an evaluable self-hosting/provider-portability option, but not into a practical local model for ordinary developer hardware. The 27 July repository was already at roughly 2.5k GitHub stars/189 forks when checked, while the HN launch discussion reached 1,335 points and 526 comments; those signals establish attention, not independent quality or serving-cost proof.

The technical report's relative coding and agentic results remain largely vendor-reported and sometimes use different harnesses across models. The model card itself notes a noticeable UX gap to leading proprietary models, sensitivity to incomplete preserved thinking history, and a tendency to make unexpected decisions under ambiguous intent. Treat claims of long-horizon autonomy as hypotheses to test under a compatible, constrained harness—not as a reason to relax task boundaries, authorization, egress controls, or independent acceptance gates.

## Integration-relevant facts

- API model name: `kimi-k3`; uses an OpenAI-SDK-compatible Chat Completions endpoint and supports `reasoning_content`, streaming, function calling, strict JSON Schema output, vision inputs and automatic context caching.^[raw/articles/moonshot-kimi-k3-2026-07-19.md]
- It currently accepts only `reasoning_effort=max`; requests need to preserve the complete assistant message across turns and tool calls. This makes adapter conformance testing more important than headline context length.^[raw/articles/moonshot-kimi-k3-2026-07-19.md]
- Moonshot explicitly warns of instability when historical thinking content is not preserved or when switching an in-progress session from another model. This reinforces the task-boundary handoff approach in [[comparisons/model-routing-hermes-opencode-pi]] and the controlled-evaluation discipline in [[coding/architecture/kitdev-deterministic-agentic-workflows]].^[raw/articles/moonshot-kimi-k3-2026-07-19.md]

## Evidence and caveats

Moonshot's coding and agentic benchmark claims are first-party and compare models across differing harnesses in several cases. The launch has strong early Hacker News attention, but that is not a substitute for an independent, repository-native evaluation. The listed model is therefore `medium` confidence for availability and interface facts, not for relative coding quality.

## Recommended trial boundary

1. Do not assume "open weights" implies local deployment: calculate memory, throughput, GPU topology, license, and provider economics for the intended workload before provisioning.
2. For API or self-hosted evaluation, use a fresh, bounded task per run; do not switch a partially completed agent session from another model.
3. Validate tool-call round trips, strict-schema output, preserved-thinking compatibility, context-cache behavior, cost, and completion quality on the same repository-native tasks used for [[entities/models/gpt-5-6]].
4. Maintain explicit behavioral constraints and independent test/review gates: Moonshot documents a risk of over-proactive behavior under ambiguity.

## Sources

- [[raw/articles/moonshot-kimi-k3-2026-07-19]]
- [Moonshot Kimi K3 technical blog](https://www.kimi.com/blog/kimi-k3)
- [Kimi K3 API quickstart](https://platform.kimi.ai/docs/guide/kimi-k3-quickstart)
- [Official Hugging Face model card and weights](https://huggingface.co/moonshotai/Kimi-K3)
- [Official Kimi K3 technical report repository](https://github.com/MoonshotAI/Kimi-K3)
- [Hacker News discussion of the open-weight release, 27 July 2026](https://news.ycombinator.com/item?id=49065752)
- [Hacker News discussion of the API launch, 19 July 2026](https://news.ycombinator.com/item?id=48960218)
