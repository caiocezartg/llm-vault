---
title: Model Routing Across Hermes, OpenCode, and Pi
created: 2026-07-17
updated: 2026-09-09
type: comparison
tags: [comparison, agent, agent-orchestration, workflow, hermes, tool, openrouter]
sources:
  - https://hermes-agent.nousresearch.com/docs/user-guide/configuring-models
  - https://hermes-agent.nousresearch.com/docs/user-guide/configuration
  - https://hermes-agent.nousresearch.com/docs/user-guide/features/fallback-providers
  - https://hermes-agent.nousresearch.com/docs/integrations/providers
  - https://hermes-agent.nousresearch.com/docs/user-guide/skills/bundled/autonomous-ai-agents/autonomous-ai-agents-opencode
  - https://hermes-agent.nousresearch.com/docs/user-guide/features/kanban-worker-lanes
  - https://opencode.ai/docs/cli/
  - https://opencode.ai/docs/agents/
  - https://opencode.ai/docs/models/
  - https://opencode.ai/docs/server/
  - https://opencode.ai/docs/sdk/
  - https://opencode.ai/docs/plugins/
  - https://opencode.ai/docs/permissions/
  - https://opencode.ai/docs/rules/
  - https://opencode.ai/docs/skills/
  - https://opencode.ai/docs/acp/
  - https://github.com/NousResearch/hermes-agent/issues/413
  - https://github.com/zaycruz/hermes-opencode-plugin
  - https://github.com/anomalyco/opencode/releases/tag/v1.18.3
  - https://github.com/marco-jardim/opencode-model-router
  - https://github.com/yeliu84/pi-model-router
  - https://pi.dev/packages/pi-auto-router
  - https://github.com/openai/codex/releases/tag/rust-v0.147.0
  - raw/articles/agent-plugins-spec-100-2026-08-13.md
  - raw/articles/openrouter-stripe-2026-08-20.md
  - raw/articles/github-hydrafusion-2026-09-04.md
  - https://github.blog/changelog/2026-08-12-agent-plugins-1-0-in-vs-code-copilot-cli-and-the-copilot-app
confidence: high
contested: false
contradictions: []
---

# Model Routing Across Hermes, OpenCode, and Pi

## Question

Which harnesses can route different task types to different providers/models through executable configuration or plugins rather than relying only on Markdown instructions?

## Comparison

| Harness | Built-in executable routing | Dynamic task-aware router | Main limitations |
|---|---|---|---|
| Hermes | Fixed main model; independently configured auxiliary-task slots; one global subagent provider/model override; per-profile and per-cron-job models; fallbacks | No first-class arbitrary task taxonomy router for normal turns or per-`delegate_task` model selection. Use profiles/process dispatch, a routing proxy exposed as an OpenAI-compatible endpoint, or custom executable integration. | `delegation.model/provider` applies to all children. Fallback is failure recovery, not semantic routing. Mid-session model changes reset prompt caches. |
| OpenCode | Each named primary agent or subagent can have a provider/model in `opencode.json`; Task invocation enforces that agent's model | Third-party `opencode-model-router` adds tier routing, modes, fallback and optional enforcement | Built-in automatic agent choice still depends on the orchestrator interpreting descriptions. The third-party router injects routing protocol tokens and should be evaluated rather than trusted from claimed savings alone. |
| Pi | Extensible TypeScript runtime supports executable providers/extensions | `pi-model-router` provides per-turn high/medium/low selection using heuristics, optional classifier, custom rules, budget and fallback. `pi-auto-router` adds capability-, quota-, cost- and failure-aware provider routing. | Third-party executable code must be audited. Per-turn switching can create context/cache/provider consistency costs; routing quality needs workload-specific evaluation. |

## Hermes-specific boundaries

Hermes has useful **model slots**, but not a general built-in semantic router:

- the main conversation uses one model unless explicitly switched;
- auxiliary jobs such as compression, title generation, vision, approval, and web extraction have independent provider/model slots and fallback chains;
- `delegation.provider` plus `delegation.model` move all `delegate_task` children to one alternate pair, but the tool call itself does not select a model per child;
- profiles and Kanban worker lanes can each have their own model, making profile assignment a reliable task-boundary routing mechanism;
- cron jobs can pin a model/provider per job;
- fallback providers activate on provider/model failure and should not be confused with task classification;
- OpenRouter Pareto Code and OpenAI-compatible gateways such as LiteLLM or other routers can be selected as the apparent Hermes model, moving dynamic selection upstream.

