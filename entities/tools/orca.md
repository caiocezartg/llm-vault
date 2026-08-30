---
title: Orca
created: 2026-07-26
updated: 2026-08-07
type: entity
tags: [tool, agent, agent-orchestration, multi-agent, workflow, coding, repository, computer-use]
sources:
  - https://github.com/stablyai/orca
  - https://www.onorca.dev/docs/model/worktrees
  - https://www.onorca.dev/docs/cli/skills
  - https://www.onorca.dev/docs/cli/orchestration
  - https://www.onorca.dev/docs/cli/reference
  - https://developers.openai.com/codex/models
  - https://developers.openai.com/codex/config-reference
confidence: high
contested: false
contradictions: []
---

# Orca

Orca is an open-source agent development environment and orchestration runtime for running multiple CLI coding agents in parallel. It is worktree-native: each coding task can have its own Git worktree, branch, files, terminals, browser state, review surface and optional issue link. Supported agents include Codex, Claude Code, OpenCode, Pi and Hermes Agent.

## Durable boundary

Orca is strongest as an **execution cockpit and coordination control plane**, not as the source of product intent:

- `orca-cli` owns Orca-managed worktrees, terminals, files, automations and its embedded browser;
- `orchestration` owns persistent messages, task records, dispatches, dependency state, worker lifecycle messages and decision gates;
- `computer-use` owns accessibility/screenshot-driven desktop interaction;
- `orca-linear` projects linked ticket context and updates into Linear;
- emulator and per-workspace-environment skills cover specialized runtime surfaces.

Discovery/spec skills such as `grill-with-docs`, `to-spec` and `to-tickets` remain cognitive/document procedures. Their reviewed artifacts should feed Orca tasks; they should not replace Orca dispatch state, Git isolation, executable repository gates or independent review. This follows [[coding/architecture/merge-gated-dag-coding-workflow]].

## Recommended workflow

```text
brief
→ optional discovery (`grill-with-docs`)
→ approved canonical spec (`to-spec`, adapted)
→ vertical task DAG (`to-tickets`, adapted)
→ Orca task/worktree/dispatch per eligible task
→ bounded implementation + TDD
→ executable repository gates
→ independent spec/code review at the delivered SHA
→ merge and post-merge validation
```

Use manual task creation and dispatch first when the task DAG was already authored and approved. Avoid asking `orca orchestration run` to independently reinterpret a broad product brief during the initial pilot; that collapses spec authoring, decomposition and execution authority back into one model loop.

## Current orchestration CLI (2026-08-07)

The current Orca guide retires the old `orca orchestration run` and `run-stop` commands. The supported supervised flow is `run-create` → task records → `worker-start` → `check`/acknowledge deliveries. Orchestration is experimental and must be enabled in Settings → Experimental; verify `orca status --json` before mutating state and load the live version-matched guide with `orca skills get orchestration --full`.

The Run is a namespace/inbox, not a scheduler. A Task carries the spec, dependencies and status; a Dispatch is one worker attempt. The coordinator must compute the eligible antichain from JSON state rather than asking a model to guess: `status == ready`, every dependency is actually accepted/merged, no blocker or write-set conflict exists, the task packet is valid, and the concurrency/risk budget allows launch. Use `orca orchestration worker-start` once per eligible task and retain the returned task/dispatch IDs. `worker_done` is delivery evidence, not engineering acceptance; release or retain settled workers deliberately and run independent repository gates/review before merge.

The current version-matched Orca guide documents optional per-launch `--model` and `--effort` for supported Claude/Codex/Cursor launches (not with `--terminal`); the receipt exposes `launch.requested` and `launch.effective`, and federated starts require a host that advertises launch-preference support. Load `orca skills get orchestration --full` before relying on the flags. If the installed agent/host does not support them, configure a dedicated Codex profile/custom Orca agent (for example `codex-luna-max`) with `model = "gpt-5.6-luna"` and the installed Codex release's accepted maximum effort value (`max` or its version-specific equivalent such as `xhigh`), then launch with `--agent codex-luna-max`. Record requested and observed model/effort separately; do not claim that a prompt alone forced the model.

