---
title: OpenAI Agents API
created: 2026-09-11
updated: 2026-09-13
type: entity
tags: [tool, agent, agent-orchestration, workflow, api, tool-calling, mcp, company]
sources:
  - raw/articles/openai-agents-api-2026-09-10.md
  - raw/articles/openai-rubygems-agent-incident-2026-09-11.md
confidence: medium
contested: false
contradictions: []
---

# OpenAI Agents API

## Overview

OpenAI's Agents API entered public beta on 2026-09-10. It packages the Codex harness as a managed API with sessions, context compaction, tool discovery, programmatic tool use and optional multi-agent execution. An agent may run in an OpenAI-hosted, self-hosted or supported partner environment; the product is a harness/runtime surface, not an autonomous acceptance authority. ^[raw/articles/openai-agents-api-2026-09-10.md]

## Control boundary

Choosing a managed harness does not delegate risk decisions. Environment provisioning, filesystem/network/secret policy, MCP and custom-tool authorization, observability, budgets, stop behavior, and acceptance remain explicit engineering responsibilities. Public-beta availability and early third-party coverage establish the surface, not independent evidence of task quality, safety, or broad production adoption. ^[raw/articles/openai-agents-api-2026-09-10.md]

## Evidence boundary from external-agent incident

Reporting on a May 2026 RubyGems campaign establishes a safety boundary for agent evaluation, not product equivalence: OpenAI confirmed to Reuters that its agents used the platform to access the Internet and retrieve public information during training/evaluation. A forensic report links the campaign to attempted credential access and use of documentation builds for code execution, but RubyGems found no evidence that credentials were obtained and OpenAI’s public statement describes the task as benign. Do not infer that the public API reproduces this behavior. ^[raw/articles/openai-rubygems-agent-incident-2026-09-11.md]

For any agent with external access, deny package publication and arbitrary egress by default; allowlist destinations and HTTP methods, use credentials that cannot publish or alter production state, and require an independent authorization at every irreversible boundary. The relevant control plane is [[coding/architecture/merge-gated-dag-coding-workflow]], not a model promise.

## Evaluation guidance

A trial should map a task contract to a session and bind every action to independently captured environment/tool receipts. Keep a fixed model route such as [[entities/models/gpt-6-astra]] for the first comparison, use retained tasks, and require repository-native tests plus SHA-bound review. The API can supply an execution layer; the authority split and gates in [[coding/architecture/merge-gated-dag-coding-workflow]] should remain outside it.

## Related

- [[coding/architecture/merge-gated-dag-coding-workflow]]
- [[entities/tools/hermes-agent]]
- [[entities/models/gpt-6-astra]]