Hermes plugin `pre_llm_call` hooks can inject context but cannot override the active model. Model-provider plugins declare inference backends; a truly dynamic router therefore normally lives behind the endpoint or in an explicit dispatcher that launches the selected profile/model.

### OpenRouter ownership change: preserve the exit path

On 19 August 2026, OpenRouter announced an agreement to join Stripe while stating that its integration surface, product and routing mission would continue unchanged. This is a material dependency change for any workflow that uses the gateway as its upstream model router, billing layer or source of model metadata—not evidence that its future neutrality, price, retention or provider policy is guaranteed. ^[raw/articles/openrouter-stripe-2026-08-20.md]

Treat an OpenRouter-backed endpoint as a convenience boundary, not a control-plane authority. Keep direct-provider or alternate-gateway configuration tested; record requested versus effective model/provider; pin any policy that matters for cost, region, data handling or capability; and test quota/outage/failover behavior. [[entities/tools/openrouter]] provides the event record and evidence boundary.

## Recommended design principle

Prefer **routing at typed task boundaries** over swapping the parent model every turn:

1. Keep a stable medium-capability orchestrator to preserve prompt caching and context continuity.
2. Assign cheap models to deterministic auxiliary slots first.
3. Route bounded worker tasks using structured metadata such as `task_type`, `risk`, `write_scope`, `required_capabilities`, and `acceptance_gate`.
4. Escalate only after executable failure evidence or a declared high-risk task class.
5. Measure actual total cost, latency, pass rate, retries, cache misses, and duplicated context; do not infer savings from per-token prices alone.

This complements [[coding/architecture/kitdev-deterministic-agentic-workflows]]: the router chooses a worker lane, while executable gates—not the router or model—decide completion. Hermes details live in [[entities/tools/hermes-agent]].

### GitHub Copilot HydraFusion: vendor-managed compound routing

GitHub's 4 September 2026 **HydraFusion** preview is a concrete hosted implementation of per-turn compound routing: it can select a single model, a cheap-first cascade with a quality gate, or a cross-family read-only critique followed by one revision. The useful implementation boundaries are complete accounting of every leg, explicit timeout/cancellation, tool-less review isolation, no patch on failed validation, and preflight validation of model bindings. ^[raw/articles/github-hydrafusion-2026-09-04.md]

It is a trial reference, not a portable control plane: the curated model roster is not selectable or fixed, intermediate drafts are withheld, pricing aggregates underlying-model token use, and the preview is currently scoped to first-turn single-prompt tasks. GitHub's own results trade quality for cost on two of three reported benchmarks, so do not generalize its 67% TerminalBench saving to repository work. Preserve requested/effective model receipts, role-level cost/latency, explicit human intervention, isolated review, and repository-native acceptance gates. Compare against [[coding/architecture/merge-gated-dag-coding-workflow]] and [[entities/tools/hermes-agent]].

## Hermes delegating implementation to OpenCode

Hermes' bundled OpenCode integration is primarily a **procedural process adapter**, not an in-process SDK and not a native `delegate_task` backend. The bundled skill teaches Hermes to start `opencode run` through terminal/process tools, select `--model` and `--agent`, attach context files, parse or observe output, resume sessions when useful, and isolate parallel work in separate workdirs/worktrees.

The integration surface is layered:

| Layer | Durable interpretation | Adoption stance |
|---|---|---|
| Process / CLI | Hermes can launch one bounded OpenCode run and collect stdout/JSON events. | Official and sufficient for the first worker-per-task experiments. |
| Handoff protocol | `AGENTS.md`, Agent Skills, task packets, file attachments and acceptance criteria share context across harnesses. | Prefer this portable layer first; Markdown guides behavior but does not enforce ownership or gates. |
| Structured output | `opencode run --format json`, session id, diff and logs can become receipts. | Treat as evidence to normalize, not as a completion verdict. |
| Server / SDK / SSE | OpenCode exposes programmatic sessions, async prompts, abort, status, diff and events. | Useful after a measured observability/cancellation bottleneck; adds auth, versioning and event-recovery work. |
| Plugins | OpenCode plugins are official and privileged; Hermes OpenCode plugins are third-party integration code. | Audit, pin and sandbox before use; never make plugin output the authority. |
| Kanban / worker lanes | Hermes Kanban can dispatch profile workers; direct external OpenCode lane is pluggable but not paved. | Use a narrow Hermes `opencode-worker` profile only after process-level validation shows need for durable queue/retry. |

### Role, process and model are separate axes

