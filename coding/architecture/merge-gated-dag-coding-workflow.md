---
title: Merge-Gated DAG Coding Workflow
created: 2026-07-25
updated: 2026-10-11
type: architecture
tags: [agent, agent-orchestration, multi-agent, workflow, coding, architecture, testing, devops]
sources:
  - https://x.com/gkpacker/status/2080306086653894733
  - https://git-scm.com/docs/git-worktree
  - https://git-scm.com/docs/git-clone
  - https://fletch.sh/blog/git-worktrees-vs-clones-for-ai-agents/
  - https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches
  - raw/articles/openai-research-acceleration-2026-09-06.md
  - raw/articles/apple-full-disk-access-agent-boundary-2026-10-02.md
  - raw/articles/adversa-cryptographic-context-injection-copilot-2026-10-06.md
  - raw/papers/chen-stratton-ai-software-production-bottlenecks-2026-10-10.md
  - raw/articles/cockroach-molt-sinai-2026-10-09.md
  - raw/articles/microsoft-mxc-v1-2026-10-07.md
confidence: high
contested: false
contradictions: []
---

# Merge-Gated DAG Coding Workflow

A practical coding-agent control plane can schedule small vertical tasks as a dependency DAG and execute only the currently eligible antichain (a “wave”). Every task runs from the latest accepted `origin/main` in a separate checkout; a linked worktree is a concurrency convenience, not a security/isolation boundary. Downstream tasks become eligible only after their dependencies are actually merged, not merely implemented or green in CI.

This pattern combines ideas from [[coding/architecture/kitdev-deterministic-agentic-workflows]] with a concrete solo-founder workflow described by Gabriel Packer. The old project name on the archived page is historical only; this page describes a generic architecture.

## Recommended authority split

- **Product/spec authority:** approved product brief/spec with stable acceptance IDs and unresolved-question handling.
- **Task contract:** a validated manifest generated from the spec; Linear may project it, but prose alone is not sufficient machine state.
- **Execution ledger:** attempts, leases, worker/run IDs, worktrees, base SHA, heartbeats, retry budget and cancellation.
- **Gates:** executable checks own mechanical verdicts.
- **Independent reviewer:** semantic/spec/security judgment at the exact reviewed commit SHA.
- **Human:** product ambiguity, high-risk exceptions and final merge policy.

## Roles

1. **Discovery/PM agent:** clarifies problem, users, desired behavior, non-goals, metrics and open product decisions. It cannot approve its own output.
2. **Design/domain agent:** produces interaction states, contracts, edge cases, accessibility/i18n/privacy implications and design evidence. It cannot create implementation-ready tasks while questions remain open.
3. **Spec editor:** compiles approved decisions into a canonical spec with requirement and acceptance IDs.
4. **Task compiler/DAG planner:** inspects the repository and produces small vertical task manifests, explicit dependencies, predicted write sets, tests, risk class and stop conditions. It must reject cycles and fake “foundation” tasks.
5. **Deterministic dispatcher:** computes eligibility from state (`Ready`, dependencies merged, no blockers, concurrency/conflict budgets available), creates a fresh separate checkout from current `origin/main`, records base SHA and launches one executor.
6. **Executor:** implements exactly one task, preferably test-first, within scope; it emits code plus factual evidence and stops at `Review` or `Blocked`.
7. **Gate runner:** independently checks manifest/schema, scope/diff/dependencies, tests, lint/type/build, security and required evidence. The executor cannot waive failures.
8. **Reviewers:** separate spec-compliance and code-risk review from implementation; verdicts are bound to the PR head SHA.
9. **Integrator/release controller:** verifies current-head gates/reviews, mergeability, rollout/rollback/observability and performs or requests merge according to policy.
10. **Retrospective/evaluation worker:** records recurring failure classes, cycle time, retries and review escapes; only repeated failures justify new gates or skills.

## State machine

```text
Draft → Spec Review → Planned → Ready → Claimed → Implementing → Verifying
                                                    ↘ Blocked
Verifying → In Review → Approved → Merge Ready → Merged → Observing → Done
                              ↘ Changes Requested → Implementing
```

`CI green`, `PR open`, `review approved`, `merged` and `done` are distinct states. New commits invalidate prior gate/review verdicts unless rerun against the new head SHA.

## Wave algorithm

At each scheduling event, refresh `origin/main`, reconcile PR/CI/merge state, then choose tasks satisfying all of:

```text
status == Ready
AND every dependency.status == Merged
AND blockers == none
AND manifest_valid
AND no predicted write-set conflict with active tasks
AND risk/concurrency budgets permit launch
```

