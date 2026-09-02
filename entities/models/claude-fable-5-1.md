---
title: Claude Fable 5.1
created: 2026-09-02
updated: 2026-09-02
type: entity
tags: [llm, model, reasoning, tool-calling, context-window, coding, evaluation, inference]
sources: [raw/articles/anthropic-claude-fable-51-2026-09-01.md]
confidence: medium
contested: false
contradictions: []
---

# Claude Fable 5.1

## Overview

Claude Fable 5.1 is Anthropic's general-access successor to Fable 5 for long-running coding, knowledge-work and research tasks, released on 1 September 2026 as `claude-fable-5-1`. [[entities/models/claude-opus-5]] remains the documented starting point for most workloads; Fable 5.1 is a high-capability candidate only after a fixed-harness trial. The same underlying weights are offered as restricted-access Mythos 5.1, with different safeguards.^[raw/articles/anthropic-claude-fable-51-2026-09-01.md]

## Integration and migration facts

- API context is 1M tokens with up to 128K output, and adaptive thinking is always enabled. The model's list input/output prices remain US$10/M and US$50/M, while cache reads are US$0.25/M. Anthropic's estimated 25% typical and up-to-45% highly-agentic savings are vendor workload estimates, not a general cost guarantee.^[raw/articles/anthropic-claude-fable-51-2026-09-01.md]
- `tool_choice` with `any` or a named `tool` is a breaking change: it returns HTTP 400. Use `auto` plus strict tool use or structured outputs for schemas; test the actual tool-call behavior, because Fable 5.1 can issue fewer parallel calls than Fable 5 in agent loops.^[raw/articles/anthropic-claude-fable-51-2026-09-01.md]
- Treat conversations as append-only. Earlier Claude models cannot read Fable 5.1 thinking blocks; editing an earlier message, system prompt or tools array can invalidate later blocks. Log `input_transformations`, use mid-conversation controls, and use server-side compaction/context editing instead of rewriting history.^[raw/articles/anthropic-claude-fable-51-2026-09-01.md]
- Data handling is a route-selection constraint: Fable 5.1 and Mythos 5.1 carry 30-day retention unless zero-data-retention access is explicitly authorized. Fable 5.1 may assist source-code vulnerability discovery but has safeguards that restrict exploit development.^[raw/articles/anthropic-claude-fable-51-2026-09-01.md]

## Controlled-trial guidance

Evaluate against [[entities/models/claude-opus-5]] and [[entities/models/gpt-5-6]] on retained coding/research tasks using an unchanged harness, repository state, tool policy, egress/credential boundary and external acceptance gates. Record effective model/fallback identity, successful-task cost, wall-clock time, tool-call parallelism, cache hit rate, history-binding drops, refusals and review findings. The routing boundary in [[comparisons/model-routing-hermes-opencode-pi]] still applies: do not infer fleet savings from cache-price claims or replace independent gates with a stronger model.

## Evidence boundary

Anthropic reports large benchmark gains, particularly on Terminal-Bench-Science, but its published scores, early-access customer quotes and cost estimates are vendor evidence. The launch immediately received substantial Hacker News attention and criticism around pricing, fallback/safeguard behavior and long-run reliability; this is an adoption/attention signal, not an independent benchmark replication. A separate practical experiment by Simon Willison demonstrated that effort settings can change output time and cost sharply on a creative task, reinforcing the need to measure workload-specific cost/latency.

## Sources

- [Anthropic announcement and availability](https://www.anthropic.com/claude-fable-and-mythos-5-1)
- [Claude Platform: migration, behavior and pricing](https://platform.claude.com/docs/en/models/fable-5-1/whats-new-fable-5-1)
- [Anthropic system card](https://www.anthropic.com/claude-fable-5-1-mythos-5-1-system-card)
- [Hacker News discussion](https://news.ycombinator.com/item?id=49525378)
- [Simon Willison's effort/cost experiment](https://simonwillison.net/2026/Sep/1/claude-fable-5-1/)
