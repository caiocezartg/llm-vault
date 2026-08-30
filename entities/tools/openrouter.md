---
title: OpenRouter
created: 2026-08-20
updated: 2026-08-20
type: entity
tags: [tool, api, llm, model, inference, openrouter]
sources:
  - raw/articles/openrouter-stripe-2026-08-20.md
  - https://news.ycombinator.com/item?id=49364559
confidence: medium
contested: false
contradictions: []
---

# OpenRouter

## Overview

OpenRouter is a model gateway/marketplace that presents one integration layer across multiple model providers, with routing, model metadata, observability and cost-management functions. In a Hermes-centered setup, it is an upstream routing option rather than a replacement for typed task boundaries, isolated execution, scoped credentials, or external acceptance gates. [[comparisons/model-routing-hermes-opencode-pi]]

## Joining Stripe — 2026-08-19

OpenRouter announced an agreement to join Stripe, subject to closing conditions. It says existing integrations, product, name and roadmap will continue unchanged. The announcement claims 10+ trillion tokens per day, 400+ models and 10+ million developers/companies, but these are first-party scale claims. ^[raw/articles/openrouter-stripe-2026-08-20.md]

The durable operational consequence is vendor concentration risk at a dependency that may be used for model routing, billing and observability. Treat the stated continuity and neutrality commitments as claims to monitor, not guarantees. Preserve a tested direct-provider or alternate-gateway fallback; pin model/provider policy explicitly; log requested versus effective routing; and test failure, quota, privacy, retention and regional-routing behavior before a critical workload depends on the gateway. This is the same authority boundary that applies to credential intermediaries such as [[entities/tools/onecli]]: a convenience/control plane does not itself verify the safety or correctness of downstream actions.

## Evidence and uncertainty

The announcement generated substantial HN discussion (816 points and 418 comments in the 20 August 2026 collection). Participants reported practical benefits such as one-key multi-provider access, model metadata, budgets and fallback routing, while also questioning markup, provider/model integrity, privacy and how Stripe ownership could change product incentives. This is a strong adoption and scrutiny signal, not an independent audit of the transaction's future effects. [Discussion](https://news.ycombinator.com/item?id=49364559)

## Related

- [[comparisons/model-routing-hermes-opencode-pi]]
- [[entities/tools/hermes-agent]]
- [[entities/tools/onecli]]