A logical role such as planner, implementer, reviewer or gate runner should not be conflated with an OS process or a model choice. Hermes can remain the planner/orchestrator while OpenCode is one implementation process. OpenCode can also have internal agents such as `build`, `plan`, `explore` or `scout`, each with model, step and permission settings, but those are **worker lanes**, not a second sovereign program planner.

The recommended split is:

- Hermes owns decomposition, task-packet validation, lane selection, budget, retry policy and user-facing synthesis.
- OpenCode implements or explores one bounded packet in the selected worktree/session.
- Deterministic scripts or CI own final gates, diff-scope checks, secret/dependency scans and exit-code evidence.
- A human or read-only reviewer lane is required for high-risk changes; the implementing model never approves itself.

This complements [[coding/architecture/kitdev-deterministic-agentic-workflows]]: the router chooses a lane, but executable gates and protected integration decide completion.

### Skills-first architecture now recommended

For Caio's Hermes-centered setup, the durable recommendation is **skills-first before runtime-first**:

1. Keep shared development rules in short `AGENTS.md` files plus portable Agent Skills usable by Hermes, OpenCode and other compatible harnesses.
2. Have Hermes materialize a typed task packet with objective, non-goals, `base_ref`, write scope, forbidden paths, lane/model class, acceptance criteria, gates, timeout and retry budget.
3. Run one fresh OpenCode session per ticket/attempt in an isolated worktree; resume a session only for a follow-up on the same packet, base and worktree.
4. Pass only relevant files or skill references; do not dump the full Hermes transcript, memory or global plan into the worker.
5. Collect JSON events, diff hash, session id, OpenCode version, gate commands and exit codes as receipts; classify the run as `passed`, `failed`, `blocked` or `timeout` from those receipts.

### Codex v0.147: portability is not authority

Codex `v0.147.0` (7 August 2026) adds portable Agent Plugin installation and search across local, personal, workspace, and remote catalogs; it can import Cursor-managed skills and synchronize imported Claude/Cursor conversation changes without duplicates. This strengthens the **distribution and discovery** layer for shared skills, but does not make a skill, plugin catalog, or synchronized transcript a trusted control-plane input. Treat imported content as untrusted until it passes the same repository policy, review, pinning, and scope checks as locally authored automation.

The release also removes `codex exec --full-auto` in favor of explicit sandbox configuration, adds `--approve-for-me`, and hardens project trust, credential restrictions, plugin isolation, and network-fail-closed behavior. The durable implication is not to automate approval more broadly: an automatically reviewed approval remains a convenience layer beneath OS/network sandboxing, scoped credentials, typed task packets, and independent executable gates. [[coding/architecture/merge-gated-dag-coding-workflow]] remains the authority model; [[entities/tools/hermes-agent]] remains the orchestrator boundary.

### Agent Plugins 1.0: portable packaging, bounded promise

Agent Plugins Specification `1.0.0` is now available in VS Code, Copilot CLI, the Copilot app and Copilot SDK, while Codex had already added plugin catalog support in `v0.147.0`. Its portable core is deliberately narrow: a `plugin.json` plus optional Agent Skills in `skills/` and MCP server configuration in `mcp.json`; hooks, agents, commands, UI and other client-specific features remain in reverse-domain extensions or compatibility packages. ^[raw/articles/agent-plugins-spec-100-2026-08-13.md]

For a cross-harness workflow this is a useful **distribution** format, not a portable authority or execution model. The specification requires package-relative paths to remain inside the resolved plugin root, but explicitly does not sandbox a plugin subprocess or constrain runtime-supplied paths. Therefore validate/pin/vet a plugin's source and its MCP server configuration, apply host/network/credential policy outside the package, and test each target client independently. The external format is additive: OpenCode has an assigned feature request rather than shipped first-class support as of 2026-08-13. [[concepts/model-context-protocol]] still governs tool protocol semantics; [[entities/tools/hermes-agent]] and repository gates retain control-plane authority.

OpenCode must execute where the worktree exists. In the intended VPS-brain/local-Windows-sandbox topology, the bridge must require an explicitly configured and preflighted workspace root; no Windows path should be assumed. Docker/sandbox policy, not model cooperation, should deny `.env`, secrets, external directories, global installs, arbitrary shell access and unapproved egress.

### Task packet, worktree and gates are the real boundary

The reusable contract is a small, versioned packet plus independent gate runner:

