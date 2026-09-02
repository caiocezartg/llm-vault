# Wiki Log

> Chronological record of all wiki actions. Append-only.
> Format: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete

## [2026-07-09] create | Global LLM Wiki initialized
- Created global Obsidian-compatible LLM Wiki at `/home/caiocezartg/llm-wiki`.
- Created schema, index, and initial seed pages.
- Created Polaris profile as semantic archivist / wiki curator.
- Initial domain: global Hermes knowledge layer for research, coding, architecture, model/tool evaluation, decisions, and reusable workflows.

Files created:
- `SCHEMA.md`
- `index.md`
- `log.md`
- `concepts/global-llm-wiki.md`
- `entities/tools/hermes-agent.md`
- `decisions/use-polaris-for-global-llm-wiki.md`

## [2026-07-11] create | deterministic KitDev agentic workflows
- Added `coding/architecture/kitdev-deterministic-agentic-workflows.md` from primary-source research on SDD, worktrees, gates, durable task coordination, least privilege, trackers and multi-harness adapters.
- Added its architecture entry to `index.md`.

## [2026-07-12] create | GPT-5.6 evaluation and adoption guidance
- Added `entities/models/gpt-5-6.md` with GA/availability facts, benchmark context, METR evaluation caveat, and controlled trial guidance.
- Updated `index.md` with the model entry and corrected the page count.

## [2026-07-13] update | deterministic KitDev agentic workflows
- Updated `coding/architecture/kitdev-deterministic-agentic-workflows.md` with durable evidence on benchmark-quality risk, early trajectory validation, selective persistent memory, and multi-model governance.

## [2026-07-14] create | Hermes research Daily Radar Agent Reach hybrid
- Added `projects/hermes-research-daily-radar.md` with the durable architecture decision for the research profile's hybrid Hermes-native + Agent Reach v1.5.0 discovery workflow.
- Updated `entities/tools/hermes-agent.md` with a backlink to the radar project.
- Updated `index.md` with the project entry and page count.

## [2026-07-14] create | Mindwalk
- Added `raw/articles/mindwalk-v010-2026-07-14.md`, preserving the primary release record and independent HN attention signal.
- Added `entities/tools/mindwalk.md` with controlled-trial guidance: use trajectory visualization for diagnosis, but retain repository-native tests and acceptance evidence as the outcome oracle.
- Updated `index.md` with the tool entry and page count.

## [2026-07-15] ingest | Bonsai 27B
- Added `raw/articles/prismml-bonsai-27b-2026-07-15.md`, preserving the primary PrismML announcement with immutable-body checksum.
- Added `entities/models/bonsai-27b.md` with local-inference relevance, model-card limitation for long-horizon agentic coding, and controlled-trial guidance.
- Updated `index.md` with the model entry and page count.

## [2026-07-16] update | skills-first Asteria / KitDev starting point
- Updated `coding/architecture/kitdev-deterministic-agentic-workflows.md` with the decision to validate a small skills-first workflow before implementing the full control plane.
- Recorded provisional name `Asteria`, role/model routing, adapted Matt Pocock skill boundaries, durable task handoffs, and the active implementation handoff path.
- Active handoff: `/home/caiocezartg/reports/asteria-skills-first-implementation-handoff.md`.

## [2026-07-16] update | GPT-5.6 robustness evidence
- Updated `entities/models/gpt-5-6.md` with the GPT-Red announcement, its first-party evaluation limitation, and the durable implication that model robustness complements—not replaces—isolated execution, tool authorization, egress limits, untrusted-content boundaries, and adversarial regression tests.
- The source was not added as a raw capture because its primary announcement remains directly linked in the entity page; no standalone GPT-Red page was created because the system is internal-only and currently serves as evidence about the GPT-5.6 safety posture rather than an independently adoptable entity.

## [2026-07-16] update | Caelum final name and local Codex implementation brief
- Finalized **Caelum** as the name of the skills-first agentic development workflow formerly discussed as KitDev/Asteria.
- Updated the architecture page and index summary to use the final name.
- Added active architecture handoff `/home/caiocezartg/reports/caelum-skills-first-implementation-handoff.md` and self-contained local Codex build brief `/home/caiocezartg/reports/caelum-codex-local-bootstrap-implementation.md`.

