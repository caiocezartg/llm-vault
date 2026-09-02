---
source_url: https://www.anthropic.com/claude-fable-and-mythos-5-1
ingested: 2026-09-02
sha256: 6f38c243151b57891f19a9455d05a97839e364d78b343cb55437aaa239d755b9
---

# Bounded primary-source capture — Claude Fable 5.1 / Mythos 5.1

Anthropic announced Claude Fable 5.1 and Claude Mythos 5.1 on 1 September 2026. They share the same model weights; Fable 5.1 is generally available and Mythos 5.1 is restricted to vetted trusted-access programs for cybersecurity and life-sciences work.

For the API, Fable 5.1 is `claude-fable-5-1`, with a 1M-token context window, 128K maximum output, and adaptive thinking always enabled. Its list price remains US$10/M input and US$50/M output; cache reads cost US$0.25/M tokens, one quarter of the previous Fable cache-read price. Anthropic characterizes the resulting reduction as approximately 25% for typical workloads and up to 45% for highly agentic workloads; these are vendor estimates.

The migration surface is material: forced tool selection (`tool_choice` type `any` or a named `tool`) returns HTTP 400; earlier Claude models cannot read Fable 5.1 thinking blocks; and editing a prior message, system prompt or tools array can invalidate later thinking blocks. Anthropic documents append-only history, server-side context editing/compaction, and explicit `input_transformations` logging as the migration-safe path.

Anthropic states that general-access Fable 5.1 may discover vulnerabilities in source code but not develop exploits. Its primary documentation says Fable 5.1 and Mythos 5.1 carry 30-day data retention unless Anthropic expressly authorizes zero-data-retention access. The announcement separately describes a time-bound enterprise ZDR exemption while Enterprise Frontier Safeguards is rolled out.

Source URLs consulted:
- https://www.anthropic.com/claude-fable-and-mythos-5-1
- https://platform.claude.com/docs/en/models/fable-5-1/whats-new-fable-5-1
- https://www.anthropic.com/claude-fable-5-1-mythos-5-1-system-card