- packet schema validation fails before launch if `base_ref`, write scope, gates, timeout or workspace selector are missing;
- one writer owns one worktree/branch; overlapping paths, migrations and shared test fixtures are serialized;
- OpenCode permissions and container mounts should mirror the declared scope instead of relying on `--auto`;
- gate sequence includes packet schema, git diff/scope, formatter/linter, focused tests, integration tests when relevant, secret/dependency scans, and human review for auth/migrations/deploy-sensitive changes;
- promotion decisions measure pass rate, retries, latency, total cost, cache misses, diff size, operational failures and gate evidence, not narrative quality.

### Third-party `zaycruz/hermes-opencode-plugin` maturity

The `zaycruz/hermes-opencode-plugin` repository is useful as an adapter prototype, not as a P0 dependency. In the 2026-07-18 report, it had four commits, no published releases/tags, last push on 2026-06-08, and OpenCode had already released v1.18.3 on 2026-07-16. Its code path reportedly constructs argv rather than `shell=True`, runs `opencode run --format json`, sets timeouts and can start `opencode serve` for sessions, but it remains a synchronous third-party Hermes plugin with inherited environment, limited preflight, no demonstrated VPS-to-Windows/Docker coverage, and no replacement for ledger/gates.

Adoption criterion: audit a pinned commit, inventory environment/egress/permissions, run the declared smoke tests plus a local fixture against the pinned OpenCode version, and keep rollback trivial. Until then, use the official procedural skill or a minimal deterministic bridge.

### Limit of Hermes issue #413

Hermes issue #413 is durable evidence of the historical problem statement: mixed CLI-agent orchestration requires backend abstraction, PTY/headless handling, parsing, lifecycle, handoff and DAG semantics. Its closed/completed status should **not** be read as a contracted API proving that OpenCode is now a native generic `delegate_task` backend. The current durable reading is narrower: Hermes supports procedural OpenCode delegation and pluggable worker-lane patterns, while a direct external OpenCode lane still requires integration design.

### Promotion criteria: process skill → Kanban/ledger → SDK/server

Promotion should be evidence-based:

| Stage | Use when | Promote only when |
|---|---|---|
| Process skill / minimal bridge | First fixture, one task at a time, low concurrency. | Multiple recorded fixture attempts expose real queue/retry/restart needs or recurring operational failures. |
| Hermes Kanban or SQLite ledger plus `opencode-worker` profile | More than one ticket, crash recovery, human handoff, leases, retries or durable audit are needed. | CLI startup/parsing or lack of real-time control becomes a measured bottleneck, or cancellation/progress/fan-out requirements are concrete. |
| OpenCode server/SDK/SSE bridge | Need session abort, status polling, event telemetry, warm server or richer UI. | Compatibility tests pass repeatedly against a pinned OpenCode version and event loss/duplication cannot corrupt the ledger. |

Do not adopt MCP, OpenCode server, Kanban, direct external `spawn_fn`, OMO/team plugins or third-party Hermes plugins by default. Each adds lifecycle, auth, versioning and state-management surface that is only justified after the simpler task-packet/worktree/gate architecture produces measured bottlenecks.

## Practical implication for Caio's setup

For a Hermes-centered architecture, the current starting point is a small executable dispatcher or restricted SSH/Tailscale bridge over typed task packets, portable skills, isolated worktrees, OpenCode `run --format json`, and deterministic gates. Pi remains the closest ready-made environment for experimenting with true per-turn router extensions. OpenCode offers strong built-in role-to-model mapping inside the worker. A general per-turn router, Kanban bridge, or SDK/server integration should be added only after profile/task-boundary routing and the process bridge show a measured gap.

Orca upstream discussion now independently validates this boundary. Its open requests cover per-worktree model/effort choice ([#8029](https://github.com/stablyai/orca/issues/8029)), task-specific OpenCode model choice ([#1122](https://github.com/stablyai/orca/issues/1122)), named built-in-agent launch profiles ([PR #5728](https://github.com/stablyai/orca/pull/5728)), verified harness × model × effort inventory ([#10846](https://github.com/stablyai/orca/issues/10846)) and deterministic workflow dispatch instead of shell scripts or probabilistic LLM routing ([#11229](https://github.com/stablyai/orca/issues/11229)). Until those capabilities land in a stable release, an explicit Hermes-to-Orca adapter can be cost-aware but should not be described as Orca-native automatic routing.

The full local report `/home/caiocezartg/reports/hermes-opencode-integration-patterns-2026-07-18.md` contains the detailed source matrix and phased backlog; this page preserves only the durable integration pattern and adoption criteria. Related Hermes runtime details live in [[entities/tools/hermes-agent]].