## [2026-07-16] update | Caelum corrected to cross-harness SDD skill pack
- Corrected the initial product direction: Caelum begins as portable Agent Skills-standard SDD skills installable into harness-native directories, not as a fixture, project scaffold, Kanban, or runtime.
- Recorded `npx skills@latest add <source>` as the preferred cross-harness distribution path; the existing ecosystem already supports Codex, Hermes Agent, OpenCode, Pi, Claude Code, and many others.
- Marked the starter/fixture implementation briefs as superseded experiments rather than active product briefs.

## [2026-07-17] ingest | Cloudflare security-audit skill
- Added `raw/articles/cloudflare-vulnerability-harness-2026-07-17.md` with an immutable excerpt and body checksum from the primary Cloudflare architecture article.
- Added `entities/tools/cloudflare-security-audit-skill.md` with the durable workflow pattern: separate discovery and adversarial validation, require structured/source-grounded evidence, and scale the control plane only after a measured bottleneck.
- Updated `index.md` with the tool entry and page count.

## [2026-07-17] create | Model routing across Hermes, OpenCode, and Pi
- Added `comparisons/model-routing-hermes-opencode-pi.md` with the verified distinction between fixed model slots, fallback, role/profile routing, and executable task-aware router extensions.
- Recorded the task-boundary recommendation: stable orchestrator, typed worker lanes, deterministic escalation, and measurement of total cost including cache/context overhead.
- Updated `entities/tools/hermes-agent.md` with a backlink and updated `index.md` with the comparison entry and page count.

## [2026-07-17] update | Hermes-to-OpenCode task delegation
- Expanded `comparisons/model-routing-hermes-opencode-pi.md` with the verified bundled integration shape: Hermes invokes OpenCode through terminal/process CLI orchestration rather than an in-process SDK or native `delegate_task` backend.
- Recorded the recommended spec-driven boundary: typed task packet, pre-launch model selection, isolated worktree/session, JSON event collection, and independent Hermes gates.
- Noted that the official Kanban external-CLI lane is pluggable but not yet paved, and that the third-party Hermes OpenCode plugin must be separately audited and trialed.

## [2026-07-17] update | Kanban bridge profile for OpenCode
- Added the minimal bridge pattern to `comparisons/model-routing-hermes-opencode-pi.md`: native Kanban dispatches a lightweight Hermes `opencode-worker` profile, which invokes one bounded OpenCode run and closes the task through native Kanban lifecycle tools.
- Recorded the trade-off: one extra cheap Hermes wrapper call in exchange for retaining claims, retries, runtime limits, logs, completion/block semantics, and avoiding a custom external `spawn_fn` during initial validation.
- Added the remote-path constraint for the intended VPS-brain/Windows-sandbox topology: OpenCode must execute where the worktree exists, under the allowed `C:/AgentWorkspace` mapping.

## [2026-07-17] update | Linear agent surface with local execution ledger
- Updated `coding/architecture/kitdev-deterministic-agentic-workflows.md` with Linear's current Agent Session, Agent Activity, prompt-context, webhook, and visible lifecycle primitives.
- Recorded the recommended hybrid boundary: Linear owns human-facing issue/spec/delegation/progress presentation while a small local structured ledger owns claims, attempts, worktrees, worker sessions, retries, gates, and final execution verdicts.
- Added webhook constraints: fast acknowledgement and asynchronous enqueue, signed delivery verification, replay protection, and idempotent deduplication by delivery/session/issue identifiers.

## [2026-07-17] update | Correct unknown Windows workspace path
- Corrected `comparisons/model-routing-hermes-opencode-pi.md`: the previously assumed `C:/AgentWorkspace` path does not exist on the user's local machine.
- The Windows sandbox workspace path is currently unspecified and must not be guessed; remote worker adapters should use the user-provided path only after validation.

## [2026-07-18] ingest | VulnHunter
- Added `raw/articles/capitalone-vulnhunter-2026-07-18.md` with an immutable primary-source excerpt, captured independent signals, and body checksum.
- Added `entities/tools/vulnhunter.md` with reusable guardrails: attacker-first analysis, self-falsification, evidence/reproducer gates, independent repair verification, and corpus-based trials before CI integration.
- Updated `entities/tools/cloudflare-security-audit-skill.md` with a cross-reference to the related, but independently unevaluated, Capital One suite.
- Updated `index.md` with the new tool entry and page count.

