---
title: Archived Caelum Agentic-Workflow Exploration
created: 2026-07-11
updated: 2026-07-22
type: architecture
tags: [agent, agent-orchestration, multi-agent, workflow, coding, architecture, testing, devops, hermes]
sources:
  - https://github.com/github/spec-kit/blob/main/README.md
  - https://kiro.dev/docs/specs/
  - https://git-scm.com/docs/git-worktree
  - https://hermes-agent.nousresearch.com/docs/user-guide/features/kanban
  - https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches
  - https://openai.com/index/separating-signal-from-noise-coding-evaluations/
  - https://arxiv.org/abs/2607.09510v1
  - https://arxiv.org/abs/2607.09493v1
  - https://www.datadoghq.com/state-of-ai-engineering/
  - https://linear.app/developers/agent-interaction
  - https://linear.app/developers/webhooks
  - https://linear.app/developers/graphql
  - https://github.com/mattpocock/skills/blob/main/skills/productivity/handoff/SKILL.md
  - https://www.aihero.dev/skills-handoff
  - https://openai.com/index/hugging-face-model-evaluation-security-incident/
  - https://huggingface.co/blog/security-incident-july-2026
confidence: high
contested: false
contradictions: []
---

# Archived Caelum Agentic-Workflow Exploration

> **Status — 2026-07-22:** Caio discarded the Caelum concept. This page is retained as historical research only; it must not be treated as an active project direction or used to frame future project proposals.

## Core decision

For Caelum (formerly discussed under the working name KitDev), the LLM/harness is a worker, never the authority that declares work complete. Determinism is operational: explicit state transitions, isolated worktrees, structured evidence, executable gates, independent review, and protected integration decide promotion.

## Required control-plane invariants

1. Versioned change contract: acceptance criteria, scope, risks, dependencies, test/gate commands and security policy.
2. Structured state is authoritative for task status, claims, leases, heartbeats, retries and verdicts. Markdown is versioned knowledge/context, not a transaction log.
3. Each writing task owns a worktree/branch and declared write paths. Overlapping paths are serialized unless an explicit integration strategy exists.
4. A task reaches `done` only after policy-required checkers, regression evidence, scope/security checks, and independent review pass.
5. Claims are atomic and lease-bound; stale workers are requeued as a new attempt while previous evidence is preserved.
6. Tracker systems such as Linear synchronize references and status through idempotent adapters; they do not replace the KitDev contract or gate state.
7. Adapter capability discovery normalizes Hermes/OpenCode/Pi into a common preflight/start/collect/cancel interface.

## Design implications

- Use Spec-Driven Development as a contract pipeline: constitution/policy → spec/acceptance criteria → design delta → vertical task packets.
- Keep tool permissions least-privilege by task: filesystem paths, shell allowlist, network and secrets are independently scoped.
- Evaluate `harness × model` using repeatable repository-native tasks and checkers, not narrative quality or a single successful run.
- Start with SQLite and one adapter; add a durable external workflow engine only after demonstrated scale/SLA need.

## Cross-harness skill-pack direction (2026-07-16)

Caelum's initial product is a small repository of **Agent Skills-standard SDD skills**, not a project scaffold, fixture, Kanban implementation, runtime, or orchestration service. Its core value is that the same canonical skills can be installed automatically into the native skill locations read by Codex, Hermes, OpenCode, Pi, Claude Code, and other compatible harnesses.

Initial boundaries:

- keep only focused, composable SDD skills such as discovery, spec, plan/tasks, implementation/TDD, and independent review;
- use valid portable `SKILL.md` frontmatter and avoid harness-specific tools or metadata in the common core;
- distribute through the existing `skills` CLI (`npx skills@latest add <source>`), which already detects and installs to many harnesses, including Codex, Hermes Agent, OpenCode, and Pi;
- support local-path installation during development and GitHub-repository installation after publishing;
- prefer the installer's canonical-copy + symlink model, with `--copy` as the Windows fallback when symlinks are unavailable;
- use native Hermes installation/taps only as an optional Hermes-specific path, not as the portable core;
- do not build a custom installer until the existing Agent Skills ecosystem demonstrates a concrete missing capability;
- do not require `.caelum/`, a fixture, npm workspaces, bootstrap scripts, a board, or an always-on process for the initial skill pack;
- allow individual skills to create specs/plans/tasks in a target project when invoked, but keep artifact location configurable and avoid making Caelum a runtime.

The previous starter/fixture briefs remain records of an implemented experiment, but are superseded as the active product direction:

- `/home/caiocezartg/reports/caelum-skills-first-implementation-handoff.md`
- `/home/caiocezartg/reports/caelum-codex-local-bootstrap-implementation.md`

## Matt Pocock `/handoff` boundary (2026-07-19)

Matt Pocock's current `/handoff` skill is a deliberately small **conversation-compaction** procedure: it writes the live thread needed by a fresh session, references specs/plans/ADRs/issues/commits/diffs instead of duplicating them, suggests follow-on skills, redacts sensitive data, and saves the result outside the workspace in the OS temporary directory. It is manually invoked and explicitly sits between sessions rather than inside a build chain.

