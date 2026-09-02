---
title: Claude Opus 5
created: 2026-07-25
updated: 2026-09-02
type: entity
tags: [llm, model, reasoning, tool-calling, context-window, coding, evaluation]
sources: [raw/articles/anthropic-claude-opus-5-2026-07-24.md, raw/articles/anthropic-claude-code-v21224-2026-08-08.md, raw/articles/anthropic-claude-fable-51-2026-09-01.md]
confidence: medium
contested: false
contradictions: []
---

# Claude Opus 5

## Overview

Claude Opus 5 is Anthropic's flagship general-access model, released on 24 July 2026 as `claude-opus-5`. It is a candidate for the high-capability lane of agentic coding and review, not a default replacement until measured in the target harness. The public launch quotes **US$5/M input** and **US$25/M output**; Fast mode is priced at twice the base rate.^[raw/articles/anthropic-claude-opus-5-2026-07-24.md]

## Integration facts

- Claude Code `v2.1.219` makes Opus 5 the default Opus choice and surfaces a **1M-context** label. The same release adds `sandbox.network.strictAllowlist`, a deny-unless-allowlisted network control for sandboxed commands. This setting constrains command egress; it is not a replacement for repository isolation, credential scoping, or acceptance gates.^[raw/articles/anthropic-claude-opus-5-2026-07-24.md]
- Anthropic offers automatic fallback for requests flagged by its safety classifiers. In Claude Code, Claude.ai, and Cowork, some cyber-related requests can fall back to Opus 4.8 by default; workflows that rely on a fixed model must observe and record fallback behavior.^[raw/articles/anthropic-claude-opus-5-2026-07-24.md]
- Anthropic reports strong coding, computer-use and knowledge-work results, but most launch benchmarks and early-access customer statements are vendor-supplied. Treat them as a basis for trial selection, not proof of performance in a specific repository or agent harness.^[raw/articles/anthropic-claude-opus-5-2026-07-24.md]
- Claude Code `v2.1.224` (7 August 2026) adds `claude self-hosted-runner` for Team/Enterprise web, mobile and desktop sessions, moving checkout and command execution to organization-operated machines or containers. This is a **hybrid execution boundary**, not self-hosted inference: prompts, responses, tool results, transcripts and model inference remain in Anthropic's control plane. A pilot therefore needs ephemeral per-session execution, external default-deny egress, scoped credentials, cloud-metadata blocking and recovery testing before it can be trusted with a private repository.^[raw/articles/anthropic-claude-code-v21224-2026-08-08.md]
- The same release enables `SendMessage`/`ListAgents` across Claude Code sessions on macOS and Linux, but messages are coordination data rather than authority: they cannot approve a permission request or mutate configuration on behalf of a recipient. It also fixes a Linux/macOS sandbox bypass in trailing-slash `denyRead` entries, so existing deny rules using that notation should be audited after upgrade.^[raw/articles/anthropic-claude-code-v21224-2026-08-08.md]

## Controlled-trial guidance

Evaluate it on a fixed set of representative tasks against [[entities/models/gpt-5-6]], [[entities/models/gemini-3-6-flash]] and the newer [[entities/models/claude-fable-5-1]]. Keep model identity, effort level, tool policy, budgets, worktree isolation, tests and reviewer separate from the variable under test. Record verified task success, cost per successful task, latency, tool calls, retry/fallback events, out-of-scope diffs and review findings. Use the task-boundary routing pattern in [[comparisons/model-routing-hermes-opencode-pi]].

## Caveats

- A 1M context window does not make unbounded context reliable or cheap; validate retrieval, compaction and cost at the intended workload size.
- Safety fallback can change the effective model mid-run. Treat it as an auditable execution event, especially in security-oriented tasks.
- The release is extremely recent. Hacker News attention documents interest, not adoption or independent benchmark confirmation.
- A self-hosted runner does not turn a cloud coding session into a contained local agent. The host, environment secret, outbound paths and per-session capability exchange become explicit production security boundaries.

## Sources

- [Anthropic launch announcement](https://www.anthropic.com/news/claude-opus-5)
- [Claude Code v2.1.219 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.219)
- [Claude Code v2.1.224 release](https://github.com/anthropics/claude-code/releases/tag/v2.1.224)
- [Independent v2.1.224 session-message verification](https://dev.classmethod.jp/en/articles/20260807-cc-updates-v2-1-224/)
- [Hacker News discussion](https://news.ycombinator.com/item?id=49038433)
