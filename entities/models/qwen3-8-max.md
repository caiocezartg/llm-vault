---
title: Qwen3.8-Max
created: 2026-08-03
updated: 2026-08-03
type: entity
tags: [llm, model, reasoning, tool-calling, context-window, open-weight, inference, evaluation, agent]
sources: [raw/articles/qwen-qwen3-8-max-2026-08-03.md]
confidence: medium
contested: false
contradictions: []
---
# Qwen3.8-Max

## Overview

Qwen released **Qwen3.8-Max** on 2 August 2026 as its API-available flagship: a Mixture-of-Experts model with 2.4T total and 95B active parameters. Qwen says this is its first Max-class model whose weights will be released next week; until the weights, license and serving guidance are actually published, it is an API evaluation candidate rather than a self-hosting option. ^[raw/articles/qwen-qwen3-8-max-2026-08-03.md]

The release is immediately relevant to model-routing experiments because Qwen documents OpenAI Responses compatibility, a Codex configuration example, text/image inputs, parallel tool calls and a stated 1M-token context. Interface compatibility does not prove behavioral compatibility: validate tool-loop serialization, long-context behavior, cost and failure recovery on the same task corpus used for [[entities/models/gpt-5-6]] and [[entities/models/kimi-k3]].

## Evidence boundary

Qwen’s launch table and autonomous-work demonstrations are first-party. The company reports a 10+ day coding run that produced `oh-my-cli`, and as of 30 July reports 16 autonomous days, 265 commits, 127 pull requests and 151 issues. The public repository exists and was still receiving signed merges on 3 August, but repository activity verifies an artifact—not that a model independently made each engineering decision or that the workflow generalizes. ^[raw/articles/qwen-qwen3-8-max-2026-08-03.md]

The launch drew rapid attention on Hacker News (480 points and 211 comments roughly five hours after submission at collection). Discussion included practical experience with prior Qwen local models, hardware/quantization concerns, and skepticism about marketing language and long-horizon autonomy. This is a strong early attention signal, not an independent benchmark, cost study, security review or quality verdict. ^[raw/articles/qwen-qwen3-8-max-2026-08-03.md]

## Controlled evaluation boundary

1. Treat Qwen’s relative benchmark and autonomous-run numbers as hypotheses until an independent evaluation uses comparable harnesses and tasks.
2. Pilot the API only on fresh, bounded repository tasks with fixed model/harness settings; record success, time, tokens/cost, tool errors, recovery attempts, out-of-scope changes and independent review findings.
3. Keep isolated execution, allowlisted tools/egress, explicit authority, and repository-native gates. Long-horizon claims do not replace the control-plane boundaries in [[coding/architecture/merge-gated-dag-coding-workflow]].
4. Reassess self-hosting only after official weights, license, memory/throughput guidance and a reproducible serving path are published.

## Sources

- [[raw/articles/qwen-qwen3-8-max-2026-08-03]]
- [Qwen official release](https://qwen.ai/blog?id=qwen3.8)
- [Autonomous coding demonstration repository](https://github.com/qwen-code-dev-bot/oh-my-cli)
- [Hacker News discussion](https://news.ycombinator.com/item?id=49150470)