A valid `worker_done` completes the active Orca dispatch and task lifecycle, but it is not by itself engineering acceptance. Treat it as “worker delivered a result.” Acceptance still requires project-native tests/gates, independent review and merge policy. Likewise, Orca decision gates record coordinator-owned choices; they are not substitutes for executable test/lint/build/security gates.

## Skill installation and versioning

Orca publishes Agent Skills packages from `skills/<name>/SKILL.md`, installable with `npx skills add https://github.com/stablyai/orca --skill <name>`. The public `SKILL.md` files are discovery stubs; the version-matched detailed guide is served by the installed Orca binary:

```text
orca skills list
orca skills get orca-cli
orca skills get orchestration --full
```

On Linux outside an Orca-managed terminal, use `orca-ide`; bare `/usr/bin/orca` is commonly the GNOME Orca screen reader. Prefer `--json` for agent-driven CLI calls.

## Pilot guidance

Start with `orca-cli` and `orchestration`. Add `computer-use`, `orca-linear`, emulator skills or per-workspace environments only when a real task requires them. Run a small pilot with two or three low-risk vertical tasks, at most two concurrent coding workers, explicit worktrees, repository-native gates and a separate reviewer. Measure scope violations, skipped commands, review rework, stale dispatches and merge conflicts before adding autonomous coordinator loops or larger concurrency.

## Model-aware routing status

As of 2026-08-18, Orca exposes execution primitives plus optional per-launch model/effort overrides for supported agent/host combinations, but it still does not provide a released, first-class semantic router that deterministically chooses a model per Linear issue or orchestration dispatch. Verified host inventory, capability negotiation and deterministic issue-to-worker branching remain active gaps:

- [Issue #8029](https://github.com/stablyai/orca/issues/8029) asks for model and reasoning/effort selection per worktree specifically because quick and difficult tasks need different configurations; it lists global-default changes, custom commands and manual launch as current workarounds.
- [Issue #1122](https://github.com/stablyai/orca/issues/1122) asks to choose an OpenCode agent and model according to the task.
- [PR #5728](https://github.com/stablyai/orca/pull/5728) implements named launch profiles such as `Codex: Work` using `codex --profile work`, preserving the underlying agent identity. It remained open and unmerged when checked.
- [Issue #2284](https://github.com/stablyai/orca/issues/2284) confirms that the stable UI did not yet ship the documented “Add custom agent” button; an Orca maintainer acknowledged the documentation desynchronization. The earlier custom-agent PRs remained open, so documentation alone is not evidence that the feature exists in a stable build.
- [Issue #10846](https://github.com/stablyai/orca/issues/10846) identifies a deeper orchestration requirement: verified per-host harness × model × effort inventory plus proof of what actually launched. It demonstrates that static catalogs can drift and requested effort preferences can be silently dropped.
- [Issue #11229](https://github.com/stablyai/orca/issues/11229) describes today’s workflow routing choices as custom scripts or probabilistic LLM control flow and proposes a deterministic declarative dispatcher; this directly bounds how “native” an automatic Linear-to-model router currently is.

The practical interim route is a small deterministic adapter that classifies a typed task packet, launches the harness with an explicit model/profile in an isolated worktree and records the requested and observed model. This can optimize model spend, but it is integration glue rather than an Orca-native optimized routing plane. Prefer deterministic labels/risk rules first, reuse an existing Sol planning pass for ambiguous classification rather than paying for a separate Sol call, and escalate from Luna to Terra or Sol only on declared risk or executable failure evidence.

Related: [[entities/tools/hermes-agent]] and [[comparisons/model-routing-hermes-opencode-pi]].