## [2026-07-18] update | Hermes–OpenCode integration patterns
- Curated durable takeaways from `/home/caiocezartg/reports/hermes-opencode-integration-patterns-2026-07-18.md` into `comparisons/model-routing-hermes-opencode-pi.md` instead of creating a new page.
- Added the layered integration map, role/process/model distinction, skills-first task-packet/worktree/gate boundary, `zaycruz` plugin maturity assessment, issue #413 limitation, and criteria for promoting from process bridge to Kanban/ledger or OpenCode SDK/server.
- Did not update `index.md` because no page was created or renamed.

## [2026-07-19] create | Oh My OpenAgent versus Oh My OpenCode Slim
- Added `comparisons/oh-my-openagent-vs-oh-my-opencode-slim.md` from current primary repository documentation.
- Distinguished the renamed original project and its official Codex Light edition from the separate Slim OpenCode fork.
- Compared agent topology, hooks/tools, workflow commands, model routing, integrations, licensing, cost caveats, and fit as a Caelum executor adapter.
- Updated `index.md` with the comparison entry and page count.

## [2026-07-19] ingest | Kimi K3
- Added `raw/articles/moonshot-kimi-k3-2026-07-19.md` as an immutable capture of Moonshot's primary announcement and API documentation.
- Added `entities/models/kimi-k3.md` with interface facts, vendor-stated limits, harness-comparison caveats, and a controlled evaluation boundary.
- Updated `index.md` with the model entry and page count.

## [2026-07-19] update | Matt Pocock handoff boundary for Caelum
- Updated `coding/architecture/kitdev-deterministic-agentic-workflows.md` from the current primary `/handoff` skill and AI Hero documentation.
- Distinguished lightweight conversation compaction from Caelum's prospective durable SDD task handoff.
- Recorded the minimal adaptation boundary: retain references-not-copies and secret redaction, then add task modes, Git/evidence fields and resume validation only when pilot evidence requires them.

## [2026-07-20] update | Public LLM Wiki usage patterns
- Curated durable findings from `/home/caiocezartg/reports/llm-wiki-usage-patterns-2026-07-19.md` into `concepts/global-llm-wiki.md`.
- Recorded the recurring source/wiki/schema/index/log pattern, observed deployment scopes, software artifact authority boundaries, evidence limitations, and minimal rollout guidance.
- Did not create a new wiki page or update `index.md`; the full 450-line source report remains outside the vault.

## [2026-07-22] update | Model-evaluation containment after OpenAI/Hugging Face incident
- Updated `entities/models/gpt-5-6.md` with the dual disclosure, its preliminary-evidence boundary, and the distinction between a benchmark-directed incident and a general deployment claim.
- Updated `coding/architecture/kitdev-deterministic-agentic-workflows.md` with durable evaluation-containment controls: deny-by-default egress, segmented proxies/caches, ephemeral credentials, separated trust domains, and boundary-violation stopping.
- Did not update `index.md`; no page was created, renamed, or archived.

## [2026-07-22] update | Caelum concept discarded
- Marked `coding/architecture/kitdev-deterministic-agentic-workflows.md` as an archived historical exploration after Caio explicitly discarded Caelum.
- Updated `index.md` to make clear it is not an active direction and must not frame future project proposals.

## [2026-07-23] update | GPT-5.6 routing for Codex Plus
- Updated `entities/models/gpt-5-6.md` with a practical Sol/Terra/Luna routing policy for the USD 20/month ChatGPT Plus Codex allowance.
- Added current five-hour usage ranges, reasoning-mode guidance, the subscription-versus-API distinction, and explicit roles for older GPT-5.5/5.4 options.
- Did not update `index.md`; no page was created, renamed, or archived.

## [2026-07-23] ingest | Gemini 3.6 Flash
- Captured Google’s primary announcement in `raw/articles/google-gemini-3-6-flash-2026-07-23.md` with source hash.
- Added `entities/models/gemini-3-6-flash.md` with documented availability, vendor-evidence boundary, observed discussion signal, and controlled-evaluation guidance.
- Updated `index.md` with the model entry and page count.

