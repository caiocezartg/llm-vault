---
title: Grok 4.7
created: 2026-09-22
updated: 2026-09-22
type: entity
tags: [llm, model, reasoning, coding, agent, inference, evaluation, context-window]
sources:
  - https://x.ai/news/grok-4-7
  - https://artificialanalysis.ai/articles/benchmarking-grok-4-7
  - https://github.blog/changelog/2026-09-21-grok-4-7-is-now-available-in-github-copilot
confidence: medium
contested: false
contradictions: []
---

# Grok 4.7

## Overview

SpaceXAI released Grok 4.7 on 21 September 2026 as a coding and knowledge-work model, replacing Grok 4.6 as the current route. The official announcement says it uses a larger base model and longer reinforcement learning on difficult, multi-hour tasks; it is offered through the API, Grok Build, Cursor, model routers and third-party coding harnesses. GitHub separately began a gradual Copilot rollout across supported paid and organization plans. ^[raw/articles/spacexai-grok-4-7-2026-09-21.md]

## Evaluation and cost boundary

Artificial Analysis measured Grok 4.7 (xhigh) plus its native Grok Build harness at 56 on its Coding Agent Index, up nine points from Grok 4.6 (xhigh), with Terminal-Bench 4.0 rising from 18% to 33%. This is useful independent evidence of a material change, but it is a **model-plus-harness** result rather than portable evidence that the model will perform the same way through every coding agent. The same evaluator measured notably higher output-token use: about 81k per Intelligence Index task, versus 36k for Grok 4.6 (high). [Artificial Analysis evaluation](https://artificialanalysis.ai/articles/benchmarking-grok-4-7)

The vendor lists $2/M input and $6/M output tokens, unchanged from Grok 4.6, with a 500k-token context window. Cost per successful accepted task therefore remains a trial question: higher completion quality may be offset by substantially longer output and tool trajectories. ^[raw/articles/spacexai-grok-4-7-2026-09-21.md]

## Adoption boundary

The immediate distribution surface is broad but uneven: GitHub says Copilot availability is gradual and organization administrators control access through model policy. Do not replace an existing production default solely from frontier benchmarks or model-picker availability; preserve the requested/effective model in run receipts and compare it on retained repository tasks with the same worktree isolation, test gates, budget and timeout settings.

## Suggested controlled trial

1. Route a small, fixed set of difficult coding, debugging and review tasks to Grok 4.7 and the current fallback under identical harness constraints.
2. Capture accepted-task rate, test/review failures, wall-clock time, input/output tokens, retries and recovery effort—not only a benchmark score.
3. Escalate only if the model's higher token use improves accepted outcomes enough to justify total cost and latency.

This trial rule is compatible with [[comparisons/model-routing-hermes-opencode-pi]] and the independent-gate design in [[coding/architecture/merge-gated-dag-coding-workflow]]. The broader migration/policy distinction in [[entities/models/gpt-5-6]] remains relevant when the route is GitHub Copilot rather than a direct API.

## Related

- [[entities/models/gpt-5-6]]
- [[comparisons/model-routing-hermes-opencode-pi]]
- [[coding/architecture/merge-gated-dag-coding-workflow]]
