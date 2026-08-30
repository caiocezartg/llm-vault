---
title: QM
created: 2026-08-02
updated: 2026-08-02
type: entity
tags: [tool, agent, agent-orchestration, multi-agent, workflow, coding, repository]
sources: [raw/articles/yc-qm-v014-2026-08-02.md]
confidence: medium
contested: false
contradictions: []
---

# QM

## Overview

QM is Y Combinator's MIT-licensed, open-source harness for company-wide agent work. It separates personal and shared scopes and exposes Slack/web interfaces, persisted sessions and memory, scoped files/permissions, scheduled work, skills, and per-scope durable sandboxes. Its core can be driven by Pi, OpenCode, Codex, or Claude Code rather than binding deployment to one agent harness. ^[raw/articles/yc-qm-v014-2026-08-02.md]

## Current release and operational boundary

`v0.1.4` shipped on 31 July 2026. It constrains the web model picker to the organization allowed-model list, a small but relevant policy-control surface. The documented modes are Strict, Auto, and Dangerous; predeclared hard-deny/approval command policy remains active even in Dangerous mode. This is a promising governance boundary, not evidence that the system is safe or effective in a production organization. ^[raw/articles/yc-qm-v014-2026-08-02.md]

## Fit and evaluation guidance

QM overlaps with [[entities/tools/hermes-agent]] at the multi-profile/skills/cron layer and with [[coding/architecture/merge-gated-dag-coding-workflow]] at the execution-control layer. The differentiator is organization-scoped collaboration across Slack/web and a selectable harness behind a common core. Evaluate it as a bounded self-hosted pilot: synthetic data, non-production credentials, one shared workflow, fixed command/egress policy, explicit trace collection, and repository-native acceptance gates. Do not treat its per-scope sandbox or Auto classifier as a complete trust boundary.

## Open questions

- Which isolation guarantees are actually enforced by the chosen sandbox implementation and deployment layer?
- How do scoped memory, shared rooms, skills, and external-content screening behave under prompt injection and cross-user data exposure?
- What is the measured cost, failure rate, and human-review burden for common engineering workflows compared with a smaller Hermes/OpenCode bridge?

## Sources

- [[raw/articles/yc-qm-v014-2026-08-02]] — primary release and repository documentation.
- https://news.ycombinator.com/item?id=49126604 — early technical discussion; attention is not adoption evidence.