## [2026-07-24] create | OneCLI
- Added `entities/tools/onecli.md` from the public repository, the 23 July host-enforcement-bypass fix, and the current Hacker News technical discussion.
- Recorded the durable agent-security pattern: secret injection and policy enforcement outside the agent process, plus the required `enforcement ⊇ injection` test and the limitation that allowed operations still require service-side least privilege, sandboxing, egress control, and human approval where appropriate.
- Updated `index.md` with the tool entry and page count.

## [2026-07-25] ingest | Claude Opus 5
- Added `raw/articles/anthropic-claude-opus-5-2026-07-24.md` with an immutable primary-source excerpt and body checksum.
- Added `entities/models/claude-opus-5.md` with API/pricing facts, Claude Code integration, fallback and strict-network-allowlist implications, and controlled-trial guidance.
- Updated `index.md` with the model entry and page count.

## [2026-07-25] create | Merge-gated DAG coding workflow
- Added `coding/architecture/merge-gated-dag-coding-workflow.md` from Gabriel Packer's concrete wave-based workflow and prior durable SDD/control-plane findings.
- Recorded role separation, authority boundaries, deterministic eligibility, conflict-aware scheduling, SHA-bound gates/reviews, post-merge observation and a minimal control-plane-first rollout.
- Updated `index.md` with the architecture entry and page count.

## [2026-07-26] create | Orca
- Added `entities/tools/orca.md` from the current public repository and official docs.
- Recorded the durable boundary: discovery/spec skills produce reviewed intent and task inputs; Orca owns worktrees, terminals, task/dispatch lifecycle and coordination, while executable gates plus independent review retain engineering acceptance.
- Added the Orca entry to `index.md`, updated the page count and linked it from the merge-gated DAG architecture page.

## [2026-07-28] update | Kimi K3 open-weight release
- Updated `entities/models/kimi-k3.md` after Moonshot published the official Kimi K3 weights, technical report and license on 27 July.
- Recorded the architecture facts, the transition from API-only trial candidate to self-hosting/provider-portability evaluation candidate, the source-reported benchmark limits, and the retained requirement for constrained harnesses and independent gates.
- Added links to the official Hugging Face card, official report repository and the independent Hacker News release discussion.

## [2026-07-29] ingest | Model Context Protocol 2026-07-28
- Added `raw/articles/mcp-spec-2026-07-28.md` as an immutable primary-source excerpt with a body checksum.
- Added `concepts/model-context-protocol.md` with the stateless transport migration boundary, header routing, MRTR, cache, authorization and deprecation implications.
- Updated `entities/tools/hermes-agent.md` with a scoped backlink: the research profile remains intentionally non-MCP for Agent Reach.
- Updated `index.md` and page count.

## [2026-07-29] update | Orca model-aware task routing boundary
- Updated `entities/tools/orca.md` from current upstream issues and PRs covering per-worktree model/effort selection, task-specific OpenCode choice, named launch profiles, stable-UI/documentation desynchronization, verified model inventory and deterministic workflow dispatch.
- Updated `comparisons/model-routing-hermes-opencode-pi.md` to distinguish a cost-aware Hermes-to-Orca adapter from Orca-native automatic routing.
- Recorded the interim optimization rule: deterministic policy first, reuse Sol's existing planning pass for ambiguous classification, verify the launched model and escalate only from risk or executable evidence.

## [2026-07-30] update | Model-evaluation containment forensic evidence
- Updated `entities/models/gpt-5-6.md` with Hugging Face’s detailed incident reconstruction and OpenAI’s 27–29 July update.
- Recorded the durable refinement: permitted package caches, disposable execution services, cloud metadata, ambient credentials and internal networking can bridge a nominally isolated evaluation; require separate patch/monitoring boundaries and complete action telemetry.
- Preserved the evidence boundary: final third-party and vendor reports remain pending.

