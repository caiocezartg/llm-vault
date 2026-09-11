---
title: OpenAI Agents API
created: 2026-09-11
updated: 2026-09-11
type: entity
tags: [tool, agent, agent-orchestration, workflow, api, tool-calling, mcp, company]
sources:
  - raw/articles/openai-agents-api-2026-09-10.md
confidence: medium
contested: false
contradictions: []
---

# OpenAI Agents API

## Overview

OpenAI's Agents API entered public beta on 2026-09-10. It packages the Codex harness as a managed API with sessions, context compaction, tool discovery, programmatic tool use and optional multi-agent execution. An agent may run in an OpenAI-hosted, self-hosted or supported partner environment; the product is a harness/runtime surface, not an autonomous acceptance authority. ^[raw/articles/openai-agents-api-2026-09-10.md]

## Control boundary

Choosing a managed harness does not delegate risk decisions. Environment provisioning, filesystem/network/secret policy, MCP and custom-tool authorization, observability, budgets, stop behavior, and acceptance remain explicit engineering responsibilities. Public-beta availability and early third-party coverage establish the surface, not independent evidence of task quality, safety, or broad production adoption. ^[raw/articles/openai-agents-api-2026-09-10.md]

## Evaluation guidance

A trial should map a task contract to a session and bind every action to independently captured environment/tool receipts. Keep a fixed model route such as [[entities/models/gpt-6-astra]] for the first comparison, use retained tasks, and require repository-native tests plus SHA-bound review. The API can supply an execution layer; the authority split and gates in [[coding/architecture/merge-gated-dag-coding-workflow]] should remain outside it.

## Related

- [[coding/architecture/merge-gated-dag-coding-workflow]]
- [[entities/tools/hermes-agent]]
- [[entities/models/gpt-6-astra]]