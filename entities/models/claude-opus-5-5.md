---
title: Claude Opus 5.5
created: 2026-09-23
updated: 2026-09-23
type: entity
tags: [llm, model, reasoning, tool-calling, context-window, coding, evaluation, inference]
sources: [raw/articles/anthropic-claude-opus-5-5-2026-09-22.md]
confidence: medium
contested: false
contradictions: []
---

# Claude Opus 5.5

## Overview

Anthropic released Claude Opus 5.5 on 22 September 2026 as `claude-opus-5-5`. It has a 1M-token context window and list pricing of US$4/M input, US$20/M output and US$0.20/M cache reads—lower than [[entities/models/claude-opus-5]]. Claude Code v2.1.280 makes it the default Opus choice; GitHub Copilot has also begun a gradual rollout for eligible plans. ^[raw/articles/anthropic-claude-opus-5-5-2026-09-22.md]

## Integration boundaries

- Adaptive thinking is mandatory: explicitly disabling it returns HTTP 400. Named or `any` tool choice also returns HTTP 400; use `auto` with strict tool use if an integration needs constrained tools. ^[raw/articles/anthropic-claude-opus-5-5-2026-09-22.md]
- Computer use on Anthropic API and Google Cloud requires the current `computer_toolset_20260801`; the prior computer tool is retained only on the documented Bedrock route. Treat model selection as route-specific compatibility, not a uniform API swap. ^[raw/articles/anthropic-claude-opus-5-5-2026-09-22.md]
- Claude Code v2.1.280 also corrects a write-authorization edge case involving symlink landing paths. Upgrade before treating in-tree permission rules as protection for writes that resolve outside the worktree. ^[raw/articles/anthropic-claude-opus-5-5-2026-09-22.md]

## Evaluation boundary and trial

Anthropic's coding, latency and cost comparisons are launch evidence. Artificial Analysis places the max-with-fallback configuration first in its current Intelligence Index, while also observing high output-token use and a US$5.98 average cost per its index task. Neither result substitutes for a repository-native agent evaluation. Compare it with [[entities/models/claude-fable-5-1]], [[entities/models/gpt-6-astra]] and [[entities/models/gpt-6-sol-luna]] on retained tasks with fixed tool policy, isolation, budget and independent acceptance gates.

Record requested and effective model, effort, fallback events, cache behavior, tool calls, wall-clock time, total cost, tests/review findings and accepted-task rate. Keep the external controls in [[comparisons/model-routing-hermes-opencode-pi]]: a stronger model or a policy fix does not replace capability scoping, egress control, worktree isolation or independent review.

## Sources

- [Anthropic announcement](https://www.anthropic.com/claude-opus-5-5)
- [Claude Code v2.1.280 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.280)
- [Artificial Analysis model evaluation](https://artificialanalysis.ai/models/claude-opus-5-5)
- [Hacker News discussion](https://news.ycombinator.com/item?id=49803892)