## [2026-07-31] update | Worktree trust boundary for coding agents
- Updated `coding/architecture/merge-gated-dag-coding-workflow.md` from official Git documentation plus a reproducible technical analysis of linked worktree shared state.
- Clarified that a linked worktree separates checkout/index/HEAD but shares common Git state; it is not a process, credential, or host-execution isolation boundary.
- Added checkout selection by trust boundary: supervised workers may use linked worktrees; unattended or untrusted workers require external sandboxing and isolated clones, with explicit lifecycle caveats for `git clone --shared`.

## [2026-08-02] ingest | QM v0.1.4
- Added `raw/articles/yc-qm-v014-2026-08-02.md`, preserving the primary GitHub release/repository record with immutable-body checksum.
- Added `entities/tools/qm.md` with the organization-scoped multi-agent/harness-routing architecture, policy boundary, open security/effectiveness questions, and a controlled-pilot recommendation.
- Updated `index.md` with the QM entry and page count.

## [2026-08-03] ingest | Qwen3.8-Max
- Added `raw/articles/qwen-qwen3-8-max-2026-08-03.md`, preserving the official release claims, API/interface facts and the contemporary Hacker News attention signal with an immutable-body checksum.
- Added `entities/models/qwen3-8-max.md` with a controlled API-trial boundary, the evidence distinction between the artifact and vendor autonomy claims, and conditions for reassessing self-hosting after weights/license/serving details publish.
- Updated `index.md` with the model entry and page count.

## [2026-08-04] ingest | production LLM serving: memory optimization and cache integrity
- Added `raw/articles/cloudflare-smaller-faster-safer-2026-08-03.md`, preserving a primary-source excerpt and immutable body checksum from Cloudflare's production serving report.
- Added `concepts/production-llm-serving-memory-integrity.md` with the reusable phase-aware serving protocol: evaluate FP8 KV/INT4 weights by model and workload, separately measure prefill and decode, and retain fail-closed cache-mapping integrity controls for shared infrastructure.
- Recorded vLLM's independent counterexamples so Cloudflare deployment results do not harden into a generic accuracy or security claim.
- Updated `index.md` with the concept entry and page count.

## [2026-08-05] ingest | LFM2.5-2.6B
- Added `raw/articles/liquid-lfm25-26b-2026-08-04.md` as an immutable primary-source excerpt with body checksum.
- Added `entities/models/lfm25-26b.md` with its local tool-loop fit, explicit agentic-coding limitation, evidence boundary and controlled-trial protocol.
- Updated `index.md` with the model entry and page count.

## [2026-08-06] ingest | Cloudflare OS
- Added `raw/articles/cloudflare-os-2026-08-06.md`, preserving a bounded primary-source excerpt and immutable body checksum.
- Added `entities/tools/cloudflare-os.md` with the agent-workspace/control-plane architecture, authorization-inheritance boundary, and controlled-pilot evaluation criteria.
- Updated `index.md` with the Cloudflare OS entry and page count.

## [2026-08-07] update | Orca orchestration CLI and Luna model routing
- Updated `entities/tools/orca.md` with the current Run/Task/Dispatch supervised flow, the retirement of `orca orchestration run`, deterministic wave eligibility rules, and the boundary between Orca agent selection and Codex model/effort configuration.

## [2026-08-08] update | Claude Code v2.1.224 execution boundary
- Added `raw/articles/anthropic-claude-code-v21224-2026-08-08.md`, preserving the official release facts and independent implementation/security analysis with an immutable-body checksum.
- Updated `entities/models/claude-opus-5.md` with self-hosted runner as a hybrid execution boundary, cross-session messaging as non-authoritative coordination, and the trailing-slash sandbox deny-rule fix.

## [2026-08-09] update | Codex v0.147 portable plugin and approval boundary
- Updated `comparisons/model-routing-hermes-opencode-pi.md` from the official `v0.147.0` release.
- Recorded the durable distinction between portable plugin/skill distribution and authority, plus the retained requirement for explicit sandboxing, scoped credentials, typed packets and independent gates when using automatic approval review.

## [2026-08-11] ingest | Muse Glimmer
- Added `raw/articles/meta-muse-glimmer-2026-08-11.md`, preserving a bounded official-source excerpt with an immutable-body checksum.
- Added `entities/models/muse-glimmer.md` with Apache-2.0 availability, stated local memory envelope, evidence boundary for vendor benchmarks, and a controlled local-agent evaluation protocol.
- Updated `index.md` with the model entry and page count.