A wave is a snapshot for observability, not a barrier. A downstream task may launch as soon as all of its own parents are merged; it need not wait for unrelated siblings in the same nominal wave. Every launch gets a new worktree from the latest accepted main SHA.

## Gates

### Before Ready

- spec has stable requirement/acceptance IDs;
- no unresolved blocking question;
- task is one vertical observable behavior with explicit non-goals;
- test, rollout, telemetry and stop conditions exist when applicable;
- DAG is acyclic and every dependency has an explicit reason;
- predicted write sets and public-contract effects are declared.

### Before execution

- dependencies are **merged** into main;
- fresh checkout/base SHA recorded;
- task claim is atomic and lease-bound;
- checkout type is chosen by trust boundary: linked worktrees only for supervised/convenience use, isolated clones plus OS/container/VM enforcement for unattended or untrusted workers;
- tool, path, network and secret permissions are scoped;
- repository preflight/baseline passes or an existing failure is recorded.

### Before review

- focused tests plus relevant regression suite pass;
- lint/typecheck/build/pre-commit pass where configured;
- changed paths, diff size, dependency/lockfile, migration and generated-file policies pass;
- acceptance IDs have machine-readable evidence;
- UI/flow changes include screenshots, recordings or browser-test artifacts where useful;
- handoff lists exact commands/results, files, deviations, risks and PR head SHA.

### Before merge

- independent spec-compliance and code-risk reviews pass at current head SHA;
- all required CI checks pass and cancelled/superseded runs are distinguished from failures;
- branch is mergeable against current main or rebased and revalidated;
- rollout, kill switch, telemetry and rollback are ready for risky changes;
- human approval is required for configured risk classes.

### After merge

- main-branch CI/deployment health passes;
- smoke/canary checks and telemetry are observed where applicable;
- only then is the task `Done` and downstream dependencies released.

## Important corrections to the simple diagram

- The orchestrator should route and reconcile; it should not use LLM judgment for deterministic eligibility or own correctness verdicts.
- The ticket may be the human-facing prompt, but the canonical execution packet should be compiled/validated and include repository revision plus acceptance traceability.
- “Under 400 lines” and story points are heuristics, not hard correctness gates; semantic cohesion and risk matter more.
- Tests are not separate tickets, but implementation and test work should not be delegated to independent writers whose changes can disagree. The same task owns both; an independent verifier checks them.
- Parallel tasks can still conflict without graph edges. Add predicted write-set/API/schema conflict detection and serialize shared hotspots.
- A full-wave barrier wastes parallelism. Release nodes when their own dependencies merge.
- Do not conflate a green PR branch with production truth: revalidate on current main and observe post-merge/deploy health.
- A linked Git worktree has a separate working directory, `HEAD`, and index, but shares the common `.git` state (including config, refs, stash, and hooks). It is therefore not a process, credential, or host-execution isolation boundary. For unattended/untrusted agents, enforce sandboxing outside the harness and prefer independent local clones; `git clone --shared` can reduce object-store duplication, but its source-repository dependency must be managed deliberately (for example, no premature source GC/deletion).

## Evidence boundary from OpenAI's internal deployment (2026)

OpenAI's 06/09/2026 internal snapshot reports 3.1 coding-agent workdays of runtime for each human workday in its research organization, including direct agents and downstream subagents. This is a scale signal for concurrent execution—not a portable productivity multiplier: OpenAI also reports expanded compute capacity and does not isolate the causal contribution of agents. ^[raw/articles/openai-research-acceleration-2026-09-06.md]

More importantly for a control plane, its outcome analysis says that more than half of successful tasks estimated at four to eight human-hours required at least one human intervention. Treat intervention as a first-class state transition with an explicit owner, evidence and re-entry condition; do not hide it in a chat thread or let aggregate agent runtime stand in for accepted output. The relevant measures are accepted tasks, gate/review escape rate, rework, time-to-accepted-change and human intervention cost. ^[raw/articles/openai-research-acceleration-2026-09-06.md]

## App-level permissions are inherited authority

Apple’s 2 October 2026 Full Disk Access announcement makes a portable agent-workflow boundary explicit: a broad permission granted to the terminal, editor or desktop agent host is inherited by arbitrary scripts, plugins and agent actions it launches. User consent can be necessary, but it is not a task-scoped security control. Keep agent execution in a minimal workspace with task-scoped filesystem, network and credential authority; do not grant Full Disk Access to a general-purpose coding-agent host merely to make one workflow convenient. This does not predict Apple’s final control mechanics. ^[raw/articles/apple-full-disk-access-agent-boundary-2026-10-02.md]

## Cryptographic Context Injection keeps its source trust after decryption

