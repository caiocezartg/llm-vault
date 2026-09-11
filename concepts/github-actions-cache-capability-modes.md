---
title: GitHub Actions Cache Capability Modes
created: 2026-09-11
updated: 2026-09-11
type: concept
tags: [workflow, devops, testing, api, coding]
sources:
  - raw/articles/github-actions-cache-mode-2026-09-10.md
confidence: high
contested: false
contradictions: []
---

# GitHub Actions Cache Capability Modes

GitHub Actions `cache-mode`, generally available on 2026-09-10, makes cache authority declarative at workflow or job scope: `read`, `write`, `write-only`, or `none`. The cache service enforces the selected capability, and a reusable workflow cannot receive broader cache access than its caller grants. ^[raw/articles/github-actions-cache-mode-2026-09-10.md]

The durable pattern is to make shared cache access reviewable rather than infer it from a trigger: low-trust pull-request jobs can restore trusted cache but not publish it; a clean trusted seeder can publish without restoring shared state; reproducibility checks can use no cache. Explicit `write` on a low-trust trigger is still an escalation, and GitHub's warning does not replace a policy/gate that prevents it. ^[raw/articles/github-actions-cache-mode-2026-09-10.md]

Cache denials may look like cache misses rather than job failures, so a hardened migration needs timing/runner-cost observation and a deterministic clean-build test. This control belongs in the same authority boundary as scoped tools, credentials and independent verification in [[coding/architecture/merge-gated-dag-coding-workflow]]; it complements but does not replace host/environment containment for agents in [[entities/tools/hermes-agent]].

## Related

- [[coding/architecture/merge-gated-dag-coding-workflow]]
- [[entities/tools/hermes-agent]]
- [[projects/hermes-research-daily-radar]]