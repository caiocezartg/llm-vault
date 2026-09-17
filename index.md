# Wiki Index

> Global Hermes LLM Wiki / Obsidian vault. Read this first to find relevant pages for any query.
> Last updated: 2026-09-17 | Total pages: 37

## Concepts

- [[concepts/global-llm-wiki]] — The purpose and operating model of the global LLM Wiki as a cross-profile knowledge layer.
- [[concepts/github-actions-cache-capability-modes]] — Explicit, cache-service-enforced `read`/`write`/`write-only`/`none` authority for GitHub Actions workflows.
- [[concepts/model-context-protocol]] — MCP 2026-07-28: stateless transport, migration boundary, and scoped implications for future integrations.
- [[concepts/production-llm-serving-memory-integrity]] — Production-serving protocol: phase-aware FP8/INT4 evaluation and shared-KV integrity boundaries.

## Entities

### Models

- [[entities/models/bonsai-27b]] — Low-bit Qwen3.6-27B derivatives for bounded local inference; benchmark and long-horizon coding caveats included.
- [[entities/models/claude-fable-5-1]] — Anthropic's Fable 5.1: API migration, retention, cost-evidence and controlled-trial boundaries for long-running coding/research tasks.
- [[entities/models/claude-opus-5]] — Anthropic flagship model for high-capability coding/review trials; model/fallback behavior and controlled-evaluation guidance.
- [[entities/models/deepseek-v4-1-flash]] — MIT-licensed open-weight V4.1 Flash: API-reroute boundary, efficiency claims, and controlled coding/agent trial protocol.
- [[entities/models/gemini-3-6-flash]] — Gemini Flash 3.6/3.7/3.8 for agentic/coding trials; migration, availability, cost-per-task and controlled-evaluation boundaries.
- [[entities/models/glm-5-3]] — Z.ai’s GLM-5.3 family: post-trained coding/agent model plus the open-weight GLM-5.3-Flash variant; vendor-benchmark caveats and controlled-trial boundary.
- [[entities/models/gpt-5-6]] — GPT-5.6 family: current availability, evaluation evidence, reliability caveats, and controlled adoption guidance.
- [[entities/models/gpt-6-astra]] — OpenAI’s GPT-6 Astra: release, independent evaluation boundary, costs and controlled routing-trial guidance.
- [[entities/models/kimi-k3]] — Kimi K3: API-available 2.8T model; integration requirements, first-party benchmark caveats, and controlled-trial guidance.
- [[entities/models/lfm25-26b]] — Open-weight 2.69B model for bounded local tool loops; its own model card excludes agentic coding and requires controlled evaluation.
- [[entities/models/muse-glimmer]] — Meta's Apache-2.0 30B local-agent model; vendor performance claims remain bounded by controlled evaluation.
- [[entities/models/qwen3-8-max]] — Qwen’s 2.4T/95B-active flagship: API trial candidate with promised open weights; retain vendor-evidence and controlled-evaluation boundaries.
- [[entities/models/tencent-hy4]] — Tencent’s Apache-2.0 770B-total/49B-active MoE preview; a controlled long-context coding/agent trial candidate, not a default route.

### Tools

- [[entities/tools/astro-triagebot-action]] — Skills-backed GitHub Action for staged issue triage; OpenAI provider support and pilot-boundary guidance.
- [[entities/tools/cloudflare-os]] — Apache-2.0 agent workspace/control-plane candidate; evaluate authorization inheritance and containment through a controlled pilot, not vendor claims.
- [[entities/tools/cloudflare-security-audit-skill]] — Multi-phase agentic security-audit skill with adversarial validation and structured evidence; controlled-trial guidance included.
- [[entities/tools/hermes-agent]] — Hermes Agent as the multi-profile agent runtime using skills, tools, cron, memory, and session search.
- [[entities/tools/mindwalk]] — Local, open-source visual replay and inspection of coding-agent sessions; useful for trajectory diagnosis, not as an outcome oracle.
- [[entities/tools/onecli]] — Open-source credential gateway for agents: network-side injection and policy enforcement; test the full injection surface and fail-closed approval paths before any production use.
- [[entities/tools/openai-agents-api]] — Public-beta managed Codex harness; environment and external-acceptance control boundaries remain with the engineering team.
- [[entities/tools/openrouter]] — Model gateway/marketplace now joining Stripe; retain tested exit paths and treat continuity/neutrality as commitments to monitor.
- [[entities/tools/orca]] — Worktree-native multi-agent ADE and coordination runtime; use discovery/spec skills upstream and retain executable gates plus independent acceptance.
- [[entities/tools/qm]] — Y Combinator's open-source multi-agent organizational harness; retain scoped-isolation and production-effectiveness caveats pending a controlled trial.
- [[entities/tools/vulnhunter]] — Capital One's open-source agentic code-security suite: attacker-first tracing, falsification, remediation, and independent verification; require controlled evaluation before CI adoption.

### Companies

### Frameworks

### Projects

## Comparisons

- [[comparisons/loop-engineering-vs-graph-engineering]] — Comparison of loop-based agent execution and explicit graph/workflow orchestration, including benefits, limits and hybrid use.
- [[comparisons/model-routing-hermes-opencode-pi]] — Executable model-routing capabilities, limitations, and recommended task-boundary strategy across Hermes, OpenCode, and Pi.
- [[comparisons/oh-my-openagent-vs-oh-my-opencode-slim]] — Standard Oh My OpenAgent/Oh My OpenCode versus the separate Slim fork: orchestration depth, agents, hooks, workflow surface, integrations, cost, and Caelum fit.

## Decisions

- [[decisions/use-polaris-for-global-llm-wiki]] — Decision to create Polaris as the dedicated profile for maintaining the global LLM Wiki.

## Coding

### Patterns
### Debugging
### Architecture

- [[coding/architecture/kitdev-deterministic-agentic-workflows]] — Archived exploration of the discarded Caelum concept; retained only as historical research, not an active direction.
- [[coding/architecture/merge-gated-dag-coding-workflow]] — Generic control-plane architecture for dependency-DAG coding waves, isolated worktrees, deterministic dispatch, SHA-bound review, executable gates and post-merge observation.
- [[coding/architecture/project-memory-and-multi-model-handoff-layers]] — Layered project state, task handoffs and durable knowledge boundaries for multi-model coding workflows.

### Runbooks

- [[coding/runbooks/orca-graph-workflow-execution]] — Operational runbook for executing the Orca graph-based coding workflow with task manifests, deterministic eligibility, worktrees, gates, review and merge.

## Projects

- [[projects/hermes-research-daily-radar]] — Selective daily software/AI radar using Hermes-native discovery plus Agent Reach for candidate expansion without increasing final report volume.

## Queries