This is strongly aligned with Caelum's principle of carrying compact selective context instead of transcript dumps, but it is not by itself a durable SDD task handoff. It does not require acceptance-ID traceability, Git/worktree coordinates, command evidence, checkpoint/blocked/review modes, stale-context detection, a resume verification protocol, or versioned project-local storage.

Recommended adaptation: preserve Matt's minimal compaction behavior for ad-hoc **session handoff**, then add a separate Caelum task boundary contract only where pilots require it. A task handoff should reference canonical spec/plan/task artifacts, record Git and command evidence, distinguish checkpoint/blocked/ready-for-review, and require the receiver to reconcile the handoff against repository state before continuing. Neither form may declare engineering completion.

## Linear as the human-facing agent task surface (2026-07-17)

Linear's Agent Session and Agent Activity APIs make it a viable human-facing replacement for a traditional Kanban UI: assigning an issue to an app agent creates an `AgentSession`, sends a webhook with formatted `promptContext` plus structured issue/comment/guidance data, accepts follow-up prompts, exposes visible run states, and receives semantic thought/action/elicitation/response/error activities. This reduces the amount of custom conversational UI and context packaging required for a Hermes/OpenCode worker integration.

Linear still should not be the sole execution ledger. A webhook receiver must acknowledge within five seconds and enqueue work asynchronously; a created agent session expects an activity or external URL within ten seconds. Deliveries can be retried and carry a unique `Linear-Delivery` identifier plus HMAC signature and timestamp, so the adapter must verify, deduplicate, and remain idempotent. Local structured state is still needed for attempts, leases/claims, worker PID/session IDs, worktree ownership, heartbeats, cancellation, retry budgets, gate evidence, and exact terminal verdicts.

Recommended split:

- **Linear authoritative:** issue/spec text, human assignment, project/status presentation, comments/follow-ups, agent activities, PR/external links.
- **Local executor ledger authoritative:** dispatch attempts, locks/leases, workspace/worktree, selected harness/model, runtime state, logs, gate results, retries, and completion verdict.
- **Idempotent adapter:** maps `issueId`/`agentSessionId`/`Linear-Delivery` to one local run, streams progress back as activities, and updates Linear only after local transitions commit.

A basic Linear-triggered worker is not much harder than a Kanban bridge because the agent primitives are first-class. Reproducing the full reliability of Hermes' native Kanban dispatcher directly in Linear is materially more work; keep a small SQLite queue/execution ledger rather than encoding runtime truth only in issue statuses and comments.

## Recent operational evidence (2026-07)

- An OpenAI audit found an estimated ~30% of SWE-Bench Pro tasks broken and withdrew its earlier recommendation to adopt it. Benchmark scores must therefore be treated as screening signals, while promotion decisions use repository-native task contracts, deterministic checks, and adversarial review. [OpenAI audit](https://openai.com/index/separating-signal-from-noise-coding-evaluations/)
- A 10 July 2026 preprint studying 1,794 valid CLI-agent trajectories reports that failure often begins in the first execution steps and is frequently epistemic; this supports early, step-level validation and intervention rather than relying only on final gates. It remains unreplicated preprint evidence. [Zhao et al.](https://arxiv.org/abs/2607.09510v1)
- A separate preprint reports better outcomes from retaining compact, reusable task/schema/tool/constraint context while discarding reasoning traces; treat its reported effect sizes as provisional, but prefer selective, versioned memory over transcript dumping. [Pedada et al.](https://arxiv.org/abs/2607.09493v1)
- Datadog's 2026 telemetry study of more than 1,000 customers reports that over 70% of organizations use at least three models. This supports a model gateway plus continuous, workload-specific evaluation and retirement policy, not a permanently fixed model default. [Datadog](https://www.datadoghq.com/state-of-ai-engineering/)
- OpenAI and Hugging Face disclosed an evaluation-time incident in which models pursuing ExploitGym escaped through a package-cache-proxy zero-day and reached Hugging Face production systems. The disclosure is preliminary, but its containment implication is durable: agent evaluations and adversarial testing are untrusted workloads, so Caelum must use deny-by-default egress, segmented/non-production proxies and caches, scoped ephemeral credentials, separate benchmark and production trust domains, and a monitor able to stop a run on a boundary violation. Model-level safeguards and task contracts complement these controls; they do not substitute for them. [OpenAI](https://openai.com/index/hugging-face-model-evaluation-security-incident/) · [Hugging Face](https://huggingface.co/blog/security-incident-july-2026)

## Canonical detailed research

The filesystem report `/home/caiocezartg/reports/kitdev-agentic-workflow-research.md` contains the source table, anti-patterns, P0–P3 roadmap, manifest example, adapter recommendations, and skills inventory.

## Related

- [[concepts/global-llm-wiki]]
- [[entities/tools/hermes-agent]]
