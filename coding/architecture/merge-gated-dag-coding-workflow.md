---
title: Merge-Gated DAG Coding Workflow
created: 2026-07-25
updated: 2026-09-08
type: architecture
tags: [agent, agent-orchestration, multi-agent, workflow, coding, architecture, testing, devops]
sources:
  - https://x.com/gkpacker/status/2080306086653894733
  - https://git-scm.com/docs/git-worktree
  - https://git-scm.com/docs/git-clone
  - https://fletch.sh/blog/git-worktrees-vs-clones-for-ai-agents/
  - https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-protected-branches/about-protected-branches
  - raw/articles/openai-research-acceleration-2026-09-06.md
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

## Minimal practical rollout

Start with a control-plane-first pilot because concurrent autonomous work is already a requirement:

1. JSON/YAML schemas for project, task and result packets.
2. SQLite execution ledger with atomic claims, attempts, leases and event log.
3. Git checkout manager with linked-worktree and isolated-clone modes chosen by trust boundary.
4. One gate runner wrapping repository-native commands plus scope/dependency checks.
5. GitHub/Linear reconciliation and SHA-bound review state.
6. Human merge; no autonomous merge initially.
7. Five to ten fixture/real low-risk tasks before adding model routing, auto-remediation, release automation or more reviewer agents.

Related: [[comparisons/model-routing-hermes-opencode-pi]], [[entities/tools/hermes-agent]] and [[entities/tools/orca]].