Adversa AI's October 2026 Copilot CLI demonstration adds a distinct trust-boundary rule: ciphertext fetched from an untrusted page does not become trusted merely because the agent decrypted it or because the plaintext arrives through the tool/runtime result channel. The reported chain links untrusted web content, local-file reads and unrelated outbound egress; it also varies by effective model, so a model refusal is not a policy boundary. The report has important limits — autopilot plus a permissive model are required, its rates are researcher-reported, and GitHub reportedly declined to classify the behavior as a product vulnerability — but the control implication is reusable. ^[raw/articles/adversa-cryptographic-context-injection-copilot-2026-10-06.md]

For every agent run, preserve provenance and taint classification across fetch, execution, decryption, tool output and intermediate state. Record resolved tool arguments and connect read paths plus egress destinations to the same run ID; summaries written by the agent are not authoritative receipts. Enforce the paths it may read, short-lived credentials, and destination/method allowlists outside the model; require explicit review for operations that combine untrusted-content processing with access beyond the task workspace. This refines the broader egress and independent-verification controls in [[entities/tools/openai-agents-api]] and [[comparisons/model-routing-hermes-opencode-pi]].

## Review capacity is a first-class throughput constraint

Chen and Stratton's observational study of 718 firms reports that coding-agent adoption correlates with substantially more code, commits and pull requests, but not a statistically significant change in firm-level issue or epic resolution in its January 2021–March 2026 sample. Its proposed mechanism is code review: PR-to-merge time rises, more PRs require revision, comments increase, and firms assign a larger share of workers to review. The evidence is not an experiment and cannot determine the outcome for a particular model, repository or team; it is a reason to instrument the production pipeline rather than treat token volume or diff count as delivery. ^[raw/papers/chen-stratton-ai-software-production-bottlenecks-2026-10-10.md]

Measure review queue depth and latency, revision/rework rate, executable-evidence coverage, reviewer intervention, acceptance rate and time-to-accepted-change alongside model cost and generation speed. Raise parallel-agent concurrency only when these downstream measures retain headroom. Use scoped tasks, SHA-bound gates, reproducible test evidence and independently reviewed diffs to reduce avoidable review load; do not replace review with an unaudited agent verdict.

## Minimal practical rollout

Start with a control-plane-first pilot because concurrent autonomous work is already a requirement:

1. JSON/YAML schemas for project, task and result packets.
2. SQLite execution ledger with atomic claims, attempts, leases and event log.
3. Git checkout manager with linked-worktree and isolated-clone modes chosen by trust boundary.
4. One gate runner wrapping repository-native commands plus scope/dependency checks.
5. GitHub/Linear reconciliation and SHA-bound review state.
6. Human merge; no autonomous merge initially.
7. Five to ten fixture/real low-risk tasks before adding model routing, auto-remediation, release automation or more reviewer agents.

## Evidence from Cockroach Labs' MOLT Sinai pipeline

Cockroach Labs' first-party five-month report provides a useful operational counterweight to throughput-oriented agent demonstrations. Its stated “teaching hospital” workflow combines issue decomposition, reviewed plans, separate implementer and reviewer roles, explicit discharge conditions, periodic recovery/process roles, and human escalation. For a Db2 migration feature, the company reports 32 decomposition/follow-up issues, 27 merged PRs, 55 review returns and nine escalations; these are implementation-specific self-reported figures, not a portable benchmark. ^[raw/articles/cockroach-molt-sinai-2026-10-09.md]

The transferable result is the control pattern, not the hospital vocabulary or reported speed: require planning before implementation, separate implementation from review, expose blocked/stalled states, make merge conditions executable, and record escalation. Its most important qualification is that after an initial autonomous period Cockroach Labs required human review for every merge, and it still described verification of the unreviewed initial Db2 work as incomplete. Keep human approval as the default for significant changes; measure review returns, escalations, rework and acceptance rather than advertising code volume or elapsed generation time. ^[raw/articles/cockroach-molt-sinai-2026-10-09.md]

## Execution containment is a separate, backend-specific gate

[[entities/tools/microsoft-execution-containers|Microsoft Execution Containers]] v1.0 makes an executable policy boundary available to agent/workload hosts: a workload can be given explicit filesystem, network, process and UI authority outside the harness. Treat policy learning/permissive modes only as evidence-gathering; accept a policy only after exercising denied and allowed paths under enforcement. MXC's process, session, WSL and experimental MicroVM backends have different guarantees, so a unified SDK API is not an isolation equivalence proof. ^[raw/articles/microsoft-mxc-v1-2026-10-07.md]

Related: [[comparisons/model-routing-hermes-opencode-pi]], [[entities/tools/hermes-agent]], [[entities/tools/orca]] and [[entities/tools/microsoft-execution-containers]].