## [2026-08-13] ingest | Agent Plugins 1.0 distribution boundary
- Added `raw/articles/agent-plugins-spec-100-2026-08-13.md`, preserving a bounded primary-source record and immutable body checksum for the published portable package format.
- Updated `comparisons/model-routing-hermes-opencode-pi.md` with the distinction between portable package distribution and operational authority: Agent Plugins carries skills/MCP configuration, not sandboxing, provenance, authorization or repository acceptance.
- Updated `concepts/model-context-protocol.md` to distinguish Agent Plugins packaging from MCP transport semantics and retain the research profile's non-MCP Agent Reach boundary.
- Updated `index.md` date; no new indexed synthesis page was created.

## [2026-08-14] update | Gemini Flash 3.7
- Added `raw/articles/google-gemini-3-7-flash-2026-08-14.md`, preserving the primary announcement with immutable-body checksum.
- Updated `entities/models/gemini-3-6-flash.md` into a 3.6/3.7 lineage page with API/Copilot rollout facts, independent Artificial Analysis snapshot, vendor-evidence boundary, and controlled-trial guidance.
- Updated `index.md` date and summary; no new entity page was created.

## [2026-08-18] create | Loop Engineering vs Graph Engineering
- Added `comparisons/loop-engineering-vs-graph-engineering.md` with definitions, relationship, benefits, limits, and practical hybrid guidance.
- Updated `index.md` with the comparison entry and page count.

## [2026-08-18] update | Apply graph engineering framing to Orca workflow
- Updated `comparisons/loop-engineering-vs-graph-engineering.md` with the mapping between Orca's task DAG/control plane, worker-local loops, deterministic gates, review and merge transitions.

## [2026-08-18] create | Orca graph workflow execution runbook
- Added `coding/runbooks/orca-graph-workflow-execution.md` with the operational sequence, task contract, gates, Orca command skeleton, example DAG and supervised pilot guidance.
- Updated `index.md` with the runbook entry and page count.

## [2026-08-18] update | Desktop-safe runbook formatting
- Replaced fragile plain-text tree/condition fences in `coding/runbooks/orca-graph-workflow-execution.md` with Markdown lists for reliable rendering.

## [2026-08-18] update | Orca UI and per-launch routing boundary
- Updated `entities/tools/orca.md` with the current public boundary: Runs/Tasks/Dispatches remain primarily CLI/runtime orchestration records, while the UI exposes worker/worktree/task-link surfaces rather than a dedicated Run/DAG explorer.
- Updated model-routing guidance to reflect documented optional per-launch `--model`/`--effort` flags for supported agent/host combinations, with requested/effective launch receipt verification.

## [2026-08-18] update | Linear issue to Orca task mapping
- Updated `coding/runbooks/orca-graph-workflow-execution.md` to distinguish Linear Issues from Orca Tasks, document explicit coordinator mapping, and record native worktree linking via `--linear-issue`.

## [2026-08-19] update | OpenAI frontier-training containment posture
- Added `raw/articles/openai-pacing-cyber-capabilities-2026-08-19.md`, retaining the primary announcement and immutable-body checksum.
- Updated `entities/models/gpt-5-6.md` with OpenAI's temporary RL pause, held frontier run, workload/network/shared-service containment claims, monitoring-stop boundary and first-party-evidence caveat.
- Updated `index.md` date; no new indexed page was created.

## [2026-08-20] ingest | OpenRouter joining Stripe and OneCLI v2
- Added `raw/articles/openrouter-stripe-2026-08-20.md` and `entities/tools/openrouter.md`, preserving the primary transaction announcement, its immutable-body checksum, and the operational requirement for tested provider/gateway exit paths.
- Added `raw/articles/onecli-v2-2026-08-20.md`; updated `entities/tools/onecli.md` with v2 workspaces/split-services/hosted-agents scope and the unverified-security boundary.
- Updated `comparisons/model-routing-hermes-opencode-pi.md` with the upstream-router dependency boundary, and updated `index.md` date/page count.

