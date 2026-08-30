---
title: Cloudflare security-audit skill
created: 2026-07-17
updated: 2026-07-18
type: entity
tags: [tool, skill, agent, testing, research, coding, security]
sources: [raw/articles/cloudflare-vulnerability-harness-2026-07-17.md, raw/articles/capitalone-vulnhunter-2026-07-18.md]
confidence: medium
contested: false
contradictions: []
---
# Cloudflare security-audit skill

## Overview

Open-source, MIT-licensed coding-agent skill from Cloudflare for multi-phase security audits. It structures a single-repository audit as reconnaissance, parallel attack-class hunting, adversarial validation, human and machine-readable reporting, schema checks, and a fresh source-grounded verification pass. Its stated design goal is to retain only exploitable, evidenced findings rather than checklist gaps.^[raw/articles/cloudflare-vulnerability-harness-2026-07-17.md]

The artifact is a useful reference for [[coding/architecture/kitdev-deterministic-agentic-workflows]] because it externalizes task outputs, separates discovery from validation, and treats independent verification as a gate. It also complements [[entities/tools/hermes-agent]]: skills are portable instructions, while the harness owns durable task state, authorization, budgets, and integration policy.

## Durable engineering lessons

- **Do not let a hunter grade itself.** A validator that cannot create findings is a concrete separation-of-duties pattern for security or quality workflows.^[raw/articles/cloudflare-vulnerability-harness-2026-07-17.md]
- **Make evidence executable where possible.** The public skill requires concrete attack scenarios and structured findings; the larger Cloudflare workflow additionally describes reproducible tests and proposed patches before human review. This is compatible with repository-native tests as the outcome oracle, not with trusting agent prose.
- **Start with a bounded skill, then add control-plane machinery only at a measured bottleneck.** Cloudflare explicitly recommends a minimal persistent Recon/Hunt/Validate loop before fleet-wide tracing or agentic deduplication.^[raw/articles/cloudflare-vulnerability-harness-2026-07-17.md]
- **Treat vendor performance claims as directional.** The public repository, article, and independent technical analysis demonstrate workflow design and adoption interest, but not an independently replicated security benchmark. Retain conventional SAST, dependency scanning, sandboxing, and human security review.

## Controlled trial guidance

Use a disposable, non-production repository or a deliberately scoped critical component. Predefine an output directory, execution budget, allowed tools, prohibited network/credential access, and a human triage owner. Measure confirmed findings, rejected findings, cost, elapsed time, and duplicate rate against baseline SAST/manual review. Do not permit an autonomous patch merge.

## Sources

- [Cloudflare: Build your own vulnerability harness](https://blog.cloudflare.com/build-your-own-vulnerability-harness/)
- [Public source and installation instructions](https://github.com/cloudflare/security-audit-skill)
- [Independent technical critique](https://starlog.is/articles/ai-agents/cloudflare-security-audit-skill)

## Related

- [[coding/architecture/kitdev-deterministic-agentic-workflows]]
- [[entities/tools/hermes-agent]]
- [[entities/tools/mindwalk]]
- [[entities/tools/vulnhunter]] — a distinct, newer open-source suite that reinforces the same hunt/falsify/verify separation while adding repair and CI components; both require independent effectiveness evaluation.
