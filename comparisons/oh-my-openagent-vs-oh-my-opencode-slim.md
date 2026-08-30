---
title: Oh My OpenAgent versus Oh My OpenCode Slim
created: 2026-07-19
updated: 2026-07-19
type: comparison
tags: [comparison, tool, agent, agent-orchestration, workflow, coding]
sources:
  - https://github.com/code-yeongyu/oh-my-openagent
  - https://github.com/code-yeongyu/oh-my-openagent/blob/dev/docs/reference/features.md
  - https://github.com/alvinunreal/oh-my-opencode-slim
  - https://github.com/alvinunreal/oh-my-opencode-slim/blob/master/docs/configuration.md
confidence: high
contested: false
contradictions: []
---

# Oh My OpenAgent versus Oh My OpenCode Slim

## Identity

The original **Oh My OpenCode** project has been renamed **Oh My OpenAgent**. Its npm package and compatibility binary still use `oh-my-opencode`. The standard OpenCode edition is the project's **Ultimate Edition**.

**Oh My OpenCode Slim** is a separate community fork/package, not the original project's official Light Edition. The official Light Edition targets Codex CLI, while Slim remains an OpenCode orchestration plugin.

At the time of this comparison, the inspected package versions were standard `4.19.0` and Slim `2.2.4`; both projects evolve rapidly, so exact counts can drift.

## Main differences

| Dimension | Standard / Oh My OpenAgent Ultimate | Oh My OpenCode Slim |
|---|---|---|
| Philosophy | Batteries-included agent harness and broad compatibility/control layer | Smaller OpenCode-focused orchestration plugin that leans more on native OpenCode primitives |
| Built-in agents | 11: core, planning, orchestration, consultation, exploration and category executor roles | 7 primary roles: Orchestrator, Explorer, Oracle, Council, Librarian, Designer and Fixer; Observer is optional |
| Orchestration | Sisyphus, Prometheus/Metis/Momus planning stack, Atlas execution, category routing and Sisyphus-Junior executors | One central Orchestrator schedules background specialists; Council provides optional multi-model consensus |
| Team coordination | Experimental Team Mode with shared tasks, claims, mailbox, optional worktrees and up to eight members | Native background subagents plus a background job board/reconciliation; no equivalently broad Team Mode is documented |
| Lifecycle/control surface | 54 base hooks, or 61 with Team Mode; 20–39 tools depending on gates | Does not expose a comparable 54-hook control layer; adds focused tools such as patch rescue, AST search, web fetch and background cancellation |
| Workflow commands | Includes `/goal`, `/handoff`, `/start-work`, `/refactor`, `/init-deep`, continuation and recovery features | Emphasizes bundled skills such as deepwork, codemap, verification planning, reflect and worktrees, plus automatic orchestration |
| Editing/context | Hashline edits, aggressive lifecycle hooks, session recovery, hierarchical `AGENTS.md`, Claude Code config compatibility | Native OpenCode editing with conservative `apply_patch` rescue, project-local prompts/config and simpler agent contracts |
| Model routing | Per-agent fallback chains, category-based routing, models.dev capability resolution | Named presets, runtime `/preset`, per-agent models/fallbacks, custom agents, Council presets and external ACP-agent wrappers |
| Extra integrations | OpenCode Ultimate, official Codex Light edition, Claude Code compatibility, OpenClaw integrations | OpenCode only as host, but can call external ACP agents; optional desktop Companion and broad terminal-multiplexer support |
| License | SUL-1.0 | MIT |

## Cost and complexity

Slim usually has a smaller baseline prompt/control surface, but the name does not guarantee lower token cost. Its default background orchestration and optional Council can fan out several model calls. Compare total task cost, retries, cache behavior and review quality rather than counting agents alone.

The standard edition provides more recovery, planning, continuation and coordination behavior out of the box, at the cost of more hooks, implicit behavior, configuration surface and potential overlap with an external workflow orchestrator.

## Caelum implication

For [[coding/architecture/kitdev-deterministic-agentic-workflows|Caelum]], OpenCode should remain an executor adapter rather than the source of workflow authority.

- Prefer plain OpenCode or a tightly restricted Slim configuration when Caelum owns spec, task boundaries, gates, handoffs and review.
- Use the standard edition only when deliberately delegating more planning/orchestration responsibility into OpenCode.
- In either edition, disable or constrain nested delegation for a task contract that requires one bounded executor, and keep completion authority in Caelum's external gates and independent review.

Related: [[comparisons/model-routing-hermes-opencode-pi]] and [[entities/tools/hermes-agent]].
