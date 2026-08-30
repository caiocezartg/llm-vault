---
title: Project Memory and Multi-Model Handoff Layers
created: 2026-08-23
updated: 2026-08-23
type: architecture
tags: [agent, agent-orchestration, multi-agent, workflow, coding, architecture, memory, convention, testing]
sources:
  - /home/caiocezartg/.hermes/skills/software-development/spec-driven-agentic-development/references/session-vs-task-handoffs.md
  - /home/caiocezartg/.hermes/skills/note-taking/global-llm-wiki-workflows/references/project-local-wiki-patterns.md
  - [[concepts/global-llm-wiki]]
  - [[coding/architecture/merge-gated-dag-coding-workflow]]
confidence: medium
contested: false
contradictions: []
---

# Project Memory and Multi-Model Handoff Layers

## Core recommendation

Do not use one `MEMORY.md` as the memory, state store, handoff, specification, and knowledge base at the same time. The reliable pattern is a small set of artifacts with explicit authority boundaries:

```text
canonical intent → structured execution state → task evidence/handoff → durable project knowledge
                              ↑
                 ephemeral session compaction
```

A new model should not be asked to rediscover settled decisions. It should reconcile a typed task packet against canonical artifacts and repository state, then continue from one explicit next action.

## Authority layers

| Layer | Canonical artifact | Stores | Must not store |
|---|---|---|---|
| Intent | spec, ADR, approved plan | requirements, acceptance IDs, non-goals, approved decisions | transient progress |
| Execution state | YAML/JSON manifest or SQLite ledger | phase, task status, dependencies, claims, attempts, leases, retries, gate verdicts | prose-only guesses |
| Task boundary | versioned task handoff/result | changed files, exact commands/results, deviations, blockers, risks, next action | a replacement spec |
| Project knowledge | project-local wiki/docs | glossary, architecture, validated debugging patterns, runbooks, reusable conventions | current ticket status |
| Session bridge | temporary `/handoff`-style note | live thread, references, immediate continuation, suggested skills | transcript dump or completion verdict |

The repository, tests and executable gates remain authoritative for code behavior. A handoff communicates evidence; it does not make work complete. A tracker such as Linear can project human-facing status, but it should not silently replace the execution ledger.

## Is `MEMORY.md` a good idea?

Yes, but only as a **small project cockpit**. Prefer naming it `CURRENT.md` or `PROJECT_STATUS.md` so its mutable role is obvious. It can contain:

- current phase and one-line objective;
- canonical spec/plan/task links;
- last accepted commit or release reference;
- current task and its single next action;
- blockers and explicit decisions that must not be reopened casually;
- the command for the next focused verification;
- a short “changed since last checkpoint” section.

It should be an index and checkpoint, not a full memory dump. If an agent needs to read the whole project history from it, the layering has failed. Keep machine-consumed status in `state.yaml`, `tasks/*.yaml`, or a ledger; keep explanation and navigation in Markdown.

Example project layout:

```text
project/
├── AGENTS.md
├── docs/
│   ├── spec.md
│   ├── adr/
│   └── llm/
│       ├── CURRENT.md
│       ├── index.md
│       ├── log.md
│       ├── architecture/
│       ├── debugging/
│       └── runbooks/
├── .agent-workflow/
│   ├── state.yaml
│   ├── tasks/
│   │   ├── T-001.yaml
│   │   └── T-001.result.md
│   ├── handoffs/
│   │   └── T-001-attempt-02.md
│   ├── gates/
│   └── events.jsonl
├── src/
└── tests/
```

`CURRENT.md` may point to `.agent-workflow/state.yaml`; it should not duplicate every field from it.

## Resume protocol for a new model

Use a fixed, cheap read order instead of placing all context into the prompt:

1. Read `AGENTS.md` and repository safety/contribution rules.
2. Read `CURRENT.md` for the cockpit view.
3. Read the referenced spec, ADRs and task manifest—not unrelated project docs.
4. Read the latest task handoff/result.
5. Reconcile the handoff with `git status`, the recorded base/head SHA and the actual changed files.
6. Run one focused health check or gate before changing code.
7. Continue with the declared next action, or stop and record a reconciliation conflict.

This makes the handoff a pointer plus evidence rather than a second, drifting source of truth.

## Minimum task handoff contract

A durable task handoff should include:

- task, attempt and handoff IDs;
- spec requirement and acceptance-criterion IDs;
- mode: `checkpoint`, `blocked`, or `ready-for-review`;
- repository, branch/worktree, base commit and current commit;
- dirty/untracked state when relevant;
- files changed and declared scope;
- exact commands with `passed`, `failed`, or `not-run` outcomes;
- decisions, deviations, blockers and risks;
- one next action and its stop condition;
- selected harness/model only when it matters for reproducibility.

The receiver should never infer “done” from a confident paragraph or from `worker_done`; gates and independent review own acceptance.

## Why multi-model workflows re-analyze work

Repeated analysis usually means the context boundary carries a summary but not a contract. Common causes are:

- settled decisions are copied without IDs, rationale or authority;
- the “next step” is vague, so every model replans;
- current state, durable knowledge and session history are mixed together;
- evidence is missing or not bound to a commit/worktree;
- non-goals and rejected alternatives are omitted;
- one model's natural-language conclusion is treated as authoritative instead of as an input to verification;
- the receiving model has no explicit read order or resume check.

The fix is not a larger summary. It is stronger boundaries: stable IDs, references-not-copies, explicit non-goals, evidence, freshness, and deterministic gates.

## Routing across models

Use the handoff to preserve the **task contract**, not the previous model's reasoning trace. A practical split is:

- high-judgment model: discovery, ambiguity resolution, architecture and spec criticism;
- balanced executor: one clear vertical task with tests and a bounded write set;
- strong debugging/escalation lane: failed gates, unclear repository behavior or risky changes;
- independent reviewer: spec, regression, security and scope review;
- cheap/local model: deterministic transformations and tightly verified tasks only.

Do not let a cheaper executor reopen the product decision or rewrite the approved spec. Do not let the planner declare implementation complete. Re-plan only when a named trigger occurs: a failed gate, changed requirement, dependency drift, scope conflict, or an unresolved question becoming material.

## Promotion rules

- **Session handoff → task handoff:** promote only the factual task boundary and evidence needed for another executor/reviewer.
- **Task handoff → project knowledge:** promote only validated, reusable findings such as an architecture rule, debugging pattern or runbook.
- **Project knowledge → global wiki:** promote only findings that recur across projects or profiles.
- **Current status:** keep it mutable and local; do not promote temporary progress into durable memory.

This preserves the distinction between immediate continuation, mutable workflow state and compounding knowledge.

## Minimal rollout

Start with four artifacts before building a memory service:

1. `CURRENT.md` as a human-readable cockpit.
2. `state.yaml` or a small task manifest as machine-readable state.
3. one versioned handoff template with exact command evidence.
4. a resume script that checks the repository ref, changed files and one focused gate.

Add a SQLite ledger, immutable attempt files, stale-context detection, automatic promotion or retrieval infrastructure only after real tasks show coordination failures that justify them.

## Anti-patterns

- one giant `MEMORY.md` containing spec, transcript, TODOs and architecture;
- copying canonical documents into every handoff;
- using Markdown prose as a transaction log for concurrent workers;
- passing chain-of-thought or full transcripts between models;
- allowing a handoff to declare `Done`;
- storing secrets or credentials in any memory layer;
- loading the whole wiki into every context instead of retrieving by index and task references.

Related: [[concepts/global-llm-wiki]], [[coding/architecture/merge-gated-dag-coding-workflow]], and [[entities/tools/hermes-agent]].