## [2026-08-23] create | Project memory and multi-model handoff layers
- Added `coding/architecture/project-memory-and-multi-model-handoff-layers.md` with the durable separation between canonical intent, structured execution state, task evidence/handoffs, project knowledge and ephemeral session compaction.
- Recorded the recommendation to use `CURRENT.md`/`PROJECT_STATUS.md` as a small cockpit rather than a monolithic `MEMORY.md`, and to keep mutable machine state in manifests or a ledger.
- Updated `index.md` and page count.

## [2026-08-24] update | Hermes Desktop model-usage boundary
- Updated `entities/tools/hermes-agent.md` with the durable distinction between focused-session context usage and provider account-quota windows.
- Recorded the split installation/runtime boundary for a local Desktop UI connected to a remote Hermes backend, including backend enablement and restart requirements.
- Updated `index.md` date; no new page was created.

## [2026-08-24] update | Native status-bar usage popover
- Updated `entities/tools/hermes-agent.md` with the native `StatusbarItem` menu pattern for compact usage controls.
- Recorded explicit quota-window labels (`Weekly`, `5hr`) and the preference against a permanent pane for this surface.

## [2026-08-24] debug | Model-usage session-switch query churn
- Updated `entities/tools/hermes-agent.md` with the account-query cache boundary: provider/model authority rather than focused-session identity.
- Recorded that session-scoped account query keys create redundant remote Desktop IPC/REST work during navigation.
- Recorded the synchronous event-listener boundary: deduplicate unchanged `session.info` route values before cloning or publishing plugin state.

## [2026-08-25] ingest | GLM-5.3
- Added `raw/articles/zai-glm-53-2026-08-25.md`, preserving a bounded primary-source excerpt, contemporary Hacker News attention/scrutiny records and immutable-body checksum.
- Added `entities/models/glm-5-3.md` with availability/evidence boundaries, contested vendor-relative benchmarks, and a controlled coding-agent trial protocol.
- Updated `index.md` date and page count.

## [2026-08-27] update | OpenAI/Hugging Face technical incident report
- Updated `entities/models/gpt-5-6.md` with the final OpenAI report and METR's independent, bounded investigation.
- Recorded durable harness implications: prevent accidental peer communication through shared services; do not treat agent-generated telemetry as authoritative; bind acceptance to independent receipts/logs and repository-native gates; stop or escalate corrupted/impossible tasks.
- Updated `index.md` date; no page was created or renamed.

## [2026-08-29] update | GLM-5.3-Flash availability and evaluation boundary
- Added `raw/articles/zai-glm-5-3-flash-model-card-2026-08-29.md`, preserving an immutable model-card excerpt and body checksum.
- Updated `entities/models/glm-5-3.md` with the distinct open-weight GLM-5.3-Flash variant, documented runtime paths, and the requirement for like-for-like harness evaluation; updated `index.md` date, with no new entity page.

## [2026-08-30] ingest | Astro Triagebot Action OpenAI provider
- Added `raw/articles/astro-triagebot-openai-provider-2026-08-30.md` with immutable primary-commit and independent-validation record plus checksum.
- Added `entities/tools/astro-triagebot-action.md`, documenting the staged reproduce/diagnose/verify/fix pattern, GitHub-visible state, reporter validation, maintainer acceptance and the new OpenAI provider path.
- Updated `index.md` date and page count.

## [2026-08-31] ingest | Tencent Hy4 preview
- Added `raw/articles/tencent-hy4-preview-model-card-2026-08-31.md` with a bounded primary model-card excerpt and immutable-body checksum.
- Added `entities/models/tencent-hy4.md`, preserving the Apache-2.0/open-weight availability facts, vendor-evidence boundary, documented serving paths, and fixed-harness trial protocol.
- Updated `index.md` date and page count.

## [2026-09-02] ingest | Claude Fable 5.1 / Mythos 5.1
- Added `raw/articles/anthropic-claude-fable-51-2026-09-01.md`, preserving a bounded primary-source capture and immutable-body checksum.
- Added `entities/models/claude-fable-5-1.md` with the API-migration, retention, vendor-evidence and controlled-trial boundaries for the 01/09 release.
- Updated `entities/models/claude-opus-5.md` with a reciprocal fixed-harness comparison link, and updated `index.md` date/page count.
